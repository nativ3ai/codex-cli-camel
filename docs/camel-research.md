# CaMeL Research Mapping (Codex CLI Fork)

This fork applies the same CaMeL-oriented protection strategy used in Hermes Agent CaMeL, adapted to Codex CLI runtime boundaries.

## Reference

- Paper: **Defending LLMs against Prompt Injection Attacks with CaMeL**
- Repo: https://github.com/google-research/camel-prompt-injection

## Runtime Mapping in `cldex-cli-camel`

- **Pre-turn input scan**: user payloads are evaluated before the turn is executed.
- **Pre-sampling context scan**: the full model input context (messages + tool outputs) is evaluated before sending the sampling request.
- **Mode controls**:
  - `CODEX_CAMEL_GUARD_MODE=off` (default)
  - `CODEX_CAMEL_GUARD_MODE=monitor` (warn only)
  - `CODEX_CAMEL_GUARD_MODE=enforce` (block risky turn)
- **Threshold control**:
  - `CODEX_CAMEL_GUARD_THRESHOLD=<int>` (default `6`)

## Detection Philosophy

This fork intentionally uses a deterministic weighted heuristic policy for operational reliability and low overhead, while preserving the same intent as CaMeL: separate trusted instructions from untrusted prompt/tool channels and reduce instruction override success.

## Limits

- Heuristic guardrails are not equivalent to full formal defenses.
- Current hook/runtime coverage can still be bypassed by adversarial multi-turn transformations.
- Guarding should be paired with approval policy, sandboxing, and execution controls.
