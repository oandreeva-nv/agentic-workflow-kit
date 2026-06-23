---
name: agentic-lightweight-loop
tags: [workflow, codex, claude, implementation]
description: >
  Use for routine bug fixes, small features, and local refactors. Provides a
  low-overhead context -> scope -> plan -> implement -> verify -> handoff loop
  that works in Codex or Claude without requiring external plugins.
license: Unlicense
---

# Agentic Lightweight Loop

Use this skill for ordinary implementation work where a formal charter or ATDD flow would add more overhead than value.

## Workflow

1. **Prime context**
   - Read root `AGENTS.md`, nearest project/subsystem guidance, coding standards, touched files, and relevant tests.
   - Prefer project-local patterns over generic methodology.

2. **Clarify scope**
   - Restate the behavior change.
   - Name non-goals.
   - List likely files.
   - Identify risks and the narrow validation plan.

3. **Plan the patch**
   - Split work into reviewable steps.
   - Prefer existing helpers and APIs.
   - Avoid broad refactors unless required.

4. **Implement incrementally**
   - Keep the diff narrow.
   - Preserve public behavior unless explicitly changing it.
   - Add or update tests proportionate to risk.

5. **Verify**
   - Run the smallest meaningful test first.
   - Expand to integration, API stability, performance, or security checks when the change touches those contracts.

6. **Review and handoff**
   - Inspect the diff for regressions, missing tests, API drift, dependency creep, and docs/release needs.
   - Report changed files, verification, residual risk, and next action.

## Prompt

```text
Use the agentic-lightweight-loop skill. Follow AGENTS.md. First inspect the touched subsystem and restate behavior change, non-goals, likely files, risks, and validation plan. Then implement the smallest safe patch, run relevant tests, review the diff, and summarize verification.
```
