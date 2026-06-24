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

## Recommended Flow: Two-Agent Framework Development Loop

Use this loop for framework or library work where design quality, compatibility, testing, and release readiness matter. It is role-based: Agent 1 leads design, challenge, reviews, and decisions; Agent 2 scans the repo, implements, tests, and returns validation evidence.

Default Claude + Codex mapping: Agent 1 = Claude Code, Agent 2 = Codex. You can swap the actual tools as long as the roles stay clear.

Phases: **Design -> Review -> Implement -> Validate -> Ship -> Reflect**

![Two-Agent Framework Development Loop](../assets/two-agent-framework-loop.svg)

Text flow summary:

1. **[Agent 1]** Superpowers brainstorming -> generate `/idea-hours`.
2. **[Agent 2]** Repo/project scan.
3. **[Agent 1]** DAE / framework spec.
4. **[Agent 2]** Validate spec against repo.
5. **[Agent 1]** gstack `/plan-eng-review` and `/plan-devex-review`.
6. **[Agent 1]** Superpowers write-plans.
7. **[Agent 2]** Translate plan to test status.
8. **[Agent 2]** TDD implementation step by step.
9. **[Agent 1]** Review diff / checkpoint.
10. **[Agent 2]** Continue implementation.
11. **[Agent 1]** Adversarial framework review.
12. **[Agent 2]** Fix review findings and run validation.
13. **[Agent 1]** Compatibility / performance / security / docs review.
14. **[Agent 2]** Final patch summary and validation evidence.
15. **[Agent 1]** gstack `/ship` or Superpowers finish branch.
16. **[Agent 2]** Reflect and update `AGENTS.md` / skills.

Legend:

- Left column = Agent 1: interactive design, challenge, reviews, and decisions.
- Right column = Agent 2: repo-grounded execution, tests, validation, and patch evidence.
- Arrows = handoffs between the two agents.

Tool mapping:

| Flow Step | Preferred Tooling | Bundled Fallback |
|---|---|---|
| 1-2 Discover / Scope | Superpowers brainstorming, `/idea-hours`, Agent 2 repo scan | `agentic-lightweight-loop` |
| 3-4 Spec / Validate | DAE / framework spec, Agent 2 spec validation | `agentic-formal-feature` |
| 5-6 Plan Review | gstack `/plan-eng-review`, `/plan-devex-review`, Superpowers write-plans | `agentic-formal-feature` plus `agentic-role-review` |
| 7-10 Implement / Checkpoint | Agent 2 TDD execution, Agent 1 checkpoint review | `agentic-lightweight-loop` or `agentic-formal-feature` |
| 11-12 Adversarial Review | Agent 1 adversarial framework review, Agent 2 fixes | `framework-contract-review` plus `agentic-role-review` |
| 13-14 Final Validation | compatibility/perf/security/docs review, Agent 2 evidence | `framework-contract-review` |
| 15-16 Ship / Learn | gstack `/ship`, Superpowers finish branch, Agent 2 reflection | `agentic-role-review`; update `AGENTS.md` / skills when reusable lessons emerge |

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

DAE/ATDD has its own dedicated guide in `../docs/DAE_README.md`. Use that file for upstream Claude Code plugin installation, the Claude-only command boundary, Codex handoff prompts, and Codex-native porting options.

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
