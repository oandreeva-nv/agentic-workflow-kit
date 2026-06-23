# Agentic Workflow Guide

Portable command guide for using methodology skill packs across projects. Keep this file project-agnostic; put project-specific rules in that project's own `AGENTS.md`.

## Files to Port

Copy these files into a new project or workspace root:

```text
AGENTS.md
CLAUDE.md
SKILL_CATALOG.md
.claude/AGENTIC_WORKFLOW.md
.claude/skills/*/SKILL.md
.codex/AGENTS.md
```

Optional project-specific additions:

```text
<project>/AGENTS.md
<project>/CLAUDE.md
<project>/.claude/skills/
<project>/.claude/agents/
```

Nearest project guidance should override this portable workflow.

## Bundled Local Skills

Run `/skills` in Claude Code after copying the repo into a project. Expected local skills:

- `agentic-lightweight-loop`
- `agentic-formal-feature`
- `agentic-role-review`
- `framework-contract-review`

For Codex, reference the skill path explicitly, for example:

```text
Use .claude/skills/agentic-formal-feature/SKILL.md and AGENTS.md for this task.
```

## Recommended Stack

Use these as layers, not as a mandatory sequence for every patch:

1. **Repo guidance**: `AGENTS.md`, nearest subsystem guidance, coding standards, and local tests.
2. **Lightweight spec spine**: GSD-style context, scope, plan, validation, and handoff for routine work.
3. **Formal feature discipline**: Superpowers or DAE-style brainstorm, ready contract, acceptance criteria, plan, TDD, review, finish.
4. **Review and ship layer**: gstack-style product, architecture, devex, QA, security, benchmark, and release reviews.
5. **Docs lookup**: Context7 or equivalent official-docs lookup for external APIs and fast-changing libraries.

## Default Prompts

### Lightweight Task

```text
Follow AGENTS.md. First inspect the touched subsystem and restate:
1. behavior change
2. non-goals
3. files likely to change
4. narrow validation plan

Then implement the smallest safe patch, run relevant tests, and review the diff for regressions.
```

### Formal Feature

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

### Role-Based Review

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

## DAE / ATDD for Claude Code

Install the Disciplined Agentic Engineering marketplace in Claude Code:

```text
/plugin marketplace add swingerman/disciplined-agentic-engineering
/plugin install engineer@disciplined-agentic-engineering
/plugin install atdd@disciplined-agentic-engineering
/plugin install crap-analyzer@disciplined-agentic-engineering
```

Local test option:

```bash
git clone https://github.com/swingerman/disciplined-agentic-engineering.git
claude --plugin-dir ./disciplined-agentic-engineering
```

DAE feature flow:

```text
/engineer.onboard          # one-time project charter, manifest, tracker, features/
/engineer.discuss          # brainstorm and decide drop / park / promote
/engineer.feature-init     # create Ready feature folder and branch
/engineer.prime-context    # load context for the Ready feature
/engineer.discover-acs     # acceptance criteria interview
/engineer.atdd             # bridge ACs into Gherkin and ATDD
/engineer.plan             # architecture plan and charter check
/atdd:atdd-team            # implement with acceptance + unit test streams
/engineer.refine           # reuse / quality / efficiency review
/engineer.arch-check       # charter architecture fitness
/atdd:mutate               # optional mutation hardening
/engineer.session-summary  # durable handoff
```

Use DAE for risky feature work, not routine typo fixes.

## gstack-Style Review Layer

If gstack is installed, use it around planning and before shipping:

```text
/office-hours              # product challenge and problem framing
/autoplan                  # initial patch plan
/plan-eng-review           # architecture review
/plan-devex-review         # developer experience review
/review                    # code review
/qa                        # QA pass
/cso                       # security review
/benchmark                 # performance check
/ship                      # release readiness
```

If commands are unavailable, ask Claude or Codex to perform the same named role review explicitly.

## Superpowers / GSD / Context Engineering

Use these as methodology shapes:

- **Superpowers**: brainstorm -> clarify spec -> write plan -> isolate worktree -> TDD -> subagent execution -> review -> finish branch.
- **GSD Core**: explicit phase control with context engineering, command routing, spec, implementation, verification, and handoff.
- **Context Engineering Kit**: spec-driven development, reflexion, and multi-agent code/PR review.

Practical default:

```text
Context -> Spec -> Plan -> Implement -> Verify -> Role Review -> Ship Handoff
```

Escalate only when the risk justifies the overhead.

## Codex + Claude Split

- Use **Claude Code** when you want installed slash commands, marketplace plugins, or Claude sub-agents.
- Use **Codex** when you want tight local implementation, test execution, diff review, or a second opinion on a Claude-produced plan.
- Use both by handing Claude's plan to Codex for implementation or handing Codex's diff to Claude/gstack for role review.
- Do not let either agent bypass project rules: nearest `AGENTS.md`, coding standards, DCO, API stability, and test requirements still apply.
