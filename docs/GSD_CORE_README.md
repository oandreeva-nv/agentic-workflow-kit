# GSD Core / Get Shit Done

This guide documents the lightweight spec and phase-control layer.

## Status In This Kit

GSD Core is treated as a methodology shape, not a bundled dependency. This kit implements the practical version through `AGENTS.md` and the local skills.

## Role In The Stack

GSD is the low-overhead spine for most agent work:

```text
context -> scope -> plan -> implement -> verify -> handoff
```

Use it when DAE or Superpowers would be too heavy, but direct editing would be too loose.

## Codex Invocation

```text
Use AGENTS.md and .agents/skills/agentic-lightweight-loop/SKILL.md.
Run a GSD-style loop: gather context, state scope and non-goals, propose a narrow plan, implement the smallest safe patch, verify with relevant commands, and summarize evidence plus residual risk.
```

For higher-risk work:

```text
Use AGENTS.md and .agents/skills/agentic-formal-feature/SKILL.md.
Run a GSD-style formal feature flow: Ready contract, acceptance criteria, plan, test matrix, implementation, validation, and handoff.
```

## Phase Rules

| Phase | Required Output |
|---|---|
| Context | files, tests, constraints, relevant docs |
| Scope | behavior change, non-goals, risk |
| Plan | ordered patch steps and validation plan |
| Implement | narrow diff, no unrelated cleanup |
| Verify | commands run and results |
| Handoff | changed behavior, evidence, risks, next action |

## Guardrails

- Keep the loop lightweight.
- Do not ask for a full spec when scope is already obvious and low risk.
- Do not implement before stating the validation plan for risky work.
- Do not let phase labels become a substitute for tests or review.
