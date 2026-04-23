# Codex CaMeL Plugin (Medium Protection)

The standalone plugin lives in a separate repository:

- https://github.com/nativ3ai/codex-cli-camel-plugin
- plugin id: `codex-camel-guard`

## Why both plugin and core fork

- Plugin path: faster adoption, medium protection, no binary fork required.
- Core fork path: stronger runtime integration and enforcement in the turn pipeline.

## CaMeL methodology reference

- arXiv paper: https://arxiv.org/abs/2503.18813
- Google research repo: https://github.com/google-research/camel-prompt-injection

## Implementation comparison

| Implementation | Deployment model | Protection posture |
| --- | --- | --- |
| `codex-cli-camel-plugin` | Plugin/hook only | Medium |
| `codex-cli-camel` | Forked binary with core runtime integration | High |
| `hermes-agent-camel` | Hermes runtime integration | High |

## Install and use

See plugin repo README for installation details and hook behavior.

Core hook references:

- Codex Hooks docs: https://developers.openai.com/codex/hooks
- Codex Plugins docs: https://developers.openai.com/codex/plugins/build
