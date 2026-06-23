# AGENTS.md

Portable agentic development workflow for projects in this workspace.

This file is intentionally project-agnostic. Copy it, `CLAUDE.md`, `.claude/AGENTIC_WORKFLOW.md`, and `.codex/AGENTS.md` into another project to reuse the workflow. Project-specific instructions in a nearer `AGENTS.md`, `CLAUDE.md`, or tool config override this file.

## Operating Rules

- Read this file first, then read the nearest project or subsystem guidance before editing.
- Prefer the project's existing architecture, tools, tests, and conventions over generic methodology.
- Use the lightest workflow that manages the actual risk.
- Ask before large refactors, new dependencies, public API changes, or irreversible actions.
- Keep changes narrowly scoped and verify them with relevant tests or explicit review when tests are not available.

## Default Development Loop

1. **Prime context**: read repo guidance, coding standards, touched modules, tests, and recent related changes.
2. **Clarify scope**: state behavior change, non-goals, likely files, risks, and validation plan before editing.
3. **Plan the patch**: split work into reviewable steps and prefer existing local patterns.
4. **Implement incrementally**: make small diffs, avoid unrelated cleanup, and preserve compatibility unless explicitly changing it.
5. **Verify**: run the narrowest meaningful tests first, then expand when the change touches broader contracts.
6. **Review before handoff**: inspect the diff for regressions, missing tests, public API drift, dependency creep, and docs or release needs.
7. **Handoff**: summarize what changed, what was verified, what remains risky, and the recommended next action.

## When to Escalate

Use the default loop for routine fixes. Escalate to a formal spec workflow when a change affects public APIs, developer-facing behavior, security boundaries, concurrency, scheduling, memory ownership, performance-critical paths, migrations, or release compatibility.

Formal workflow artifacts:

1. **Charter / constraints**: architecture boundaries, compatibility rules, performance budget, security posture, autonomy level, and test expectations.
2. **Ready contract**: outcome, user value, scope, non-goals, owner, branch, and success criteria.
3. **Acceptance criteria**: domain-language behavior covering happy path, edge cases, errors, security, compatibility, and performance.
4. **Gherkin spec when useful**: `Feature`, `Scenario`, `Given`, `When`, `Then`, written without implementation leakage.
5. **Architecture plan**: touched modules, API changes, lifecycle model, test matrix, rollback or migration story, and explicit charter check.
6. **Implementation with two test streams**: acceptance or integration tests for behavior plus unit tests for internal structure.
7. **Review and hardening**: code review, security review, performance regression check, and mutation or fault-injection testing when practical.

## Review Lenses

Apply these lenses before declaring framework-level or reusable infrastructure work done:

- **API Contract Guardian**: public names, arguments, defaults, schemas, serialization, and stability tests remain intentional.
- **Compatibility & Migration Reviewer**: old behavior still works or has an explicit migration and release note path.
- **Error Model Designer**: exceptions, warnings, logs, and user-facing failure modes are precise and stable.
- **Lifecycle & Concurrency Reviewer**: ownership, cancellation, cleanup, streams, locks, async state, and forked resources are safe.
- **Performance Regression Guard**: hot paths avoid new synchronization, allocation churn, CPU overhead, and compute regressions.
- **Security & Abuse Reviewer**: extension points, file/network/process boundaries, untrusted inputs, and secrets handling are checked.
- **Dependency Gatekeeper**: new dependencies are avoided unless they remove more long-term burden than they add.
- **Docs-as-Tests Reviewer**: docs, examples, and quickstarts match runnable behavior for user-facing changes.
- **Test Matrix Reviewer**: relevant versions, backends, platforms, and failure cases are covered or called out.
- **Release Readiness Reviewer**: versioning impact, changelog, migration notes, CI scope, and rollback are clear.

## Tool Routing

- **Codex**: local code edits, tests, repo spelunking, diffs, implementation review, and second opinions.
- **Claude Code**: slash-command workflows, installed skills, marketplace plugins, and specialist sub-agents.
- **DAE / ATDD**: feature-level work needing charter, acceptance criteria, Gherkin, architecture plan, dual test streams, and mutation hardening.
- **gstack-like review**: product challenge, architecture review, QA, security review, benchmark review, and ship readiness.
- **Docs lookup**: use repo docs and source first. For external or fast-changing APIs, use Context7 or equivalent official-docs lookup before relying on memory.

See `.claude/AGENTIC_WORKFLOW.md` for command examples, `.claude/skills/*/SKILL.md` for bundled local skills, and `SKILL_CATALOG.md` for the external tool inventory.
