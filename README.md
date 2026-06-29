# EverRun

Bounded coding-agent runner. AI writes code, the system applies safety gates.

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

## Next

- **[Getting Started](docs/getting-started.md)** — the fast path to your first run
- **[Release Onboarding](docs/release/v0.1.0-onboarding.md)** — verification checklist and canonical docs

## Docs

Start here:

- [Getting Started](docs/getting-started.md)
- [Install](docs/install.md) · [Init](docs/init.md) · [Shape](docs/shape.md) · [Run](docs/run.md) · [Habit Loop](docs/habit-loop.md)
- [Configuration](docs/configuration.md) · [Troubleshooting](docs/troubleshooting.md)

Reference:

- [Constitution](docs/constitution.md) · [Doctrine](docs/doctrine.md)
- [Runtime Governance](docs/runtime-governance.md)
- [Pack Shape](docs/pack-shape.md)
- [Release Evidence](docs/release-evidence/README.md)

---

One coding agent is enough to start. EverRun orchestrates external CLIs (OpenCode, Codex, Claude Code) — it does not include a model runtime.
