# Run

Run executes the next Impl Pack with validation, judgment, and evidence.

```bash
everrun run
everrun status
everrun report
```

## Getting a pack into the queue

EverRun runs the next `.todo.json` Impl Pack in `sdd/task-dir/` by filename
order. There are two common ways to put a pack there:

- **Shape it** — `everrun pack-shape start`, then `/write` (see [shape.md](shape.md)).
- **Enqueue it** — `everrun enqueue` writes an Impl Pack from a task description.

## Run the pack

```bash
everrun run
```

On success the pack file is renamed from `.todo.json` to `.done.json` and the
loop continues to the next pack. On failure the file stays `.todo.json` and the
execution history is updated.

## Watch and review

```bash
everrun status   # latest run status
everrun report   # latest terminal report (verdict + next action)
everrun logs     # latest run log (use --debug for the raw trace)
```

Reports are written under `.everrun/history/<run-id>/` (execution report,
summary, and diagnosis). The final CLI screen prints paths to all of them.

## Decision states

Each pack reaches one terminal decision:

```text
ACCEPT            = validated and accepted
RETRY             = safe to retry
SHRINK_AND_RETRY  = reduce scope and retry
STOP              = cannot continue safely
HUMAN_REVIEW      = judge cannot safely decide
```

Use human review only when judgment is genuinely needed — not as a routine step.

## Next

- [habit-loop.md](habit-loop.md) — turn this into a repeatable daily loop
- [troubleshooting.md](troubleshooting.md) — validation failures and dirty workspace
