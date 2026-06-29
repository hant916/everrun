# Init

`everrun init` is the first-run command. Run it once inside your project:

```bash
cd your-project
everrun init
```

## What it does

`everrun init`:

- checks global readiness (Python, Git),
- detects which coding agent CLIs are available on your PATH,
- guides you when no coding agent is found (it does not install anything for
  you),
- creates `.everrun/`,
- creates or updates `.everrun/role-assignment.json` from the detected agents,
- creates `sdd/task-dir/`,
- creates a demo Impl Pack,
- prints the next command.

You do not need to run `everrun doctor` before `everrun init`. Init performs the
first-run readiness checks itself.

## Output

EverRun reports capability — what it can do now — not a list of what is missing.

### One coding agent (single-agent mode)

```text
EverRun init

✓ Coding agent ready: OpenCode
✓ Project initialized
✓ Demo pack created

Mode:
  single-agent

Next:
  everrun demo
```

A tip may appear, but missing optional agents are never shown as warnings:

```text
Tip:
  Add Codex or Claude Code later for stronger fallback.
```

### Two or more coding agents (multi-agent mode)

```text
EverRun init

✓ Coding agents ready: OpenCode, Codex
✓ Project initialized
✓ Demo pack created

Mode:
  multi-agent

Role chains:
  coder:   opencode, codex
  planner: codex, opencode
  judge:   codex, opencode

Next:
  everrun demo
```

### No coding agent (blocked)

```text
EverRun init

No coding agent found.

EverRun needs one external coding agent CLI:
  OpenCode, Codex, or Claude Code

Recommended:
  OpenCode + deepseek/deepseek-v4-flash

Install one agent, then run:
  everrun init
```

In this state, init exits non-zero and does not write a successful project
configuration with empty backend chains.

## Role assignment

Init writes `.everrun/role-assignment.json` automatically from the detected
agents.

Most users should not edit role-assignment.json manually during first setup.

To change a role later, use `everrun use` (see
[configuration.md](configuration.md)).

## Preview without writing

```bash
everrun init --dry-run
```

A dry run reports what would happen based on detected agents and writes no
project files. It performs no install action.

## Next

- [shape.md](shape.md) — shape your first bounded task
- [configuration.md](configuration.md) — role chains and config reference
