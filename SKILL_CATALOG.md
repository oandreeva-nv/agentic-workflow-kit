# Skill Catalog

This repo bundles local workflow skills and documents external skill systems that must be installed separately.

## Bundled Local Skills

These are project-local Claude Code skills under `.claude/skills/`. After copying this repo into a project, launch Claude Code from the project root and run `/skills` to verify discovery.

| Skill | Use When | File |
|---|---|---|
| `agentic-lightweight-loop` | Routine bug fixes, small features, local refactors | `.claude/skills/agentic-lightweight-loop/SKILL.md` |
| `agentic-formal-feature` | Risky feature work needing spec, acceptance criteria, architecture plan, TDD, and hardening | `.claude/skills/agentic-formal-feature/SKILL.md` |
| `agentic-role-review` | gstack-style product/architecture/devex/QA/security/performance/ship review | `.claude/skills/agentic-role-review/SKILL.md` |
| `framework-contract-review` | Framework/library/API work with compatibility, lifecycle, performance, docs, tests, and release risk | `.claude/skills/framework-contract-review/SKILL.md` |

## External Skills And Tools

These are not bundled here. This repo provides prompts, command mappings, and local fallback skills.

| External System | Status In This Repo | How To Use |
|---|---|---|
| Disciplined Agentic Engineering / ATDD | Install separately as Claude Code plugins | Use `/plugin marketplace add swingerman/disciplined-agentic-engineering`, then install `engineer`, `atdd`, and `crap-analyzer` |
| gstack | Install separately | Use real slash commands when available; otherwise use `agentic-role-review` as the local fallback |
| Superpowers | Install separately if you use that pack | Use `agentic-formal-feature` as the local fallback shape: brainstorm -> clarify -> plan -> isolate -> TDD -> review -> finish |
| GSD Core / Get Shit Done | Install separately if you use that pack | Use `agentic-formal-feature` as the local fallback for phase control and spec/context engineering |
| Context Engineering Kit | Install separately if you use that pack | Use `agentic-formal-feature` and `agentic-role-review` as local substitutes |
| Context7 or official-doc lookup | Configure in your agent/editor environment | Use for external APIs and fast-changing docs before relying on memory |
| ponytail | Not bundled; no verified install source is encoded here | Add an adapter skill once your local ponytail installation and commands are known |

## Claude Code Install

Copy the files into a project:

```bash
cp AGENTS.md CLAUDE.md SKILL_CATALOG.md /path/to/project/
mkdir -p /path/to/project/.claude /path/to/project/.codex
cp -R .claude/AGENTIC_WORKFLOW.md .claude/README.md .claude/skills /path/to/project/.claude/
cp .codex/AGENTS.md /path/to/project/.codex/
```

Then start Claude Code from that project and run:

```text
/skills
```

## Codex Usage

Codex does not use Claude Code slash commands. It reads `AGENTS.md` and can be asked to follow a local skill file explicitly:

```text
Use .claude/skills/agentic-formal-feature/SKILL.md and AGENTS.md for this task.
```

To install Codex-specific skills from the OpenAI skill registry, use:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/list-skills.py
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo openai/skills \
  --path skills/.curated/<skill-name>
```

Restart Codex after installing new Codex skills.
