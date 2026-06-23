# Portable Claude Workflow

This directory contains project-agnostic workflow guidance for Claude Code.

Start Claude Code at the workspace or project root, then read:

```text
AGENTS.md
.claude/AGENTIC_WORKFLOW.md
```

For project-specific skills and agents, keep them in that project's own `.claude/skills/` and `.claude/agents/` directories.

## Bundled Skills

This kit includes project-local Claude Code skills in `.claude/skills/`:

- `agentic-lightweight-loop`
- `agentic-formal-feature`
- `agentic-role-review`
- `framework-contract-review`

Start Claude Code from the project root and run `/skills` to verify they were discovered.
