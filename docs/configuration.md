# Configuration

Reference for the project files EverRun manages. Most first-run users do not
need to edit these by hand — `everrun init` configures them for you.

## `.everrun/`

EverRun stores its project state under `.everrun/` in your project root:
runtime config, role assignment, logs, history, and reports.

## `.everrun/role-assignment.json`

This file maps each role to an ordered chain of backends. EverRun tries the
first backend in a chain, then falls back to the next.

The schema is three flat chains:

- `coder_chain`
- `planner_chain`
- `judge_chain`

### Single-agent config

With only OpenCode detected, all three chains use it:

```json
{
  "coder_chain": ["opencode"],
  "planner_chain": ["opencode"],
  "judge_chain": ["opencode"]
}
```

### Multi-agent config

Chains are ordered by per-role priority over the detected agents:

```json
{
  "coder_chain": ["opencode", "codex"],
  "planner_chain": ["codex", "opencode"],
  "judge_chain": ["codex", "opencode"]
}
```

All three agents:

```json
{
  "coder_chain": ["opencode", "codex", "claude"],
  "planner_chain": ["claude", "codex", "opencode"],
  "judge_chain": ["codex", "claude", "opencode"]
}
```

Entries may also carry an explicit model, for example
`opencode/deepseek/deepseek-v4-flash`.

## Changing a role

Use `everrun use <role> <agent> <model>`:

```bash
everrun use coder opencode deepseek/deepseek-v4-flash
everrun use planner claude claude-sonnet-4-20250514
everrun use judge codex gpt-4o
```

After configuring, run `everrun verify --models` to test connectivity.

## `everrun.toml`

`everrun.toml` is optional — every setting has a safe default. A missing or
unparseable file is never an error.

```toml
[core]
target = "."

[planner]
max_supplements_per_pr = 2
max_prs_per_task = 4
accept_score_threshold = 85
min_confidence_for_accept = 0.70

[governance]
max_coder_executions_per_pack = 4
```

See [release/install-ux.md](release/install-ux.md) for the full config
reference, defaults table, and override order.

## `.everrunignore`

Optional ignore file controlling which paths EverRun excludes from its view of
the project.

## `sdd/task-dir/`

The default input directory for Impl Packs. `everrun init` creates it and places
the demo pack there. `everrun pack-shape start` writes shaped packs here, and
`everrun run` executes the next `.todo.json` pack by filename order.
