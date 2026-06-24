# Framework-Specific Custom Skills

Framework-specific custom skills are Codex/Claude skills you create for a particular framework, library, API surface, or internal platform. This is not a separate upstream product; it uses the skill systems provided by your coding agent.

## Upstream / Product Sources

| Surface | Source |
|---|---|
| Codex skills docs | https://developers.openai.com/codex/skills |
| Codex plugins docs | https://developers.openai.com/codex/plugins |
| Open Agent Skills standard | https://agentskills.io |

## Install

Repo-local Codex skill:

```text
.agents/skills/<framework>-contract-review/SKILL.md
```

User-level Codex skill:

```text
~/.agents/skills/<framework>-contract-review/SKILL.md
```

Claude Code compatibility mirror when needed:

```text
.claude/skills/<framework>-contract-review/SKILL.md
```

For reusable distribution, package the skill as a Codex plugin rather than copying folders manually.

## Use

Invoke explicitly in Codex:

```text
Use .agents/skills/<framework>-contract-review/SKILL.md and AGENTS.md.
Review this plan/diff for framework contract risk. Findings first.
```

Or by skill name when your Codex surface has discovered it:

```text
Use the <framework>-contract-review skill. Review this public API change for compatibility, lifecycle, performance, security, docs, test matrix, and release readiness.
```

## Minimal Skill Template

```markdown
---
name: <framework>-contract-review
description: Use for <framework> public API, lifecycle, compatibility, performance, security, docs, and release-risk changes.
---

Read AGENTS.md and the nearest subsystem guidance first.

Review:
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

## Notes

- Create a custom skill only when the rules are reused across tasks.
- Keep large references in separate files and link them from `SKILL.md`.
- Prefer project docs over duplicating long framework policy in the skill.
