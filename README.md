# Agentic Workflow Kit

Portable agent workflow files for using Codex, Claude Code, DAE/ATDD, gstack-style reviews, Superpowers/GSD-style planning, and official-docs lookup across software projects.

The kit is intentionally project-agnostic. Copy it into a workspace or project root, then add project-specific rules in the nearest `AGENTS.md` or `CLAUDE.md`.

## What Is Included

```text
AGENTS.md                       # portable workflow policy for coding agents
CLAUDE.md                       # Claude Code entrypoint that imports AGENTS.md
SKILL_CATALOG.md                # explicit inventory of bundled and external skills
.claude/AGENTIC_WORKFLOW.md     # commands, prompts, and workflow examples
.claude/README.md               # short Claude Code orientation
.agents/skills/*/SKILL.md       # bundled Codex-native skills
.claude/skills/*/SKILL.md       # Claude Code compatibility mirror
.codex/AGENTS.md                # Codex-specific lightweight guidance
```

## Install Into A Project

From this repository:

```bash
cp AGENTS.md CLAUDE.md SKILL_CATALOG.md /path/to/project/
mkdir -p /path/to/project/.agents /path/to/project/.claude /path/to/project/.codex
cp .claude/AGENTIC_WORKFLOW.md .claude/README.md /path/to/project/.claude/
cp -R .agents/skills /path/to/project/.agents/
cp -R .claude/skills /path/to/project/.claude/
cp .codex/AGENTS.md /path/to/project/.codex/
```

Then add project-specific guidance in `/path/to/project/AGENTS.md` or a nested subsystem `AGENTS.md` as needed. Nearest guidance should override this portable workflow.

## Recommended Stack

Use these as layers, not as a required sequence for every patch:

1. **Repo guidance**: `AGENTS.md`, subsystem docs, coding standards, and local tests.
2. **Lightweight spec spine**: GSD-style context, scope, plan, validation, and handoff.
3. **Formal feature discipline**: Superpowers or DAE-style brainstorm, ready contract, acceptance criteria, plan, TDD, review, finish.
4. **Review and ship layer**: gstack-style product, architecture, devex, QA, security, benchmark, and release reviews.
5. **Docs lookup**: Context7 or equivalent official-docs lookup for external or fast-changing APIs.

## Bundled Local Skills

This repo includes Codex-native skills under `.agents/skills/` and a Claude Code compatibility mirror under `.claude/skills/`:

| Skill | Purpose |
|---|---|
| `agentic-lightweight-loop` | Routine context -> plan -> implement -> verify -> handoff loop |
| `agentic-formal-feature` | GSD/Superpowers/DAE-style formal spec and implementation workflow |
| `agentic-role-review` | gstack-style multi-role review and ship-readiness layer |
| `framework-contract-review` | Framework/API compatibility, lifecycle, performance, security, docs, test matrix, and release review |

See `SKILL_CATALOG.md` for the full inventory and external install notes.

## Claude Code Setup

Claude Code reads `CLAUDE.md`, which imports `AGENTS.md`. Start Claude Code from the project root and use the prompts in `.claude/AGENTIC_WORKFLOW.md`.

To install Disciplined Agentic Engineering plugins in Claude Code:

```text
/plugin marketplace add swingerman/disciplined-agentic-engineering
/plugin install engineer@disciplined-agentic-engineering
/plugin install atdd@disciplined-agentic-engineering
/plugin install crap-analyzer@disciplined-agentic-engineering
```

Typical DAE feature flow:

```text
/engineer.onboard
/engineer.discuss
/engineer.feature-init
/engineer.prime-context
/engineer.discover-acs
/engineer.atdd
/engineer.plan
/atdd:atdd-team
/engineer.refine
/engineer.arch-check
/atdd:mutate
/engineer.session-summary
```

Use DAE for risky features, not routine cleanup.

## Codex Skills

Codex always reads relevant `AGENTS.md` guidance. Repo-local Codex skills live in `.agents/skills/`; launch Codex from the project so those skills are discoverable. Additional user-level Codex skills can be installed into `~/.agents/skills` or via the skill installer.

`openai/skills` is deprecated in favor of current plugin examples, but it can still be useful for curated local installs. List curated Codex skills:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/list-skills.py
```

Install a curated skill:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo openai/skills \
  --path skills/.curated/<skill-name>
```

Install an experimental skill:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo openai/skills \
  --path skills/.experimental/<skill-name>
```

Restart Codex after installing skills.

## gstack-Style Reviews

If gstack is installed, use these around planning and before shipping:

```text
/office-hours
/autoplan
/plan-eng-review
/plan-devex-review
/review
/qa
/cso
/benchmark
/ship
```

If the slash commands are unavailable, ask Codex or Claude to perform the same named role review explicitly.

## Default Prompts

Lightweight task:

```text
Follow AGENTS.md. First inspect the touched subsystem and restate:
1. behavior change
2. non-goals
3. files likely to change
4. narrow validation plan

Then implement the smallest safe patch, run relevant tests, and review the diff for regressions.
```

Formal feature:

```text
Use a formal spec-driven workflow:
1. draft the Ready contract
2. list acceptance criteria in domain language
3. write Gherkin scenarios only if they add executable clarity
4. propose the architecture plan and test matrix
5. wait for approval before implementation
6. implement with acceptance/integration tests plus unit tests
7. run role-based review before handoff
```

Role review:

```text
Review this diff as:
- API Contract Guardian
- Compatibility & Migration Reviewer
- Error Model Designer
- Lifecycle & Concurrency Reviewer
- Performance Regression Guard
- Security & Abuse Reviewer
- Dependency Gatekeeper
- Docs-as-Tests Reviewer
- Test Matrix Reviewer
- Release Readiness Reviewer

Report findings first, with file and line references.
```

## License

Add the license appropriate for your organization before publishing publicly.
