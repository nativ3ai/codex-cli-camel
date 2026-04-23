# CaMeL How It Works

This page maps Google DeepMind's CaMeL methodology to the runtime flow in `codex-cli-camel`.

References:
- arXiv: https://arxiv.org/abs/2503.18813
- Google repo: https://github.com/google-research/camel-prompt-injection

## Explorable graph

```mermaid
flowchart TD
    A[User Input] --> B[Pre-turn Input Scan]
    B --> C{Score >= Threshold?}
    C -- No --> D[Build Full Runtime Context]
    C -- Yes --> E{Mode}
    E -- monitor --> F[Warn and Continue]
    E -- enforce --> G[Block Turn]
    F --> D
    D --> H[Pre-sampling Context Scan]
    H --> I{Score >= Threshold?}
    I -- No --> J[Model Sampling]
    I -- Yes --> K{Mode}
    K -- monitor --> L[Warn and Continue]
    K -- enforce --> M[Block Sampling]
    L --> J
    J --> N[Assistant Output]

    O[Controls] --> P[codex camel activate --mode monitor|enforce --threshold N]
    O --> Q[CODEX_CAMEL_GUARD_MODE]
    O --> R[CODEX_CAMEL_GUARD_THRESHOLD]
    P --> B
    Q --> E
    Q --> K
    R --> C
    R --> I
```

## Tree view

<details>
<summary><strong>Runtime Tree</strong></summary>

- CaMeL guard pipeline
  - Input boundary
    - pre-turn user/input scan
    - decision:
      - below threshold: continue
      - above threshold + monitor: warn, continue
      - above threshold + enforce: block turn
  - Context boundary
    - pre-sampling context/tool-output scan
    - decision:
      - below threshold: sample normally
      - above threshold + monitor: warn, continue
      - above threshold + enforce: block sampling
  - Output
    - normal assistant response (if not blocked)
- Controls
  - persisted config (`~/.codex/config.toml`)
    - `[camel_guard].enabled`
    - `[camel_guard].mode`
    - `[camel_guard].threshold`
  - environment overrides
    - `CODEX_CAMEL_GUARD_MODE`
    - `CODEX_CAMEL_GUARD_THRESHOLD`
- Validation
  - benchmark harness: `benchmarks/camel_guard/benchmark.py`
  - runtime compare: `codex camel compare`
  - report artifact: `benchmarks/camel_guard/latest.json`

</details>

## Mapping table

| CaMeL methodology concept | `codex-cli-camel` implementation |
| --- | --- |
| Treat external/tool text as untrusted | Pre-sampling context scan over tool and message context |
| Prevent instruction override | Weighted guard policy + threshold gate |
| Apply controls at runtime boundaries | Pre-turn and pre-sampling checks |
| Stage deployment safely | `monitor` first, `enforce` when stable |
| Measure behavior continuously | Benchmark harness and mode comparison |
