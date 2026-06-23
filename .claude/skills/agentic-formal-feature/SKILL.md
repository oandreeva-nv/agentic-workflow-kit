---
name: agentic-formal-feature
tags: [workflow, spec, gsd, superpowers, dae, atdd]
description: >
  Use for risky or feature-level work that needs explicit spec discipline:
  charter, ready contract, acceptance criteria, architecture plan, dual test
  streams, role review, and optional mutation/fault-injection hardening.
license: Unlicense
---

# Agentic Formal Feature

Use this skill when a change affects public APIs, developer-facing behavior, security boundaries, concurrency, scheduling, memory ownership, performance-critical paths, migrations, or release compatibility.

This is the local fallback for GSD / Superpowers / DAE-style workflows. If DAE is installed in Claude Code, prefer the DAE commands listed below for the formal phases.

## Phase Gate

Do not implement until the Ready contract and architecture plan are accepted, unless the user explicitly asks to proceed without approval.

## Artifacts

1. **Charter / constraints**
   - Architecture boundaries
   - Compatibility rules
   - Performance budget
   - Security posture
   - Autonomy level
   - Test expectations

2. **Ready contract**
   - Outcome
   - User value
   - Scope
   - Non-goals
   - Owner / branch
   - Success criteria

3. **Acceptance criteria**
   - Domain-language happy path
   - Edge cases
   - Error behavior
   - Security and abuse cases
   - Compatibility and migration behavior
   - Performance expectations

4. **Gherkin when useful**
   - `Feature`
   - `Scenario`
   - `Given`
   - `When`
   - `Then`
   - Avoid implementation details.

5. **Architecture plan**
   - Touched modules
   - Public API changes
   - Data/lifecycle model
   - Test matrix
   - Rollback or migration story
   - Explicit charter check

6. **Implementation**
   - Acceptance or integration tests for behavior
   - Unit tests for internal structure
   - Incremental commits or patch steps

7. **Hardening**
   - Role-based review
   - Security review
   - Performance regression check
   - Mutation testing, property tests, or fault injection when practical

## DAE Command Mapping

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

## Prompt

```text
Use the agentic-formal-feature skill. Draft the Ready contract, acceptance criteria, and architecture plan first. Do not implement until I approve the plan. After implementation, run the role review and report verification plus residual risk.
```
