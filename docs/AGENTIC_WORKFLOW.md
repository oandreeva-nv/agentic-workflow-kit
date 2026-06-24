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

### Stage And Complexity Matrix

Select the stage first, then choose the lowest complexity band that fits the actual risk. The columns are additive: a framework release usually uses the routine repo scan, the formal spec workflow, and the framework/release checks.

| Stage | Routine / local work | Feature / spec work | Framework / release work | External product layer |
| --- | --- | --- | --- | --- |
| Discover / scope | Read [AGENTS.md](../AGENTS.md), nearest repo guidance, and use [agentic-lightweight-loop](../.agents/skills/agentic-lightweight-loop/SKILL.md) to restate the change and validation target. | Use [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md), [GSD Core](GSD_CORE_README.md), or [Superpowers](SUPERPOWERS_README.md) to clarify outcome, non-goals, constraints, and approval points. | Add [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md) early if public API, compatibility, lifecycle, performance, docs, or release semantics might change. | Use [gstack](GSTACK_README.md) `/office-hours` for product challenge. Use [Ponytail](PONYTAIL_README.md) when the main risk is overbuilding. |
| Repo context | Use [agentic-lightweight-loop](../.agents/skills/agentic-lightweight-loop/SKILL.md) to map touched files, tests, commands, conventions, and local constraints. | Use [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md) to check whether the proposed contract fits current architecture and test coverage. | Add framework-specific custom skills from [FRAMEWORK_SKILLS_README.md](FRAMEWORK_SKILLS_README.md) when the repo has durable framework rules. | Use [Context7 or docs lookup](DOCS_LOOKUP_README.md) before relying on memory for external APIs, SDKs, CLIs, or package behavior. |
| Contract / spec | Keep the contract lightweight: behavior change, non-goals, validation, and rollback if needed. | Produce a Ready contract, acceptance criteria, architecture options, and test matrix with [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md). | Run [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md) against the spec before implementation if downstream users depend on the behavior. | Use [DAE/ATDD](DAE_README.md) for signed charter, Gherkin/ATDD, architecture checkpoints, and mutation or hardening discipline. Use Context Engineering Kit if your team has it installed. |
| Plan | Use a short patch checklist and the smallest meaningful validation command. | Write an ordered implementation plan with test-first or test-near steps. Use [Superpowers](SUPERPOWERS_README.md) planning or [GSD Core](GSD_CORE_README.md) phase control if installed. | Include migration, compatibility, docs-as-tests, test matrix, release notes, and rollback or deprecation strategy. | Use [gstack](GSTACK_README.md) `/autoplan`, `/plan-eng-review`, `/plan-devex-review`, or `/plan-design-review` when available. |
| Build | Use [agentic-lightweight-loop](../.agents/skills/agentic-lightweight-loop/SKILL.md): narrow diff, local tests, no broad refactor. | Use [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md): implement against the approved contract and keep validation evidence current. | Use framework-specific custom skills and keep compatibility, lifecycle/concurrency, performance, docs, and release notes in the diff as needed. | Use [Ponytail](PONYTAIL_README.md) to challenge unnecessary code, dependencies, or complexity. Use Superpowers execution/TDD commands if installed. |
| Review | Self-review the diff against the requested behavior and tests. | Use [agentic-role-review](../.agents/skills/agentic-role-review/SKILL.md) for product, architecture, devex, QA, security, performance, docs, and release lenses. | Use [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md) for API contract, compatibility, lifecycle/concurrency, error model, docs, test matrix, and release risk. | Use [gstack](GSTACK_README.md) `/review`, `/devex-review`, `/qa`, `/cso`, `/benchmark`; use [code/security review tooling](CODE_SECURITY_REVIEW_README.md) and real scanners when installed. |
| Validate | Run the smallest relevant tests and report what did not run. | Run acceptance/integration tests plus unit tests that prove the contract. | Run compatibility, migration, docs, matrix, performance, and security validation proportionate to release risk. | Use [DAE/ATDD](DAE_README.md) mutation or hardening steps, gstack `/qa` and `/benchmark`, and scanner output only when those tools actually ran. |
| Ship / reflect | Summarize files changed, tests run, and residual risk. | Produce PR or handoff notes with contract, validation evidence, and open decisions. | Add release notes, migration notes, deprecation notes, and reusable guidance updates. | Use gstack `/ship`, `/land-and-deploy`, `/document-release`, `/retro`; use Superpowers branch finishing; update [AGENTS/CLAUDE guidance](AGENTS_CLAUDE_README.md) or custom skills only when the lesson should persist. |

### Situation Playbooks

Use these playbooks as the primary selection rule. Pick the row that best matches the task, then apply the stage matrix above only for the stages you actually need.

| Situation | Recommended sequence | Do not add |
| --- | --- | --- |
| Tiny docs edit, typo, formatting-only change | [AGENTS.md](../AGENTS.md) -> direct edit -> quick diff check. | DAE, full formal spec, role review, or external product commands. |
| Small local bug or local refactor | [AGENTS.md](../AGENTS.md) -> [agentic-lightweight-loop](../.agents/skills/agentic-lightweight-loop/SKILL.md) -> focused tests -> concise handoff. | Framework/release review unless repo scan reveals public contract, migration, security, or performance risk. |
| New application feature | [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md) for Ready contract, acceptance criteria, plan, and implementation -> [agentic-role-review](../.agents/skills/agentic-role-review/SKILL.md) before handoff. | DAE unless the feature needs signed checkpoints or ATDD artifacts. |
| Framework, SDK, plugin, public API, or library change | [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md) -> [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md) before coding if the contract is unclear -> implementation -> [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md) plus [agentic-role-review](../.agents/skills/agentic-role-review/SKILL.md). | Treating the work as a normal app feature just because the patch is small. |
| External API, SDK, cloud, package, CLI, or migration-sensitive change | [Context7/docs lookup](DOCS_LOOKUP_README.md) or official docs -> choose [agentic-lightweight-loop](../.agents/skills/agentic-lightweight-loop/SKILL.md) for local fixes or [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md) for feature/migration work -> validation. | Memory-only implementation of fast-changing behavior. |
| High-risk feature needing ATDD discipline | [DAE/ATDD](DAE_README.md) in Claude Code for charter, Ready artifacts, Gherkin/ATDD, and architecture plan -> Codex implementation using [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md) -> role/framework review -> validation evidence. | Claiming DAE ran in Codex unless a Codex-native port exists and was actually invoked. |
| Security-sensitive change | [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md) -> threat and abuse cases in acceptance criteria -> implementation -> [agentic-role-review](../.agents/skills/agentic-role-review/SKILL.md) plus [code/security review tooling](CODE_SECURITY_REVIEW_README.md). | A security signoff without scanner/tool evidence or an explicit fallback review label. |
| Performance-sensitive change | [agentic-formal-feature](../.agents/skills/agentic-formal-feature/SKILL.md) -> define baseline and budget -> implementation -> benchmark or targeted performance test -> [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md) if shared hot paths are affected. | Performance claims without measurement or a clear reason measurement was not practical. |
| Overbuilding or dependency-risk concern | [Ponytail](PONYTAIL_README.md) if installed, or ask the agent to challenge whether the code can be deleted, reused, simplified, or handled by an existing dependency -> then choose lightweight or formal flow. | Skipping validation, security, accessibility, or data-loss handling in the name of minimalism. |
| Release readiness / pre-merge review | [agentic-role-review](../.agents/skills/agentic-role-review/SKILL.md) or [gstack](GSTACK_README.md) `/ship` -> [framework-contract-review](../.agents/skills/framework-contract-review/SKILL.md) for framework releases -> final validation evidence and residual risk. | Shipping notes that hide failed, skipped, or unavailable validation. |
| Recurring project rule that should travel across repos | Capture it in [AGENTS.md](../AGENTS.md) if it is repo policy; create a framework-specific skill using [FRAMEWORK_SKILLS_README.md](FRAMEWORK_SKILLS_README.md) if it is a reusable workflow. | A new custom skill for a one-off preference. |

### Prompt Library

These prompts are meant to be copied into Codex, Claude Code, or another coding agent. Replace bracketed placeholders before use.

#### Routine Local Change

```text
Use .agents/skills/agentic-lightweight-loop/SKILL.md and AGENTS.md.
Task: [one-sentence task]
Treat this as routine/local unless repo scan shows public API, migration, security, performance, or release risk.

Before editing, report:
1. behavior change
2. non-goals
3. likely files/tests
4. validation command

Then make the smallest patch, run focused validation, inspect the diff, and report files changed, commands run, failures or skipped checks, and residual risk.
```

#### Formal Feature

```text
Use .agents/skills/agentic-formal-feature/SKILL.md and AGENTS.md.
Task: [feature or behavior]
Do not implement until the Ready contract and implementation plan are accepted.

Produce:
1. problem and non-goals
2. Ready contract
3. acceptance criteria in domain language
4. Gherkin scenarios only where they clarify executable behavior
5. architecture plan with tradeoffs
6. test matrix and validation commands
7. review gates before handoff
```

#### Framework Or Public API Change

```text
Use .agents/skills/framework-contract-review/SKILL.md and AGENTS.md.
Task or diff: [link, branch, patch, or summary]
Treat this as framework/API work even if the patch is small.

Find blockers first across:
- public API and compatibility
- migration and deprecation path
- error model and developer experience
- lifecycle, concurrency, cancellation, cleanup
- performance and resource use
- security and extension-point abuse
- docs-as-tests and examples
- supported version/platform/backend matrix
- release notes and ship readiness

For each finding, give severity, evidence, and concrete remediation.
```

#### gstack-Style Review Without gstack

```text
Use .agents/skills/agentic-role-review/SKILL.md and AGENTS.md.
Review this plan or diff using the same shape as gstack /review, /qa, /cso, /benchmark, and /ship.

Cover product, architecture, devex, API compatibility, lifecycle/concurrency, performance, security, QA, docs, test matrix, and release readiness.
Findings first. Order by severity. Include file and line references when reviewing code. Separate open questions from confirmed findings.
```

#### Real gstack Commands

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

Use these only in an agent surface where gstack is actually installed. Otherwise use the fallback review prompt above and label it as a fallback.

#### DAE / ATDD Handoff To Codex

```text
Use AGENTS.md and .agents/skills/agentic-formal-feature/SKILL.md.
Implement the approved DAE/ATDD feature from [artifact path].

Respect the DAE charter, Ready contract, acceptance criteria, Gherkin/ATDD scenarios, architecture plan, and test matrix. Do not change the accepted contract without calling it out.

During implementation, keep two test streams visible:
1. acceptance/integration tests that prove user-visible behavior
2. unit/component tests that prove design and edge cases

At handoff, report the DAE artifacts used, files changed, validation commands, failures or skipped checks, and remaining review risks.
```

#### Docs Lookup Before Coding

```text
Use Context7 or equivalent official-docs lookup before implementation.
Topic: [library/API/SDK/CLI]
Question: [specific behavior/version/configuration]

Return the documented facts, version assumptions, source links if available, and the implementation consequences. Then choose agentic-lightweight-loop for a local patch or agentic-formal-feature for feature/migration work.
```

#### Ponytail / Minimalism Pass

```text
Use Ponytail if installed; otherwise run a Ponytail-style minimalism pass.
Before adding code, check whether the change can be skipped, deleted, reused from existing code, handled by stdlib/native platform behavior, or implemented with a smaller existing dependency.

Do not reduce validation, security, accessibility, compatibility, or data-loss handling. Report what was simplified and what must remain.
```

#### Release Handoff

```text
Use .agents/skills/agentic-role-review/SKILL.md and AGENTS.md for release readiness.
If this is framework/library work, also use .agents/skills/framework-contract-review/SKILL.md.

Produce:
1. ship/no-ship recommendation
2. user-visible change summary
3. compatibility and migration notes
4. tests, scans, docs checks, benchmarks, and CI evidence
5. failed, skipped, or unavailable validation
6. residual risks and owner decisions needed
7. AGENTS.md, docs, or skill updates that should persist
```

### Tool Coverage And Fallbacks

This workflow mentions both local skills and external products. External products must be installed separately; local skills are the portable fallback.

| Layer | Actual tool or file | Install/use guide | Local fallback |
| --- | --- | --- | --- |
| Repo guidance | `AGENTS.md`, `CLAUDE.md`, `.codex/AGENTS.md` | [Repo guidance docs](AGENTS_CLAUDE_README.md) | Always read nearest repo guidance first. |
| Routine loop | `agentic-lightweight-loop` | [.agents skill](../.agents/skills/agentic-lightweight-loop/SKILL.md) | Built into this repo. |
| Formal feature loop | `agentic-formal-feature` | [.agents skill](../.agents/skills/agentic-formal-feature/SKILL.md) | Built into this repo; also substitutes for unavailable GSD/Superpowers/DAE planning. |
| Role review | `agentic-role-review` | [.agents skill](../.agents/skills/agentic-role-review/SKILL.md) | Built into this repo; fallback for unavailable gstack review commands. |
| Framework contract review | `framework-contract-review` | [.agents skill](../.agents/skills/framework-contract-review/SKILL.md) | Built into this repo; extend with [framework-specific custom skills](FRAMEWORK_SKILLS_README.md). |
| Superpowers | Claude Code plugin family | [Superpowers guide](SUPERPOWERS_README.md) | Use `agentic-formal-feature` for planning/TDD and `agentic-role-review` for review. |
| GSD Core | Open GSD runtime | [GSD Core guide](GSD_CORE_README.md) | Use `agentic-formal-feature` with explicit phase outputs. |
| DAE / ATDD | Claude Code plugin set | [DAE guide](DAE_README.md) | Use `agentic-formal-feature` with DAE-style artifacts; do not claim upstream DAE commands ran. |
| gstack | Review, QA, security, benchmark, ship slash commands | [gstack guide](GSTACK_README.md) | Use `agentic-role-review`; add `framework-contract-review` for framework releases. |
| Context7 / docs lookup | CLI, MCP, or equivalent official-docs lookup | [Docs lookup guide](DOCS_LOOKUP_README.md) | Use official docs or repo/vendor docs manually and cite what you used. |
| Ponytail | Minimalism and review plugin | [Ponytail guide](PONYTAIL_README.md) | Run the Ponytail-style minimalism prompt above. |
| Code/security review tooling | Codex review/security surfaces, scanners, gstack CSO | [Code/security review guide](CODE_SECURITY_REVIEW_README.md) | Use `agentic-role-review` and label scanner/tool gaps explicitly. |
| Context Engineering Kit | Team-installed spec/context/review pack, if available | Team-specific install docs | Use `agentic-formal-feature` plus `agentic-role-review`. |

### Evidence Rules

- Say which tool or skill actually ran: local skill, installed external command, scanner, CI job, or manual fallback prompt.
- Do not claim gstack, DAE, Context7, Ponytail, scanners, benchmarks, or CI ran unless they did.
- Escalate from lightweight to formal workflow when repo scan reveals public API, migration, security, concurrency, performance, or release risk.
- Create or update framework-specific custom skills only for durable cross-repo rules, not one-off preferences.

## Example Claude + Codex Split

- Use **Claude Code** when you want installed slash commands, marketplace plugins, or Claude sub-agents.
- Use **Codex** when you want tight local implementation, test execution, diff review, or a second opinion on a Claude-produced plan.
- Use both by handing Claude's plan to Codex for implementation or handing Codex's diff to Claude/gstack for role review.
- Do not let either agent bypass project rules: nearest `AGENTS.md`, coding standards, DCO, API stability, and test requirements still apply.
