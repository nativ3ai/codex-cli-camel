# CaMeL Research Mapping (Codex CLI Fork)

This fork applies the same CaMeL-oriented protection strategy used in Hermes Agent CaMeL, adapted to Codex CLI runtime boundaries.

## Reference

- Paper: **Defending LLMs against Prompt Injection Attacks with CaMeL**
- Repo: https://github.com/google-research/camel-prompt-injection

## Runtime Mapping in `codex-cli-camel`

- **Pre-turn input scan**: user payloads are evaluated before the turn is executed.
- **Pre-sampling context scan**: the full model input context (messages + tool outputs) is evaluated before sending the sampling request.
- **Mode controls**:
  - persisted in config via `codex camel activate --mode monitor|enforce --threshold <n>`
  - environment override via `CODEX_CAMEL_GUARD_MODE=off|monitor|enforce`
- **Threshold control**:
  - persisted threshold in `[camel_guard].threshold`
  - environment override via `CODEX_CAMEL_GUARD_THRESHOLD=<int>`

## Detection Philosophy

This fork intentionally uses a deterministic weighted heuristic policy for operational reliability and low overhead, while preserving the same intent as CaMeL: separate trusted instructions from untrusted prompt/tool channels and reduce instruction override success.

## Limits

- Heuristic guardrails are not equivalent to full formal defenses.
- Current hook/runtime coverage can still be bypassed by adversarial multi-turn transformations.
- Guarding should be paired with approval policy, sandboxing, and execution controls.
