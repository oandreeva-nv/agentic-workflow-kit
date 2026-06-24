# Portable Claude Workflow

This directory contains project-agnostic workflow guidance for Claude Code.

Start Claude Code at the workspace or project root, then read:

```text
AGENTS.md
.claude/AGENTIC_WORKFLOW.md
docs/README.md
docs/DAE_README.md
```

For Codex-native project skills, use `.agents/skills/`. For Claude Code compatibility, keep mirror skills in `.claude/skills/` and agents in `.claude/agents/`.

## Bundled Skills

This kit includes Claude Code compatibility skills in `.claude/skills/`, mirrored from the Codex-native `.agents/skills/`:

- `agentic-lightweight-loop`
- `agentic-formal-feature`
- `agentic-role-review`
- `framework-contract-review`

Start Claude Code from the project root and run `/skills` to verify they were discovered.
