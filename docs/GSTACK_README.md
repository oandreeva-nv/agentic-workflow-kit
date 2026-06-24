# gstack-Style Reviews

This guide documents how this kit uses gstack as an optional review, QA, security, and ship layer.

## Status In This Kit

gstack is not bundled here. Install it separately from your team or vendor source in the agent surface that supports its slash commands, usually Claude Code. If gstack is unavailable, use the local fallback skill `agentic-role-review`.

## Role In The Stack

Use gstack after scope or plan drafting and again before handoff or release:

```text
plan challenge -> engineering review -> QA/security/perf review -> ship readiness
```

## Commands When gstack Is Installed

```text
/office-hours              # product challenge and problem framing
/autoplan                  # initial patch plan
/plan-eng-review           # architecture review
/plan-devex-review         # developer experience review
/review                    # code review
/devex-review              # developer experience review
/qa                        # QA pass
/qa-only                   # QA-only pass
/cso                       # security review
/benchmark                 # performance check
/ship                      # release readiness
/land-and-deploy           # final ship/deploy flow
```

## Local Fallback Mapping

| Need | gstack Command | Local Fallback |
|---|---|---|
| Product challenge | `/office-hours` | `agentic-role-review` Product Challenger |
| Initial plan | `/autoplan` | `agentic-formal-feature` plan |
| Engineering review | `/plan-eng-review`, `/review` | `agentic-role-review` architecture/API/lifecycle lenses |
| Developer experience | `/plan-devex-review`, `/devex-review` | `agentic-role-review` devex/error model lenses |
| QA | `/qa`, `/qa-only` | `agentic-role-review` QA/test matrix lenses |
| Security | `/cso` | `agentic-role-review` security and abuse lens |
| Performance | `/benchmark` | `framework-contract-review` performance guard |
| Release readiness | `/ship`, `/land-and-deploy` | `agentic-role-review` release manager lens |

## Codex Fallback Invocation

```text
Use .agents/skills/agentic-role-review/SKILL.md and AGENTS.md.
Run a gstack-style review of this plan/diff across product, architecture, devex, API compatibility, lifecycle/concurrency, performance, security, QA, docs, test matrix, and release readiness. Findings first, ordered by severity, with file/line references where possible.
```

Short form:

```text
Use the agentic-role-review skill for a gstack-style pre-ship review.
```

## Guardrails

- Findings first; summary second.
- Do not treat review roles as approval unless blockers are resolved.
- Do not claim real gstack ran unless the gstack command actually ran.
- Escalate to `framework-contract-review` for public API, lifecycle, compatibility, or release-risk changes.
