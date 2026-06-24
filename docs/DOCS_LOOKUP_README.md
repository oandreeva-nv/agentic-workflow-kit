# Context7 Or Equivalent Docs Lookup

This guide documents how to handle external or fast-changing documentation.

## Status In This Kit

Context7 is not bundled here. Use Context7, official vendor docs MCP servers, local docs, or another approved docs lookup tool in the agent/editor environment. For OpenAI product questions, use official OpenAI docs or the OpenAI docs skill when available.

## When To Use Docs Lookup

Use docs lookup before relying on memory for:

- external APIs and SDKs
- recently changing frameworks or libraries
- install commands
- configuration syntax
- security guidance
- cloud service behavior
- product or model availability
- deprecations and migrations

## Codex Prompt

```text
Before implementing, look up the current official docs for <library/tool> using the configured docs lookup tool. Prefer official documentation over blog posts. Summarize only the relevant API/configuration facts, cite the source, then apply the repo's existing patterns.
```

If no docs lookup tool is configured:

```text
State that no docs lookup tool is configured. Use local repo docs first. If internet access is required for current external docs, ask for approval or provide the exact docs page the user should verify.
```

## Source Priority

1. Repo source and local docs.
2. Official vendor docs through Context7, MCP, or equivalent.
3. Official vendor website.
4. Primary source code or release notes.
5. Secondary articles only when primary sources are unavailable, and label them as secondary.

## What To Capture

- exact version or date-sensitive assumption
- API names and options used
- deprecation or migration note
- source link
- how the docs fact changes the implementation or validation plan

## Guardrails

- Do not cite memory for changing APIs.
- Do not paste large chunks of docs into project files.
- Do not add dependencies based only on examples without checking repo constraints.
- Keep docs lookup scoped to the task.
