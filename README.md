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

Codex uses two durable instruction surfaces here:

- `AGENTS.md` for project conventions, commands, and review expectations.
- `.agents/skills/<skill-name>/SKILL.md` for reusable, task-specific workflows that Codex can invoke explicitly or implicitly.

For this repo, the bundled Codex-native skills are already checked in under `.agents/skills/`. Copy that directory into a project and start Codex from the project root so the skills are discoverable.

For personal skills that should apply across projects, put them in:

```text
~/.agents/skills/<skill-name>/SKILL.md
```

For reusable distribution to other developers, prefer packaging skills as a Codex plugin. The older `openai/skills` catalog is deprecated; use it only for local experimentation with legacy curated or experimental skills.

Legacy local install examples:

```bash
# List legacy curated skills
python ~/.codex/skills/.system/skill-installer/scripts/list-skills.py

# Install a legacy curated skill
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo openai/skills \
  --path skills/.curated/<skill-name>

# Install a legacy experimental skill
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo openai/skills \
  --path skills/.experimental/<skill-name>
```

Restart Codex after adding or installing skills if they do not appear automatically.

### Use A Particular Codex Skill

Start Codex from the project root so `.agents/skills` is scanned. Then use one of these patterns:

```text
Use .agents/skills/agentic-formal-feature/SKILL.md and AGENTS.md for this task.
```

```text
Use the agentic-role-review skill from .agents/skills. Review this diff for API compatibility, lifecycle/concurrency, performance, security, test matrix, docs, and release readiness. Findings first.
```

If your Codex surface supports skill discovery, check the loaded skills with:

```text
/skills
```

Expected bundled skills:

```text
agentic-lightweight-loop
agentic-formal-feature
agentic-role-review
framework-contract-review
```

## gstack-Style Reviews

gstack is treated as an optional external review-and-ship layer. This repo does not install gstack. To use real gstack commands, install the gstack package/plugin from your team or vendor source in the agent surface that supports those slash commands, usually Claude Code. Verify installation by checking that commands such as `/office-hours`, `/review`, `/qa`, `/cso`, and `/ship` appear in that surface's slash-command list.

Use gstack with the bundled skills like this:

1. **Before implementation**: use `agentic-lightweight-loop` for small tasks or `agentic-formal-feature` for risky work.
2. **Plan challenge**: if gstack is available, run `/office-hours`, `/autoplan`, `/plan-eng-review`, and `/plan-devex-review` on the plan.
3. **Implementation**: use Codex or Claude to make the patch, following `AGENTS.md` and the selected skill.
4. **Pre-handoff review**: if gstack is available, run `/review`, `/qa`, `/cso`, `/benchmark` when relevant, and `/ship` before release.
5. **Fallback**: if gstack is not installed, use the bundled `agentic-role-review` skill to run the same review lenses locally.

Command mapping:

| Need | gstack command if installed | Bundled fallback |
|---|---|---|
| Product challenge | `/office-hours` | `agentic-role-review` Product Challenger |
| Initial patch plan | `/autoplan` | `agentic-formal-feature` architecture plan |
| Engineering review | `/plan-eng-review`, `/review` | `agentic-role-review` Architecture/API/Lifecycle lenses |
| Developer experience | `/plan-devex-review`, `/devex-review` | `agentic-role-review` DevEx/Error Model lenses |
| QA | `/qa`, `/qa-only` | `agentic-role-review` QA/Test Matrix lenses |
| Security | `/cso` | `agentic-role-review` Security & Abuse lens |
| Performance | `/benchmark` | `framework-contract-review` Performance Regression Guard |
| Release readiness | `/ship`, `/land-and-deploy` | `agentic-role-review` Release Manager lens |

Fallback prompt for Codex:

```text
Use .agents/skills/agentic-role-review/SKILL.md and AGENTS.md. Run a gstack-style review of this plan/diff across product, architecture, devex, API compatibility, lifecycle/concurrency, performance, security, QA, docs, test matrix, and release readiness. Findings first.
```

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
