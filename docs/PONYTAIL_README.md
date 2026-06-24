# Ponytail Workflow

This guide reserves the Ponytail layer in the stack.

## Status In This Kit

Ponytail is not bundled here, and this kit does not encode a verified public install source or command for it. Treat Ponytail as an optional external tool until your local installation, command names, and expected outputs are known.

## Intended Role

Use Ponytail as a workflow adapter or orchestration layer only if your team already has it installed and documented. In this kit, it should sit between general methodology and concrete agent execution:

```text
intent -> routed workflow -> agent/task selection -> validation handoff
```

## What To Install

Install nothing from this repo for Ponytail by default.

Before documenting real commands, capture:

- install source
- supported agent surfaces
- command names
- expected inputs and outputs
- whether it can edit files or only route work
- whether it overlaps with gstack, Superpowers, or GSD

## Codex Usage Without Ponytail Installed

Use local routing prompts instead:

```text
Follow AGENTS.md. Classify this task as lightweight, formal feature, framework contract review, or role-based review. Select the smallest matching local skill under .agents/skills and explain the selected workflow before editing.
```

## Placeholder Skill Mapping

| Ponytail Need | Current Local Substitute |
|---|---|
| Route task type | `agentic-lightweight-loop` or `agentic-formal-feature` |
| Ask review roles | `agentic-role-review` |
| Framework hardening | `framework-contract-review` |
| External docs lookup | Context7 or official docs lookup guide |

## Guardrails

- Do not claim Ponytail is installed unless a project-specific doc confirms it.
- Do not add Ponytail commands to shared docs until they are verified locally.
- Keep this guide as the adapter placeholder until a concrete installation exists.
