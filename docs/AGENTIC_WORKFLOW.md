# Agentic Workflow Guide

Portable command guide for using methodology skill packs across projects. Keep this file project-agnostic; put project-specific rules in that project's own `AGENTS.md`.

## Bundled Local Skills

Codex-native skills live in `.agents/skills/`. Claude Code compatibility copies live in `.claude/skills/`. Run `/skills` in Claude Code after copying the repo into a project. Expected local skills:

- `agentic-lightweight-loop`
- `agentic-formal-feature`
- `agentic-role-review`
- `framework-contract-review`

For Codex, reference the skill path explicitly, for example:

```text
Use .agents/skills/agentic-formal-feature/SKILL.md and AGENTS.md for this task.
```

## Recommended Stack

Use these as layers, not as a mandatory sequence for every patch:

1. **Repo guidance**: `AGENTS.md`, nearest subsystem guidance, coding standards, and local tests.
2. **Lightweight spec spine**: GSD-style context, scope, plan, validation, and handoff for routine work.
3. **Formal feature discipline**: Superpowers or DAE-style brainstorm, ready contract, acceptance criteria, plan, TDD, review, finish.
4. **Review and ship layer**: gstack-style product, architecture, devex, QA, security, benchmark, and release reviews.
5. **Docs lookup**: Context7 or equivalent official-docs lookup for external APIs and fast-changing libraries.

## Recommended Flow: Generic Two-Agent Development Loop

Use this loop for framework, library, or infrastructure work where design quality, compatibility, testing, and release readiness matter. It is role-based, not tool-specific: Agent 1 leads design, challenge, reviews, and decisions; Agent 2 scans the repo, implements, tests, and returns validation evidence.

Default Claude + Codex mapping: Agent 1 = Claude Code, Agent 2 = Codex. You can swap the actual tools as long as the roles stay clear.

Phases: **Discover -> Specify -> Plan -> Build -> Review -> Validate -> Ship -> Reflect**

![Two-Agent Framework Development Loop](../assets/two-agent-framework-loop.svg)

Legend:

- Agent 1 = interactive design, challenge, review, and decision surface.
- Agent 2 = repo-grounded execution, tests, validation, and evidence surface.
- External tools are optional. If unavailable, use the bundled local fallback skills.

### Stage And Skill Matrix

| Stage | Generic Goal | Agent 1 Role | Agent 2 Role | Skills / Tools To Use |
|---|---|---|---|---|
| 1. Discover / Scope | Frame the problem, outcome, non-goals, risk, and user value | Lead brainstorming and product challenge | Inspect repo context if needed | [agentic-lightweight-loop](../.agents/skills/agentic-lightweight-loop/SKILL.md); [Superpowers](SUPERPOWERS_README.md) brainstorming; [GSD Core](GSD_CORE_README.md) context setup; [gstack](GSTACK_README.md) `/office-hours`; [Ponytail](PONYTAIL_README.md) only if installed |
| 2. Repo Context | Map touched files, tests, commands, conventions, and constraints | Ask for gaps or constraints that matter | Scan source, tests, docs, and nearest guidance | [agentic-lightweight-loop](../.agents/skills/agentic-lightweight-loop/SKILL.md); [AGENTS.md](../AGENTS.md); [repo guidance docs](AGENTS_CLAUDE_README.md); [Context7/docs lookup](DOCS_LOOKUP_README.md) when external APIs are involved |
| 3. Contract / Spec | Define Ready contract, acceptance criteria, API expectations, and non-goals | Own product/API decisions and acceptance criteria | Validate whether the contract fits current code | [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md); [DAE/ATDD](DAE_README.md); [GSD Core](GSD_CORE_README.md); [framework-specific custom skills](FRAMEWORK_SKILLS_README.md); [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md) for public APIs |
| 4. Spec Validation | Check the spec against architecture, tests, migration paths, and known constraints | Decide whether to revise scope or proceed | Report blockers, missing tests, and feasibility gaps | [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md); [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md); [docs lookup](DOCS_LOOKUP_README.md); [code/security review tooling](CODE_SECURITY_REVIEW_README.md) when risk appears early |
| 5. Plan | Produce an implementation sequence, test matrix, rollback/migration story, and validation plan | Challenge architecture, devex, compatibility, and risk | Translate the plan into files, tests, and execution steps | [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md); [Superpowers](SUPERPOWERS_README.md) write-plans; [gstack](GSTACK_README.md) `/autoplan`, `/plan-eng-review`, `/plan-devex-review`; [agentic-role-review](../.agents/skills/agentic-role-review/SKILL.md) |
| 6. Build | Implement incrementally while preserving the approved contract | Stay available for checkpoint decisions | Edit code, add/update tests, and keep diffs narrow | [agentic-lightweight-loop](../.agents/skills/agentic-lightweight-loop/SKILL.md) for small work; [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md) for risky work; [framework-specific custom skills](FRAMEWORK_SKILLS_README.md); [docs lookup](DOCS_LOOKUP_README.md) for external APIs |
| 7. Checkpoint Review | Review partial diff before the change becomes large | Review scope, design, API shape, and risk | Summarize diff, test status, blockers, and next patch | [agentic-role-review](../.agents/skills/agentic-role-review/SKILL.md); [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md); [gstack](GSTACK_README.md) `/review`; [code/security review tooling](CODE_SECURITY_REVIEW_README.md) for Codex `/review` usage |
| 8. Fix / Continue | Resolve checkpoint findings and continue implementation | Decide tradeoffs when findings conflict | Fix findings and rerun targeted validation | [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md); [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md); [code/security review tooling](CODE_SECURITY_REVIEW_README.md) for risky fixes |
| 9. Adversarial Review | Challenge the finished diff across product, architecture, devex, API, lifecycle, security, performance, tests, docs, and release risk | Lead adversarial review and acceptance decision | Provide diff, evidence, and suspected weak spots | [agentic-role-review](../.agents/skills/agentic-role-review/SKILL.md); [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md); [gstack](GSTACK_README.md) `/qa`, `/cso`, `/benchmark`; [code/security review tooling](CODE_SECURITY_REVIEW_README.md) |
| 10. Final Validation | Run final tests, scans, benchmarks, docs checks, and compatibility checks appropriate to risk | Decide whether validation is enough to ship | Run commands and produce evidence with failures called out | [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md); [agentic-role-review](../.agents/skills/agentic-role-review/SKILL.md); [DAE/ATDD](DAE_README.md) mutation step if available; [framework-specific custom skills](FRAMEWORK_SKILLS_README.md) for docs-as-tests; [code/security review tooling](CODE_SECURITY_REVIEW_README.md) for scanners |
| 11. Ship Readiness | Prepare release notes, migration notes, PR summary, residual-risk callout, and deploy/merge decision | Own ship/no-ship decision | Produce final patch summary and validation evidence | [agentic-role-review](../.agents/skills/agentic-role-review/SKILL.md); [gstack](GSTACK_README.md) `/ship`, `/land-and-deploy`; [Superpowers](SUPERPOWERS_README.md) finish branch; [DAE/ATDD](DAE_README.md) session summary |
| 12. Reflect / Learn | Capture reusable lessons in guidance, docs, or skills | Decide what should become durable guidance | Update `AGENTS.md`, docs, or skills only when reusable | [repo guidance docs](AGENTS_CLAUDE_README.md); [framework-specific custom skills](FRAMEWORK_SKILLS_README.md); [skill-creator](FRAMEWORK_SKILLS_README.md) guidance if creating a new Codex skill |

### Skill Selection Rules

- Use [agentic-lightweight-loop](../.agents/skills/agentic-lightweight-loop/SKILL.md) when the task is routine and the risk is local.
- Use [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md) when the task needs a contract, acceptance criteria, TDD, or a reviewable plan.
- Use [agentic-role-review](../.agents/skills/agentic-role-review/SKILL.md) when you need [gstack-style](GSTACK_README.md) product, architecture, devex, QA, security, performance, docs, and release lenses.
- Use [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md) when public API, compatibility, lifecycle/concurrency, performance, docs, test matrix, or release risk matters.
- Use [DAE/ATDD](DAE_README.md) for high-risk features that justify checkpoint artifacts and acceptance-test discipline.
- Use [Context7 or equivalent docs lookup](DOCS_LOOKUP_README.md) when external APIs, SDKs, or fast-changing behavior are involved.
- Use [framework-specific custom skills](FRAMEWORK_SKILLS_README.md) when a project has durable framework rules beyond the generic skills.

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

## DAE / ATDD

DAE/ATDD has its own dedicated guide in `DAE_README.md`. Use that file for upstream Claude Code plugin installation, the Claude-only command boundary, Codex handoff prompts, and Codex-native porting options.

Short rule: run upstream `/engineer.*` and `/atdd:*` commands in Claude Code; use Codex to validate repo fit, implement approved DAE plans, run tests, and report evidence.

## gstack-Style Review Layer

gstack is optional and external to this kit. Install it from your team or vendor source in the agent surface that supports its slash commands, usually Claude Code. This kit provides the local fallback skill `agentic-role-review` for the same review shape.

Use real gstack commands when available:

```text
/office-hours              # product challenge and problem framing
/autoplan                  # initial patch plan
/plan-eng-review           # architecture review
/plan-devex-review         # developer experience review
/review                    # code review
/devex-review              # developer experience review
/qa                        # QA pass
/qa-only                   # QA-only pass
/cso                       # security review
/benchmark                 # performance check
/ship                      # release readiness
/land-and-deploy           # final ship/deploy flow
```

Use this sequence with the bundled skills:

1. Draft scope with `agentic-lightweight-loop` or `agentic-formal-feature`.
2. Run gstack plan challenge commands if installed.
3. Implement the patch with Codex or Claude.
4. Run gstack review/QA/security/benchmark/ship commands if installed.
5. If gstack is unavailable, invoke `agentic-role-review` and ask for the same lenses explicitly.

Fallback invocation examples:

```text
Use .agents/skills/agentic-role-review/SKILL.md and AGENTS.md. Run a gstack-style review of this plan/diff across product, architecture, devex, API compatibility, lifecycle/concurrency, performance, security, QA, docs, test matrix, and release readiness. Findings first.
```

```text
Use the agentic-role-review skill for a gstack-style pre-ship review.
```

```text
Use .claude/skills/agentic-role-review/SKILL.md. Run the same gstack-style review lenses. Findings first.
```

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

## Example Claude + Codex Split

- Use **Claude Code** when you want installed slash commands, marketplace plugins, or Claude sub-agents.
- Use **Codex** when you want tight local implementation, test execution, diff review, or a second opinion on a Claude-produced plan.
- Use both by handing Claude's plan to Codex for implementation or handing Codex's diff to Claude/gstack for role review.
- Do not let either agent bypass project rules: nearest `AGENTS.md`, coding standards, DCO, API stability, and test requirements still apply.
