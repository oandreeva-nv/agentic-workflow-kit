---
name: framework-contract-review
tags: [framework, api, compatibility, lifecycle, performance, security]
description: >
  Use when changing framework/library code where APIs, compatibility,
  lifecycle, errors, performance, tests, docs, and release behavior become part
  of the long-term developer contract.
license: Unlicense
---

# Framework Contract Review

Use this skill for framework, SDK, library, platform, plugin, or infrastructure code where downstream projects depend on stable behavior.

## Required Review Areas

### API Contract Guardian

- Public symbols and imports
- Constructor and function signatures
- Defaults and config schema
- Serialization and persistence
- API stability tests or snapshots

### Compatibility & Migration Reviewer

- Backward compatibility
- Feature flags or staged rollout
- Deprecation path
- Migration guide
- Changelog or release note

### Error Model Designer

- Exception types
- Warning behavior
- Logs and observability
- User-actionable messages
- Stable failure semantics

### Lifecycle & Concurrency Reviewer

- Ownership and cleanup
- Resource leaks
- Cancellation
- Async/task state
- Locks and ordering
- Thread, process, stream, or event-loop boundaries

### Performance Regression Guard

- Hot-path allocations
- Extra synchronization
- Broad scans or N+1 behavior
- Cache behavior
- Benchmark or microbenchmark coverage

### Security & Abuse Reviewer

- Untrusted input handling
- Secrets and credentials
- File, network, process, and plugin boundaries
- Sandbox or permission assumptions
- Supply-chain exposure

### Docs-as-Tests Reviewer

- Examples compile/run
- Quickstarts are current
- Public docs match implementation
- Edge cases and error cases documented

### Test Matrix Reviewer

- Supported versions
- Platforms
- Backends
- Failure modes
- Upgrade/downgrade paths

### Release Readiness Reviewer

- Semver impact
- Rollback plan
- CI scope
- Release notes
- Owner approval

## Prompt

```text
Use the framework-contract-review skill. Check API contract, compatibility, error model, lifecycle/concurrency, performance, security, dependencies, docs-as-tests, test matrix, and release readiness. Report blockers first with concrete remediation.
```
