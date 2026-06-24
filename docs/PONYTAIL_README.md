# Ponytail

Ponytail is an agent skill/plugin by Dietrich Gebert that pushes coding agents toward minimal, necessary solutions. Its core idea is a decision ladder: avoid building, reuse existing code, prefer standard library/native platform features, then write the minimum that works.

## Upstream

| Resource | Link |
|---|---|
| GitHub repo | https://github.com/DietrichGebert/ponytail |

## Install

### Claude Code

```text
/plugin marketplace add DietrichGebert/ponytail
/plugin install ponytail@ponytail
```

The upstream README notes those are two separate prompts.

### Codex

```bash
codex plugin marketplace add DietrichGebert/ponytail
codex
```

Then in the Codex TUI:

```text
/plugins
```

Select the Ponytail marketplace and install Ponytail. Then open:

```text
/hooks
```

Review and trust Ponytail's lifecycle hooks, then start a new thread. Restart the Codex desktop app after installing if you use the desktop app.

### Other Hosts

The upstream repo also documents installs for GitHub Copilot CLI, Pi, OpenCode, Gemini CLI, Antigravity CLI, CodeWhale, Swival, OpenClaw, Cursor, Windsurf, Cline, Kiro, Zed, and others. Use the upstream README for the current host-specific adapter.

## Use

Ponytail is often always-on after installation. It also exposes commands/skills such as:

```text
/ponytail [lite|full|ultra|off]
/ponytail-review
/ponytail-audit
/ponytail-debt
/ponytail-gain
/ponytail-help
```

The upstream README says Codex invokes Ponytail commands as skills, for example with `@ponytail-review`.

## Codex Prompt

```text
Use Ponytail if installed. Before adding code, check whether this can be skipped, reused from the codebase, handled by stdlib/native platform behavior, or implemented with a smaller existing dependency. Do not cut validation, security, accessibility, or data-loss handling.
```

## Notes

- Ponytail is not a replacement for tests or review.
- It should reduce over-engineering, not remove necessary safety checks.
- If Ponytail is not installed, use the prompt above as a manual discipline.
