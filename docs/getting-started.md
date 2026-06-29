# Getting Started

The fast path to your first successful EverRun run.

```bash
pip install everrun-0.1.0-py3-none-any.whl
cd your-project
everrun init
everrun demo
```

EverRun checks your local setup, configures the project, creates a demo pack, and gives you the next command.

Then start the real loop:

```bash
everrun pack-shape start
everrun run
everrun report
```

## The onboarding arc

```text
Install → Init → Demo → Shape → Run → Report → Repeat
```

1. **Install** the wheel.
2. **Init** inside your project — `everrun init` checks readiness and configures
   the project.
3. **Demo** — `everrun demo` runs a deterministic, no-model demo so you can see
   the bounded run loop, validation, decision, and report trail.
4. **Shape** — `everrun pack-shape start` turns fuzzy intent into a bounded
   Impl Pack.
5. **Run** — `everrun run` executes the next pack with validation and judgment.
6. **Report** — `everrun report` shows the verdict and evidence.
7. **Repeat** — shape the next bounded task from what you learned.

## What `everrun init` does for you

You do not need to run `everrun doctor` first, edit
`.everrun/role-assignment.json` by hand, or read a backend matrix before your
first demo. `everrun init`:

- checks global readiness (Python, Git),
- detects which coding agent CLIs are already on your PATH,
- initializes the project files,
- writes role chains from the agents it found,
- creates a demo pack,
- prints the next command.

## Coding agents

EverRun does not include a model runtime. It orchestrates one or more external
coding agent CLIs. **One coding agent is enough to start.**

- **0 coding agents** → init is blocked with a recommended install.
- **1 coding agent** → READY, single-agent mode.
- **2+ coding agents** → READY, multi-agent mode (stronger fallback and review).

See [install.md](install.md) for details.

## Where to go next

- [install.md](install.md) — install details and coding agents
- [init.md](init.md) — what `everrun init` does
- [shape.md](shape.md) — turn intent into a bounded Impl Pack
- [run.md](run.md) — run packs, read decisions and reports
- [habit-loop.md](habit-loop.md) — make the loop a daily habit
- [configuration.md](configuration.md) — config and role chains reference
- [troubleshooting.md](troubleshooting.md) — when something needs fixing
