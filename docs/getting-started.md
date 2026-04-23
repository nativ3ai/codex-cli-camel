# Getting started with codex-cli-camel

## 1. Install and run

```bash
npm install -g codex-camel
codex --help
codex-camel --help
```

If `codex` resolves to another installation, run all commands with `codex-camel`.

Alternative (from source):

```bash
git clone https://github.com/nativ3ai/codex-cli-camel.git
cd codex-cli-camel/codex-rs
cargo run -p codex-cli --
```

## 2. Enable CaMeL guard

```bash
codex camel monitor --threshold 6
codex camel status
```

`threshold` is the score cutoff for triggering CaMeL policy action (`score >= threshold`).
- lower = stricter
- higher = looser
- `6` is the current benchmark baseline

## 3. Validate against malicious samples

```bash
codex camel compare
python3 ../benchmarks/camel_guard/benchmark.py
```

## 4. Move to enforcement

```bash
codex camel enforce --threshold 6
```

If needed, disable quickly:

```bash
codex camel off
```
