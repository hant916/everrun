# Install

## Install the wheel

```bash
pip install everrun-0.1.0-py3-none-any.whl
```

Confirm the installed version:

```bash
everrun version
```

Requirements:

- Python 3.9+
- Git on PATH
- At least one external coding agent CLI on PATH

## Coding agents

EverRun does not include a model runtime.
It orchestrates external coding agent CLIs.

You need at least one:

- OpenCode
- Codex
- Claude Code

One is enough to start.
Multiple agents improve fallback and independent review.

EverRun detects which agent CLIs are on your PATH and configures the project
around what it finds. It never installs these tools for you.

### Readiness model

```text
0 coding agents  = BLOCKED
1 coding agent   = READY, single-agent mode
2+ coding agents = READY, multi-agent mode
```

A single coding agent is a valid READY state, not a degraded one.

### Recommended first agent

If you have no coding agent yet, OpenCode is the recommended low-cost first-run
path:

```text
OpenCode + deepseek/deepseek-v4-flash
```

### Installing a coding agent

OpenCode:

```bash
npm install -g opencode-ai
```

Codex:

```bash
npm install -g @openai/codex
codex login
```

Claude Code:

```bash
npm install -g @anthropic-ai/claude-code
claude login
```

After installing one agent, run:

```bash
everrun init
```

## Next

- [getting-started.md](getting-started.md) — the fast path
- [init.md](init.md) — what `everrun init` does
- [troubleshooting.md](troubleshooting.md) — PATH and agent detection issues
