# EverRun

Bounded coding-agent runner. AI writes code, the system applies safety gates.

**[everrun.ailuros.io](https://everrun.ailuros.io)**

```bash
pip install everrun-0.1.0-py3-none-any.whl
cd your-project
everrun init
everrun demo
```

Then start the real loop:

```bash
everrun pack-shape start
everrun run
everrun report
```

---

## Impl Pack

An **Impl Pack** is the contract EverRun executes. It tells the coder what to build,
the controller what to guard, and the planner what to verify.

Write one as a `.todo.json` file. Copy the example and replace the fields:

- **[Impl Pack Schema](docs/impl-pack-schema.md)** — every field, type, and default
- **[Example Pack](examples/example-greeting-cli.todo.json)** — a complete, ready-to-customize template

Or generate one interactively with `everrun pack-shape start`.

---

## Next

- **[Getting Started](docs/getting-started.md)** — the fast path to your first run
- **[Release Onboarding](docs/release/v0.1.0-onboarding.md)** — verification checklist and canonical docs

## Docs

Start here:

- [Getting Started](docs/getting-started.md)
- [Install](docs/install.md) · [Init](docs/init.md) · [Shape](docs/shape.md) · [Run](docs/run.md) · [Habit Loop](docs/habit-loop.md)
- [Configuration](docs/configuration.md) · [Troubleshooting](docs/troubleshooting.md)

Reference:

- [Impl Pack Schema](docs/impl-pack-schema.md) — the full JSON contract
- [Example Pack](examples/example-greeting-cli.todo.json) — a complete, copy-pasteable starting point
- [Constitution](docs/constitution.md) · [Doctrine](docs/doctrine.md)
- [Runtime Governance](docs/runtime-governance.md)
- [Pack Shape](docs/pack-shape.md)
- [Release Evidence](docs/release-evidence/README.md)

---

One coding agent is enough to start. EverRun orchestrates external CLIs (OpenCode, Codex, Claude Code) — it does not include a model runtime.
