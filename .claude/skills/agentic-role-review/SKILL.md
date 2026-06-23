---
name: agentic-role-review
tags: [review, gstack, qa, security, release]
description: >
  Use for gstack-style review before handoff or shipping. Reviews a plan, diff,
  branch, or PR through product, architecture, devex, QA, security, performance,
  docs, test matrix, and release-readiness lenses.
license: Unlicense
---

# Agentic Role Review

Use this skill as a local gstack-style review layer. If gstack is installed, you can use its slash commands directly. If not, run this role review explicitly.

## Review Rules

- Findings come first.
- Order findings by severity.
- Include file and line references when reviewing code.
- Separate confirmed findings from open questions.
- Do not bury risks in a summary.

## Lenses

- **Product Challenger**: does the change solve the stated user problem without unnecessary scope?
- **Architecture Reviewer**: does it fit the existing boundaries and abstractions?
- **Developer Experience Reviewer**: are APIs, errors, docs, and workflows usable?
- **API Contract Guardian**: are public names, arguments, defaults, schemas, and compatibility intentional?
- **Lifecycle & Concurrency Reviewer**: are ownership, cleanup, cancellation, async state, and locks safe?
- **Performance Regression Guard**: does it add hot-path allocation, sync, extra IO, broad scans, or compute overhead?
- **Security & Abuse Reviewer**: are untrusted inputs, secrets, file/network/process boundaries, and extension points safe?
- **Dependency Gatekeeper**: are new dependencies justified and maintainable?
- **QA Lead**: are the right unit, integration, system, browser, platform, or regression tests present?
- **Docs-as-Tests Reviewer**: do docs and examples match runnable behavior?
- **Release Manager**: are versioning, changelog, migration, CI, rollout, and rollback clear?

## gstack Command Mapping

```text
/office-hours
/autoplan
/plan-eng-review
/plan-design-review
/plan-devex-review
/review
/devex-review
/qa
/cso
/benchmark
/ship
/land-and-deploy
/document-release
/retro
```

## Prompt

```text
Use the agentic-role-review skill. Review this plan/diff as Product, Architecture, DevEx, API Contract, Lifecycle/Concurrency, Performance, Security, Dependency, QA, Docs-as-Tests, and Release reviewers. Findings first, ordered by severity, with file/line references where possible.
```
