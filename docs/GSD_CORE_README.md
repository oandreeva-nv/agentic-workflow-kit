# GSD Core / Get Shit Done

GSD Core is an open-source meta-prompting, context-engineering, and spec-driven development system for Claude Code, OpenCode, Gemini CLI, Kimi CLI, Kilo, Codex, Copilot, Cursor, Windsurf, and more.

## Upstream

| Resource | Link |
|---|---|
| GitHub repo | https://github.com/open-gsd/gsd-core |
| npm package | https://www.npmjs.com/package/@opengsd/gsd-core |

## What It Does

GSD Core runs a disciplined phase loop for each milestone:

```text
Discuss -> Plan -> Execute -> Verify -> Ship
```

The upstream README frames it as a context-engineering system that keeps the main session lean while heavy research, planning, and execution happen in fresh-context subagents.

## Install

```bash
npx @opengsd/gsd-core@latest
```

The installer prompts for runtime and whether to install globally or locally. The upstream README explicitly says to use the installer for cross-runtime compatibility and not to copy files from `agents/` or `commands/` directly.

## Use

Start a first project:

```text
/gsd-new-project
```

Then follow the phase loop:

```text
Discuss -> Plan -> Execute -> Verify -> Ship
```

Useful upstream docs:

| Topic | Link |
|---|---|
| Install on your runtime | https://github.com/open-gsd/gsd-core/blob/main/docs/how-to/install-on-your-runtime.md |
| Your first project | https://github.com/open-gsd/gsd-core/blob/main/docs/tutorials/your-first-project.md |
| Commands reference | https://github.com/open-gsd/gsd-core/blob/main/docs/COMMANDS.md |
| Configuration | https://github.com/open-gsd/gsd-core/blob/main/docs/CONFIGURATION.md |

## Codex Use

Install GSD Core with the upstream installer and choose Codex when prompted. If you do not have GSD installed, use this repo's formal feature skill as a local substitute:

```text
Use AGENTS.md and .agents/skills/agentic-formal-feature/SKILL.md.
Run a GSD-style loop: discuss/context, plan, execute, verify, and ship handoff. Keep phase outputs explicit and do not implement before the validation plan is clear.
```

## Notes

- GSD Core is an actual product with a runtime installer.
- Prefer the installer over copying files manually.
- Keep GSD artifacts in the repo only when they are intended to be durable project context.
