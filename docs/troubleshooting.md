# Troubleshooting

This is the repair manual. You should not need it for a first run.

`everrun doctor` is diagnostic.
You do not need to run it before every project.
`everrun init` performs first-run readiness checks.

Run doctor when something is wrong, in CI readiness checks, or to inspect your
environment in detail:

```bash
everrun doctor          # human-readable readiness report
everrun doctor --json   # machine-readable, for CI
```

Doctor reports coding-agent readiness as a verdict:

```text
0 agents → BLOCKED
1 agent  → READY (single-agent)
2+ agents → READY (multi-agent)
```

A single coding agent is READY, not a warning.

## No coding agent found

`everrun init` blocked with "No coding agent found".

EverRun needs at least one external coding agent CLI on PATH: OpenCode, Codex,
or Claude Code. Install one (see [install.md](install.md)), then re-run
`everrun init`. Recommended: OpenCode + `deepseek/deepseek-v4-flash`.

## OpenCode not on PATH

Confirm the CLI resolves:

```bash
opencode --version
```

If "command not found", reinstall it (`npm install -g opencode-ai`) and ensure
your shell PATH includes the global npm bin directory.

## Codex / Claude Code not on PATH

These are optional. If another agent is ready, EverRun runs in single-agent mode
and does not warn about the missing ones. To add them, install and log in:

```bash
npm install -g @openai/codex && codex login
npm install -g @anthropic-ai/claude-code && claude login
```

## git not found

EverRun requires Git on PATH for its run and validation flow. Install Git and
confirm `git --version` works.

## License missing

If your build enforces licensing, doctor reports a license error. Set the
license per your distribution's instructions, then re-run `everrun doctor`.

## Validation failed

A pack that fails its validation commands does not get accepted. Read
`everrun report` and `everrun logs --debug` to see which validation command
failed, fix the cause, and re-run.

## Dirty workspace

EverRun expects to operate on a workspace it can reason about. Commit or stash
unrelated local changes before running, and review changed files with your VCS
after a run.

## Single-agent FAQ

**Is single-agent mode degraded?** No. One coding agent is a valid READY state.
Multiple agents only add fallback and independent review.

## Model / profile format

OpenCode profiles use the `provider/model` form, for example:

```text
opencode/deepseek/deepseek-v4-flash
```

The recommended low-cost first-run model is `deepseek/deepseek-v4-flash`.

## When to run `everrun doctor`

- after install, if `everrun init` reports a problem,
- in CI to assert environment readiness (`everrun doctor --json`),
- when debugging PATH, backend, or license issues.

It is not part of the normal first-run path — `everrun init` already checks
readiness.
