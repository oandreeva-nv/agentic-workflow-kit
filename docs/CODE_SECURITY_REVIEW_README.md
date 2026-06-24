# Code Review And Security Review Tooling

This guide covers actual review/security products that can be used with this workflow. It also shows local fallbacks when those products are unavailable.

## Products / Sources

| Product | Source |
|---|---|
| gstack review, QA, CSO, benchmark, ship commands | https://github.com/garrytan/gstack |
| Codex code review docs | https://developers.openai.com/codex/review |
| Codex Security docs | https://developers.openai.com/codex/security |
| Codex skills docs | https://developers.openai.com/codex/skills |

## Install

### gstack

Install gstack from its upstream repo:

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/gstack
cd ~/gstack && ./setup
```

For Codex specifically:

```bash
cd ~/gstack && ./setup --host codex
```

For Claude Code, see `docs/GSTACK_README.md` or the upstream gstack README.

### Codex Review / Security

Codex review and Codex Security are OpenAI product surfaces, not repo-local skills in this kit. Use the current Codex UI/CLI/plugin instructions from official docs for your environment.

## Use

gstack review commands:

```text
/review
/qa
/qa-only
/cso
/benchmark
/ship
/land-and-deploy
```

Codex review fallback prompt:

```text
Review this diff. Findings first, ordered by severity, with file/line references. Cover correctness, compatibility, lifecycle/concurrency, performance, security, tests, docs, and release risk.
```

Local skill fallback:

```text
Use .agents/skills/agentic-role-review/SKILL.md and AGENTS.md.
Review this diff across product, architecture, devex, API compatibility, lifecycle/concurrency, performance, security, QA, docs, test matrix, and release readiness. Findings first.
```

Framework/API-specific fallback:

```text
Use .agents/skills/framework-contract-review/SKILL.md and AGENTS.md.
Review this framework/API change for public contract, migration, lifecycle, performance, security, docs, test matrix, and release readiness. Findings first.
```

## Evidence Rule

Separate manual review from tool evidence. Say exactly what ran:

- `gstack /cso` ran or did not run
- Codex Security scan ran or did not run
- dependency audit ran or did not run
- tests/linters/benchmarks ran or did not run

Do not imply scanner coverage from a manual prompt review.
