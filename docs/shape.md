# Shape

Shape turns fuzzy intent into a bounded Impl Pack.
Run executes that Impl Pack with validation, judgment, and evidence.

```text
prompt → shape → Impl Pack → run → evidence
```

EverRun is not a generic "natural language → magic code change" wrapper. The
product story is deliberate:

```text
fuzzy intent → shape → bounded Impl Pack → run → validation → judgment → evidence
```

## Start a shaping session

```bash
everrun pack-shape start
```

This opens an interactive session. Describe what you want in plain language; the
session helps you converge on a single bounded Impl Pack.

## Interactive commands

Inside a Pack Shape session:

```text
/help      Show commands
/draft     Show latest captured draft
/validate  Validate latest draft
/write     Validate and write latest draft to sdd/task-dir
/status    Show session status
/exit      Leave the session
```

(The bare words `help`, `draft`, `validate`, `write`, `status`, `exit`, and
`quit` work as aliases; anything else you type is routed to the backend as a
prompt.)

## When to use shape

Use shape when your intent is still fuzzy and you want to converge it into one
bounded, runnable task — rather than hand-writing the Impl Pack JSON yourself.

## The flow

1. Run `everrun pack-shape start`.
2. Describe the bounded task you want.
3. Use `/draft` to see the captured Impl Pack draft.
4. Use `/validate` to check the draft against the Impl Pack schema and bounds.
5. Use `/write` to validate and write the draft into `sdd/task-dir/`.
6. Leave with `/exit`.

The shaped pack lands in `sdd/task-dir/` as a `.todo.json` file — the same input
directory `everrun run` reads from.

## How it connects to run

Once the pack is written, run it:

```bash
everrun run
everrun report
```

See [run.md](run.md) for what happens during a run and how to read the result.

## Non-interactive helpers

If you already have a session, you can validate or write its draft without the
interactive loop:

```bash
everrun pack-shape list
everrun pack-shape validate <session-id>
everrun pack-shape write <session-id>
```
