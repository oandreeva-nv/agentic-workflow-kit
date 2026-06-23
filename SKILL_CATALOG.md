# Skill Catalog

This repo bundles local workflow skills and documents external skill systems that must be installed separately.

## Bundled Local Skills

Primary Codex-native skills live under `.agents/skills/`. Claude Code compatibility copies live under `.claude/skills/`. After copying this repo into a project, launch Codex or Claude Code from the project root and verify discovery with the available skills UI or `/skills`.

| Skill | Use When | Codex Path | Claude Mirror |
|---|---|---|---|
| `agentic-lightweight-loop` | Routine bug fixes, small features, local refactors | `.agents/skills/agentic-lightweight-loop/SKILL.md` | `.claude/skills/agentic-lightweight-loop/SKILL.md` |
| `agentic-formal-feature` | Risky feature work needing spec, acceptance criteria, architecture plan, TDD, and hardening | `.agents/skills/agentic-formal-feature/SKILL.md` | `.claude/skills/agentic-formal-feature/SKILL.md` |
| `agentic-role-review` | gstack-style product/architecture/devex/QA/security/performance/ship review | `.agents/skills/agentic-role-review/SKILL.md` | `.claude/skills/agentic-role-review/SKILL.md` |
| `framework-contract-review` | Framework/library/API work with compatibility, lifecycle, performance, docs, tests, and release risk | `.agents/skills/framework-contract-review/SKILL.md` | `.claude/skills/framework-contract-review/SKILL.md` |

## External Skills And Tools

These are not bundled here. This repo provides prompts, command mappings, and local fallback skills.

| External System | Status In This Repo | How To Use |
|---|---|---|
| Disciplined Agentic Engineering / ATDD | Install separately as Claude Code plugins | Use `/plugin marketplace add swingerman/disciplined-agentic-engineering`, then install `engineer`, `atdd`, and `crap-analyzer` |
| gstack | Optional external package/plugin; not bundled here | Install from your team/vendor source in the surface that supports its slash commands. Use real commands for plan/review/QA/security/ship checks. If unavailable, invoke `.agents/skills/agentic-role-review/SKILL.md` or ask for `agentic-role-review` by name. |
| Superpowers | Install separately if you use that pack | Use `agentic-formal-feature` as the local fallback shape: brainstorm -> clarify -> plan -> isolate -> TDD -> review -> finish |
| GSD Core / Get Shit Done | Install separately if you use that pack | Use `agentic-formal-feature` as the local fallback for phase control and spec/context engineering |
| Context Engineering Kit | Install separately if you use that pack | Use `agentic-formal-feature` and `agentic-role-review` as local substitutes |
| Context7 or official-doc lookup | Configure in your agent/editor environment | Use for external APIs and fast-changing docs before relying on memory |
| ponytail | Not bundled; no verified install source is encoded here | Add an adapter skill once your local ponytail installation and commands are known |
| `openai/skills` | Deprecated upstream catalog; still useful as a source for curated local installs | Prefer current plugin examples for distribution; use `$skill-installer` only for local experimentation |

## Install Into A Project

Copy the files into a project:

```bash
cp AGENTS.md CLAUDE.md SKILL_CATALOG.md /path/to/project/
mkdir -p /path/to/project/.agents /path/to/project/.claude /path/to/project/.codex
cp -R .agents/skills /path/to/project/.agents/
cp -R .claude/AGENTIC_WORKFLOW.md .claude/README.md .claude/skills /path/to/project/.claude/
cp .codex/AGENTS.md /path/to/project/.codex/
```

Then start Claude Code from that project and run:

```text
/skills
```

For Codex, start it from the project root so `.agents/skills` is scanned.

## Codex Usage

Codex reads `AGENTS.md` and can invoke repo-local skills from `.agents/skills` implicitly or explicitly:

```text
Use .agents/skills/agentic-formal-feature/SKILL.md and AGENTS.md for this task.
```

Use `.agents/skills` for project-scoped skills and `~/.agents/skills` for personal skills that should apply across projects. For reusable distribution to other developers, prefer packaging skills as a Codex plugin.

The older `openai/skills` catalog is deprecated. Use it only for local experimentation with legacy curated or experimental skills:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/list-skills.py
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo openai/skills \
  --path skills/.curated/<skill-name>
```

Restart Codex after adding or installing skills if they do not appear automatically.
