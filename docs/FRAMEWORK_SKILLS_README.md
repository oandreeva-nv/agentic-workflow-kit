# Framework-Specific Custom Skills

This guide documents how to add project or framework-specific skills on top of the generic workflow skills.

## Status In This Kit

The bundled skills are intentionally framework-agnostic:

- `agentic-lightweight-loop`
- `agentic-formal-feature`
- `agentic-role-review`
- `framework-contract-review`

Framework-specific skills should be added per project or packaged as a Codex plugin when they are reusable across projects.

## When To Create A Custom Skill

Create one when a framework has stable rules that agents repeatedly need:

- public API compatibility policy
- lifecycle/resource ownership model
- plugin or extension-point constraints
- supported version matrix
- migration and deprecation process
- error model and logging conventions
- performance-sensitive hot paths
- docs/examples that must stay runnable

Do not create a skill for one-off task instructions.

## Codex Skill Location

Repo-local skill:

```text
.agents/skills/<framework>-contract-review/SKILL.md
```

Personal skill:

```text
~/.agents/skills/<framework>-contract-review/SKILL.md
```

Claude Code compatibility mirror, if needed:

```text
.claude/skills/<framework>-contract-review/SKILL.md
```

## Minimal Skill Template

```markdown
---
name: <framework>-contract-review
description: Use for <framework> public API, lifecycle, compatibility, performance, security, docs, and release-risk changes.
---

Read AGENTS.md and the nearest subsystem guidance first.

For this framework, review:
1. API contract and compatibility
2. lifecycle, cancellation, cleanup, and concurrency
3. error model and diagnostics
4. performance-sensitive paths
5. security and extension-point abuse cases
6. dependency and version matrix impact
7. docs, examples, and migration notes
8. release readiness

Report findings first, ordered by severity, with file/line references when possible.
```

## Invocation

```text
Use .agents/skills/<framework>-contract-review/SKILL.md and AGENTS.md.
Review this plan/diff for framework contract risk. Findings first.
```

## Guardrails

- Keep each skill focused.
- Prefer references to repo docs over duplicating large policy text.
- Include concrete commands only when they are stable for that project.
- Mirror to `.claude/skills` only if Claude Code users need the same workflow.
