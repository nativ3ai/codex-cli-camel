# CaMeL Research Mapping (Codex CLI Fork)

This fork applies Google's CaMeL methodology to Codex CLI runtime boundaries.

## Reference

- Paper (arXiv): **Defeating Prompt Injections by Design**  
  https://arxiv.org/abs/2503.18813
- Official research repo:  
  https://github.com/google-research/camel-prompt-injection

## Methodology to Runtime Mapping

| CaMeL methodology concept | Codex CLI implementation |
| --- | --- |
| Treat tool/output channels as untrusted data | Pre-sampling context scan over messages and tool outputs |
| Separate control policy from untrusted text | Deterministic weighted guard policy + explicit mode control |
| Enforce policy at runtime boundaries | Pre-turn input scan and pre-sampling context scan hooks |
| Progressive deployment and measurement | `monitor` mode for observation, `enforce` mode for blocking |
| Controlled policy tuning | Threshold in config (`[camel_guard].threshold`) and env override |

## Operational controls

| Control | Location | Values |
| --- | --- | --- |
| Guard mode | `codex camel activate --mode ...` or `CODEX_CAMEL_GUARD_MODE` | `off`, `monitor`, `enforce` |
| Guard threshold | `codex camel activate --threshold ...` or `CODEX_CAMEL_GUARD_THRESHOLD` | Integer score threshold |

## Detection Philosophy

This fork uses a deterministic weighted policy for low overhead and repeatable operations while preserving CaMeL's core objective: reduce instruction-override success by enforcing policy boundaries between trusted instructions and untrusted channels.

## Related implementations

| Project | Role |
| --- | --- |
| `nativ3ai/codex-cli-camel` | Core Codex CLI fork with integrated CaMeL guard |
| `nativ3ai/codex-cli-camel-plugin` | Plugin path with medium-protection deployment |
| `nativ3ai/hermes-agent-camel` | Battle-tested Hermes runtime implementation |

## Limits

- Heuristic guardrails are not equivalent to full formal defenses.
- Current hook/runtime coverage can still be bypassed by adversarial multi-turn transformations.
- Guarding should be paired with approval policy, sandboxing, and execution controls.
