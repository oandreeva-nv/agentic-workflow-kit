# Code Review And Security Review Tooling

This guide documents the review and security layer.

## Status In This Kit

This repo bundles review methodology skills, not scanners. Use real scanners or plugins when installed; otherwise use local review lenses and clearly report that no scanner ran.

| Need | Tooling |
|---|---|
| General code review | Codex `/review`, manual review, or `agentic-role-review` |
| Framework/API review | `framework-contract-review` |
| Security review | gstack `/cso`, Codex Security plugin if installed, or local security lens |
| QA/test matrix | gstack `/qa` or `agentic-role-review` QA lens |
| Release readiness | gstack `/ship` or `agentic-role-review` release lens |

## Codex Review Invocation

```text
Use .agents/skills/agentic-role-review/SKILL.md and AGENTS.md.
Review this diff. Findings first, ordered by severity, with file/line references. Cover correctness, compatibility, lifecycle/concurrency, performance, security, tests, docs, and release risk.
```

Framework-specific review:

```text
Use .agents/skills/framework-contract-review/SKILL.md and AGENTS.md.
Review this framework/API change for public contract, migration, lifecycle, performance, security, docs, test matrix, and release readiness. Findings first.
```

Security-focused review:

```text
Review this diff for security and abuse risk. Focus on untrusted input, file/network/process boundaries, authz/authn, secrets, dependency risk, extension points, logging of sensitive data, and unsafe defaults. Findings first.
```

## Scanner Rule

If a real scanner, Codex Security plugin, SAST tool, dependency audit, or secret scan is not installed or not run, say that explicitly. Do not imply tool coverage from manual review.

## Evidence To Report

- commands run
- files reviewed
- findings and severity
- tests or scans passed/failed
- unverified risk areas
- next action

## Guardrails

- Findings first.
- Do not bury security issues in a summary.
- Avoid speculative vulnerabilities; tie findings to code paths.
- Separate manual review from automated scanner evidence.
- Re-run relevant validation after fixes.
