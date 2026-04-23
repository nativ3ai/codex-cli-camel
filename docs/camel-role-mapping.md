# CaMeL Role Mapping

This document maps the "Defeating Prompt Injections by Design" CaMeL methodology to `codex-cli-camel` runtime roles.

References:
- arXiv paper: https://arxiv.org/abs/2503.18813
- Google research repo: https://github.com/google-research/camel-prompt-injection

## Role mapping table

| CaMeL role | Trust level | `codex-cli-camel` runtime source | Enforcement behavior |
| --- | --- | --- | --- |
| System policy role | Trusted | system/developer policy + CLI/runtime control plane | Never overridden by untrusted text channels |
| User intent role | Conditionally trusted | direct user prompts/requests | Allowed when below threshold; flagged/blocked when injection patterns score high |
| Tool/output role | Untrusted by default | tool outputs, fetched content, external text | Scanned before sampling; can trigger `monitor` warning or `enforce` block |
| Guard policy role | Trusted | deterministic scoring rules + threshold + mode | Decides `allow`, `warn`, `block` at runtime boundaries |
| Runtime executor role | Trusted with controls | Codex CLI turn pipeline | Applies guard decisions before model sampling/execution |

## Boundary mapping

| Runtime boundary | What is scanned | Why it exists |
| --- | --- | --- |
| Pre-turn input boundary | incoming user payload | catches direct override attempts early |
| Pre-sampling context boundary | full model context (messages + tool outputs) | catches indirect injections introduced by tools/content |

## Mode mapping by role outcome

| Detection outcome | `monitor` mode | `enforce` mode |
| --- | --- | --- |
| score < threshold | allow | allow |
| score >= threshold | warn + continue | block turn/sampling |

## Practical interpretation

- CaMeL's key idea is to keep policy/control channels separate from untrusted text channels.
- In this fork, the separation is operationalized by explicit role boundaries and runtime gates.
- This is defense-in-depth and should be combined with sandboxing and approval policy.
