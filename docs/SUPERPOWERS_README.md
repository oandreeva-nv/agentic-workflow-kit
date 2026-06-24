# Superpowers Workflow

This guide documents how this kit uses Superpowers-style methodology.

## Status In This Kit

Superpowers is treated as an external methodology backbone. This repo does not install an upstream Superpowers package. Instead, it provides local fallback skills that preserve the same shape:

| Need | Local Fallback |
|---|---|
| Brainstorming and scope clarification | `agentic-lightweight-loop` |
| Formal plans and TDD execution | `agentic-formal-feature` |
| Role-based review before handoff | `agentic-role-review` |
| Framework/API hardening | `framework-contract-review` |

## When To Use

Use this layer when a task needs more discipline than a direct edit, but does not necessarily need the full DAE checkpoint pipeline.

Good fits:

- non-trivial feature work
- public API or framework behavior changes
- refactors with test risk
- ambiguous tasks needing discovery before implementation
- work that benefits from a written plan before edits

Use a lighter loop for small bug fixes, comments, formatting, or isolated docs edits.

## Expected Flow

```text
brainstorm -> clarify spec -> write plan -> isolate work -> TDD -> execute plan -> review -> finish branch
```

If you use a real Superpowers installation, run the upstream commands in the agent surface that supports them. If it is unavailable, use the local skills and prompts below.

## Codex Invocation

```text
Use AGENTS.md and .agents/skills/agentic-formal-feature/SKILL.md.
Run this with a Superpowers-style workflow: brainstorm the goal, clarify scope and non-goals, write an implementation plan, identify tests first, implement incrementally, run validation, and review the diff before handoff.
```

For smaller tasks:

```text
Use AGENTS.md and .agents/skills/agentic-lightweight-loop/SKILL.md.
Clarify the behavior change and validation plan, then make the smallest safe patch and review the diff.
```

## Claude Code Invocation

Use the mirrored Claude-compatible skills when you want the same shape in Claude Code:

```text
Use .claude/skills/agentic-formal-feature/SKILL.md and AGENTS.md.
Follow a Superpowers-style plan-first and TDD workflow.
```

## Outputs To Preserve

- clarified behavior change
- non-goals
- implementation plan
- test plan
- validation evidence
- review findings or residual risk

## Guardrails

- Do not add ceremony after the risk is already clear and low.
- Do not skip tests just because the plan is well written.
- Keep the implementation plan tied to files and commands in the actual repo.
- Update `AGENTS.md` or a skill only when the lesson is reusable.
