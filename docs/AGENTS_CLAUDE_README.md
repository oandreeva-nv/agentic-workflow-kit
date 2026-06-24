# Repo AGENTS.md / CLAUDE.md Guidance

`AGENTS.md` and `CLAUDE.md` are durable instruction files for coding agents. They are not one installable product, but they are real agent configuration surfaces.

## Upstream / Product Sources

| Surface | Source |
|---|---|
| OpenAI Codex `AGENTS.md` guidance | https://developers.openai.com/codex/customization |
| AGENTS.md convention | https://agents.md |
| Claude Code memory / `CLAUDE.md` docs | https://docs.anthropic.com/en/docs/claude-code/memory |

## Install

There is no package install. Add files to the repo:

```text
AGENTS.md
CLAUDE.md
.codex/AGENTS.md       # optional Codex-specific local notes
.claude/README.md      # optional Claude orientation
```

Copy this kit's portable files into a project:

```bash
cp AGENTS.md CLAUDE.md SKILL_CATALOG.md /path/to/project/
cp .codex/AGENTS.md /path/to/project/.codex/
cp .claude/README.md /path/to/project/.claude/
```

## Use

Codex: start from the project root so Codex discovers `AGENTS.md` and `.agents/skills`.

```text
Follow AGENTS.md. Before editing, read the nearest subsystem guidance and identify the validation commands for this change.
```

Claude Code: start from the project root. `CLAUDE.md` should point Claude to shared repo guidance and any Claude-only plugin notes.

## What Belongs Where

| File | Use For |
|---|---|
| `AGENTS.md` | Stable repo rules, commands, tests, architecture boundaries, review expectations |
| nested `AGENTS.md` | Subtree-specific rules that override root guidance |
| `CLAUDE.md` | Claude Code entrypoint and Claude-specific plugin/slash-command notes |
| `.codex/AGENTS.md` | Codex-specific lightweight guidance when needed |

## Notes

- Put durable repo policy in `AGENTS.md`, not in prompts.
- Keep `CLAUDE.md` thin and tool-specific.
- Do not duplicate large policy blocks across both files.
