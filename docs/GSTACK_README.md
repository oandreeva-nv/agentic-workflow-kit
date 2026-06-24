# gstack

gstack is Garry Tan's Claude Code setup for turning Claude Code into a virtual product/engineering/release team. It provides specialist slash commands for product challenge, architecture review, design review, QA, security, performance, documentation, and shipping.

## Upstream

| Resource | Link |
|---|---|
| GitHub repo | https://github.com/garrytan/gstack |

## Install

### Claude Code

The upstream README documents this install prompt for Claude Code:

```text
Install gstack: run `git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup` then add a "gstack" section to CLAUDE.md that says to use the /browse skill from gstack for all web browsing, never use mcp__claude-in-chrome__* tools, and lists the available skills.
```

Team mode from inside a repo:

```bash
(cd ~/.claude/skills/gstack && ./setup --team) && ~/.claude/skills/gstack/bin/gstack-team-init required && git add .claude/ CLAUDE.md && git commit -m "require gstack for AI-assisted work"
```

Use `optional` instead of `required` if you want to nudge teammates rather than block them.

### Codex And Other Agents

gstack also documents multi-host setup:

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/gstack
cd ~/gstack && ./setup
```

Target Codex explicitly:

```bash
./setup --host codex
```

The upstream README says Codex skills install to `~/.codex/skills/gstack-*/`.

## Use

Quick-start commands from upstream:

```text
/office-hours
/plan-ceo-review
/plan-eng-review
/review
/qa
/ship
```

Common command groups:

| Need | Commands |
|---|---|
| Product and planning | `/office-hours`, `/autoplan`, `/plan-ceo-review`, `/plan-eng-review`, `/plan-design-review`, `/plan-devex-review` |
| Engineering review | `/review`, `/devex-review`, `/careful`, `/freeze`, `/guard`, `/unfreeze` |
| QA and investigation | `/qa`, `/qa-only`, `/investigate`, `/benchmark`, `/canary` |
| Security | `/cso` |
| Shipping | `/ship`, `/land-and-deploy`, `/document-release`, `/document-generate`, `/retro` |
| Tooling | `/browse`, `/connect-chrome`, `/setup-deploy`, `/gstack-upgrade`, `/learn`, `/codex` |

## Codex Fallback

If real gstack is not installed, use this repo's local review skill:

```text
Use .agents/skills/agentic-role-review/SKILL.md and AGENTS.md.
Run a gstack-style review of this plan/diff across product, architecture, devex, API compatibility, lifecycle/concurrency, performance, security, QA, docs, test matrix, and release readiness. Findings first.
```

## Notes

- gstack is an installable product. Do not claim it ran unless the command actually ran.
- If installed for Codex, invoke the installed gstack skills using the Codex skill/plugin UI for your surface.
- Use this repo's fallback only when gstack is absent.
