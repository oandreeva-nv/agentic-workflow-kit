# Context7 Or Equivalent Docs Lookup

Context7 is a documentation lookup platform by Upstash. It provides up-to-date, version-specific library documentation for coding agents through either a CLI + skills mode or an MCP server mode.

## Upstream

| Resource | Link |
|---|---|
| GitHub repo | https://github.com/upstash/context7 |
| Website | https://context7.com |
| npm MCP package | https://www.npmjs.com/package/@upstash/context7-mcp |
| npm CLI package | https://www.npmjs.com/package/ctx7 |

## Install

The upstream README recommends a free API key for higher rate limits and requires Node.js 18 or newer for the CLI.

```bash
npx ctx7 setup
```

The setup flow authenticates via OAuth, generates an API key, and installs the appropriate skill. It can install either CLI + Skills mode or MCP mode. You can target specific agents with flags such as:

```bash
npx ctx7 setup --claude
npx ctx7 setup --cursor
npx ctx7 setup --opencode
```

Manual MCP server URL:

```text
https://mcp.context7.com/mcp
```

Pass your API key via the `CONTEXT7_API_KEY` header when configuring manually.

Remove generated setup:

```bash
npx ctx7 remove
```

## Use

Prompt style:

```text
Create a Next.js middleware that checks for a valid JWT in cookies and redirects unauthenticated users to /login. use context7
```

Use an exact library ID when known:

```text
Implement basic authentication with Supabase. use library /supabase/supabase for API and docs.
```

CLI commands:

```bash
ctx7 library <name> <query>
ctx7 docs <libraryId> <query>
```

MCP tools listed upstream:

| Tool | Purpose |
|---|---|
| `resolve-library-id` | Resolve a library name into a Context7-compatible library ID |
| `query-docs` | Retrieve docs for a Context7 library ID and query |

## When To Use

Use Context7 or equivalent official-docs lookup before relying on memory for external APIs, SDKs, package configuration, cloud services, framework migrations, or recently changed behavior.

## Notes

- Context7 docs are community-contributed; use judgment for security-sensitive work.
- Prefer official vendor docs when a product has a first-party docs MCP or official manual.
- For OpenAI product questions, use official OpenAI docs / Codex manual first.
