# Repo AGENTS.md / CLAUDE.md Guidance

This guide documents the durable repo instruction layer.

## Files

| File | Purpose |
|---|---|
| `AGENTS.md` | Shared coding-agent rules, workflows, tool routing, review lenses, and verification expectations |
| `CLAUDE.md` | Claude Code entrypoint that imports or points to shared repo guidance |
| `.codex/AGENTS.md` | Codex-specific lightweight notes, when needed |
| `.claude/AGENTIC_WORKFLOW.md` | Operating guide for prompts, stack layers, and handoffs |

## Scope Rules

Use `AGENTS.md` for durable instructions that should apply to everyone working in the repo. Use nested `AGENTS.md` files only when a subtree has different commands, conventions, or risks.

Use prompt/thread context for one-off task constraints. Do not put temporary task details into `AGENTS.md`.

## What Belongs In AGENTS.md

- build, test, lint, and validation commands
- architecture boundaries
- coding conventions
- public API compatibility rules
- security and secrets handling rules
- review expectations
- known generated files or files not to edit
- how to update reusable skills or docs

## What Belongs In CLAUDE.md

- Claude Code entrypoint guidance
- links to shared `AGENTS.md`
- Claude-specific slash-command or plugin notes
- references to `.claude/AGENTIC_WORKFLOW.md`

Keep `CLAUDE.md` thin when possible. The shared rules should live in `AGENTS.md`.

## Codex Usage

Codex reads relevant `AGENTS.md` guidance. Start Codex from the project root so repo guidance and `.agents/skills` are discoverable.

```text
Follow AGENTS.md. Before editing, read the nearest subsystem guidance and identify the validation commands for this change.
```

## Guardrails

- Nearest repo guidance wins for files under its subtree.
- Do not duplicate long policies between `AGENTS.md`, `CLAUDE.md`, and workflow guides.
- Keep repo guidance factual and stable.
- Put volatile tool install details in dedicated docs instead of `AGENTS.md`.
