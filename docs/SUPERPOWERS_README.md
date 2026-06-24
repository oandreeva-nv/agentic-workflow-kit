# Superpowers

Superpowers is a Claude Code plugin family by Jesse Vincent / `obra`. It provides a curated methodology and skills layer for Claude Code: brainstorming, planning, TDD, debugging, collaboration, plan execution, review, and branch finishing.

## Upstream

| Resource | Link |
|---|---|
| Marketplace | https://github.com/obra/superpowers-marketplace |
| Core plugin repo | https://github.com/obra/superpowers |
| Community skills repo | https://github.com/obra/superpowers-skills |

## Install

Install the marketplace in Claude Code:

```text
/plugin marketplace add obra/superpowers-marketplace
```

Install the core Superpowers plugin:

```text
/plugin install superpowers@superpowers-marketplace
```

The marketplace README says the core plugin provides 20+ skills, `/brainstorm`, `/write-plan`, `/execute-plan`, skills-search, and session-start context injection.

## Use

Typical Claude Code flow:

```text
/brainstorm
/write-plan
/execute-plan
```

Use Superpowers when you want a methodology backbone before implementation: clarify intent, write a reviewable plan, execute incrementally, and review/finish the branch.

## Codex Use

Superpowers itself is a Claude Code plugin. In Codex, use the methodology through local skills or by passing Superpowers-generated artifacts into Codex:

```text
Use AGENTS.md and .agents/skills/agentic-formal-feature/SKILL.md.
Follow the approved Superpowers plan. Implement incrementally, run the relevant tests, and report validation evidence.
```

Local fallbacks in this repo:

| Superpowers Need | Local Codex Skill |
|---|---|
| Lightweight task loop | `.agents/skills/agentic-lightweight-loop/SKILL.md` |
| Plan-first feature work | `.agents/skills/agentic-formal-feature/SKILL.md` |
| Review before handoff | `.agents/skills/agentic-role-review/SKILL.md` |
| Framework/API hardening | `.agents/skills/framework-contract-review/SKILL.md` |

## Notes

- Install and run real Superpowers commands in Claude Code.
- Use Codex for repo scan, implementation, tests, and second opinions.
- Do not document Superpowers commands as Codex commands unless a Codex-native plugin exists.
