# DAE / ATDD With Claude Code And Codex

Disciplined Agentic Engineering (DAE) is an open-source Claude Code plugin set by Steve Freeman / `swingerman`. It formalizes a disciplined feature workflow around a human-signed charter, acceptance criteria, Gherkin specs, architecture planning, implementation, verification, and mutation hardening.

## Upstream

| Resource | Link |
|---|---|
| GitHub repo | https://github.com/swingerman/disciplined-agentic-engineering |

## What It Provides

The upstream repo packages three Claude Code plugins:

| Plugin | Purpose |
|---|---|
| `engineer` | DAE methodology kit: charter, feature intake, acceptance criteria, planning, refinement, verification, hardening |
| `atdd` | Acceptance Test Driven Development flow with Gherkin, acceptance/unit test streams, and mutation hardening |
| `crap-analyzer` | Change Risk Anti-Pattern analysis for changed code |

Feature checkpoints:

```text
0 Onboard -> 1.5 Ready -> 2 ACs -> 3 Spec -> 4 Plan -> 5 Implement -> 6 Refine -> 7 Light Verify -> 8 Hardening
```

## Install

Install in Claude Code:

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

## Use In Claude Code

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

## Codex Boundary

DAE's slash commands are Claude Code plugin commands. They do not run directly in Codex unless someone ports them into a Codex plugin.

Codex can still use DAE artifacts. Recommended handoff:

```text
Use AGENTS.md and .agents/skills/agentic-formal-feature/SKILL.md.
Implement the approved DAE feature in features/<id>/plan.md.
Read feature.md, acs.md, spec.md, and plan.md first.
Preserve the Ready contract and acceptance criteria.
Use acceptance/integration tests plus unit tests where the repo supports them.
Run the relevant validation commands and report evidence.
Do not claim mutation testing unless you actually run the mutation command.
```

## Codex-Only Substitute

If Claude Code DAE is unavailable:

```text
Use AGENTS.md and .agents/skills/agentic-formal-feature/SKILL.md.
Run this as a DAE/ATDD-style feature. First produce the Ready contract, acceptance criteria, Gherkin scenarios if useful, architecture plan, test matrix, and validation/mutation plan. Stop before implementation for approval.
```

## Notes

- Use real DAE in Claude Code when you want upstream `/engineer.*` or `/atdd:*` commands.
- Use Codex for repo validation, implementation, tests, and evidence.
- Do not claim DAE checkpoints are complete unless the corresponding command or documented equivalent actually ran.
