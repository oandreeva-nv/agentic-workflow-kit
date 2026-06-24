# DAE / ATDD With Claude Code And Codex

This file is the canonical DAE-specific guide for this kit. Keep general workflow guidance in `.claude/AGENTIC_WORKFLOW.md`; keep DAE install notes, Codex boundaries, and DAE handoff prompts here.

External project: https://github.com/swingerman/disciplined-agentic-engineering

## What DAE Is

Disciplined Agentic Engineering (DAE) is a Claude Code methodology marketplace focused on spec-driven and test-driven AI coding. The upstream repo currently packages three Claude Code plugins:

| Plugin | Purpose |
|---|---|
| `engineer` | DAE methodology kit: charter, feature intake, AC discovery, planning, refinement, verification, hardening |
| `atdd` | Acceptance Test Driven Development flow with Gherkin, acceptance/unit test streams, and mutation hardening |
| `crap-analyzer` | Change Risk Anti-Pattern analysis for changed code |

DAE's feature flow is checkpoint-based:

```text
0 Onboard -> 1.5 Ready -> 2 ACs -> 3 Spec -> 4 Plan -> 5 Implement -> 6 Refine -> 7 Light Verify -> 8 Hardening
```

Use DAE when the work is risky enough to justify explicit contracts: public APIs, framework behavior, migrations, security boundaries, concurrency/lifecycle behavior, performance-sensitive paths, or release-critical changes.

## Key Boundary

DAE's upstream slash commands are Claude Code plugin commands. They do not run directly inside Codex.

Claude Code commands such as these are Claude-only unless someone ports them into a Codex plugin:

```text
/engineer.onboard
/engineer.discuss
/engineer.feature-init
/engineer.discover-acs
/engineer.atdd
/engineer.plan
/atdd:atdd-team
/engineer.refine
/engineer.arch-check
/atdd:mutate
/engineer.session-summary
```

Codex can still use the DAE methodology by reading DAE artifacts, following repo skills, running tests, and executing deterministic guardrail scripts when those scripts are present and allowed. For Codex-native reuse, encode the workflow as `.agents/skills/.../SKILL.md` or package it as a Codex plugin.

## Recommended Hybrid Flow

Use Claude Code for DAE orchestration and Codex for repo-grounded implementation and validation.

1. In Claude Code, install DAE plugins.
2. In Claude Code, run DAE through spec and plan checkpoints.
3. Commit or keep the DAE artifacts in the repo, usually under a feature folder such as `features/<id>/`.
4. In Codex, implement from the approved artifacts.
5. In Codex, run tests and collect validation evidence.
6. In Claude Code, run DAE review, arch-check, mutation, and session-summary steps when you want the upstream plugin workflow.

### Claude Code Install

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

### Claude Code DAE Sequence

```text
/engineer.onboard          # one-time project charter, manifest, tracker, features/
/engineer.discuss          # brainstorm and decide drop / park / promote
/engineer.feature-init     # create Ready feature folder and branch
/engineer.prime-context    # load context for the Ready feature
/engineer.discover-acs     # acceptance criteria interview
/engineer.atdd             # bridge ACs into Gherkin and ATDD
/engineer.plan             # architecture plan and charter check
```

After `/engineer.plan`, hand the generated artifacts to Codex.

## Codex Handoff Prompts

### Implement An Approved DAE Plan

```text
Use AGENTS.md and .agents/skills/agentic-formal-feature/SKILL.md.
Implement the approved DAE feature in features/<id>/plan.md.
Read feature.md, acs.md, spec.md, and plan.md first.
Preserve the Ready contract and acceptance criteria.
Use acceptance/integration tests plus unit tests where the repo supports them.
Run the relevant validation commands and report evidence.
Do not claim mutation testing unless you actually run the mutation command.
```

### Validate A DAE Spec Before Implementation

```text
Use AGENTS.md and .agents/skills/agentic-formal-feature/SKILL.md.
Validate this DAE feature folder against the current repo before implementation.
Check whether feature.md, acs.md, spec.md, and plan.md are consistent with existing architecture, public APIs, tests, and project constraints.
Return blockers, gaps, and a narrow validation plan. Do not edit code yet.
```

### Fix Findings After DAE Or gstack Review

```text
Use AGENTS.md, .agents/skills/agentic-formal-feature/SKILL.md, and .agents/skills/framework-contract-review/SKILL.md.
Fix the review findings for features/<id> while preserving the approved DAE contract.
Run the smallest relevant validation first, then expand if public API, compatibility, security, lifecycle, or performance behavior changed.
```

### Codex-Only DAE-Style Planning

Use this when Claude Code is unavailable or you do not need the upstream plugin commands:

```text
Use AGENTS.md and .agents/skills/agentic-formal-feature/SKILL.md.
Run this as a DAE/ATDD-style feature.
First produce:
1. Ready contract
2. acceptance criteria in domain language
3. Gherkin scenarios if they add executable clarity
4. architecture plan with explicit charter/constraint check
5. acceptance plus unit test matrix
6. validation and mutation-testing plan
Stop before implementation for approval.
```

After approval:

```text
Continue with the approved DAE/ATDD plan.
Implement incrementally with acceptance/integration tests plus unit tests.
Run validation.
If mutation testing is unavailable, identify the missing command or tool instead of faking mutation results.
```

## Codex-Native Porting Options

| Option | Use When | Shape |
|---|---|---|
| Repo skill | You want DAE-style behavior inside one project | `.agents/skills/dae-atdd-feature/SKILL.md` |
| User skill | You want your personal DAE-style workflow across projects | `~/.agents/skills/dae-atdd-feature/SKILL.md` |
| Codex plugin | You want reusable distribution to other developers | `.codex-plugin/plugin.json` plus bundled skills/resources/scripts |
| Hybrid Claude + Codex | You want the real upstream DAE slash commands plus Codex implementation | Claude Code plugins + Codex handoff prompts |

Do not copy Claude Code slash commands into Codex docs as if they were Codex commands. In Codex, invoke skills with `/skills`, `$skill-name`, or an explicit path prompt.

## Artifact Expectations

A DAE feature folder should make the implementation contract durable. The exact upstream layout may evolve, but this kit expects these concepts:

| Artifact | Purpose |
|---|---|
| `feature.md` | Ready contract: outcome, scope, non-goals, owner, branch, success criteria |
| `acs.md` | Acceptance criteria in domain language, including edge cases and failure modes |
| `spec.md` | Gherkin behavior spec when useful |
| `plan.md` | Architecture plan, touched modules, test strategy, charter/constraint check |
| `handoffs/` or session notes | Checkpoint completion evidence and pickup context |

Codex should treat these artifacts as requirements, not suggestions, unless the user explicitly changes the contract.

## Guardrail Rules

- Do not bypass the nearest `AGENTS.md`, project coding standards, or test requirements.
- Do not invent DAE artifacts if the upstream plugin did not create them; clearly label any Codex-created equivalent.
- Do not claim a checkpoint is complete without evidence.
- Do not claim mutation testing, arch-checks, CRAP analysis, or security scans unless the corresponding command actually ran.
- If a DAE artifact conflicts with the repo, stop and report the conflict before implementation.
- Keep DAE for high-risk features; use the lightweight loop for routine edits.

## Quick Decision

| Need | Recommended Surface |
|---|---|
| Use upstream `/engineer.*` or `/atdd:*` commands | Claude Code |
| Implement an approved DAE plan | Codex |
| Validate repo fit before implementation | Codex |
| Run the same DAE discipline without Claude plugins | Codex with `agentic-formal-feature` |
| Package DAE-style flow for teams using Codex | Codex plugin |
