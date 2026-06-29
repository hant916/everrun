# EverRun

**Bounded coding-agent runner.** Lets AI coding agents (Codex, Claude, OpenCode) execute implementation packs continuously with deterministic safety gates.

## Install

```bash
pip install everrun-0.1.0-py3-none-any.whl
```

Requirements: Python 3.11+, Git, and at least one supported backend CLI (codex / claude / opencode).

## Quick Start

```bash
everrun init          # first run only — creates .everrun/
everrun todo          # write or select the next task
everrun run           # execute the bounded pack loop
```

## How It Works

```
impl pack -> coder -> validation -> planner -> judge -> accept / retry / human_review
                    |
            controller (hard gates)
```

- **Coder** — writes files, runs commands
- **Controller** — checks hard gates (scope, forbidden paths, secrets, validation)
- **Planner** — semantic review, decide accept/retry/human_review
- **Judge** — optional deep review for high-risk changes

## Key Principles

- **Dirty workspace is not a hard bound.** Forbidden to commit != forbidden to exist. Only secrets block.
- **Recoverable runtime failures don't terminate.** Backend timeouts, auth errors, planner unavailability route to retry/fallback, not HUMAN_REVIEW.
- **Hard gates are deterministic.** Scope, forbidden paths, secrets — no LLM judgment on safety boundaries.
- **Every ACCEPT requires validation to pass and scope to be clean.**

## Docs

- [Installation & Configuration](docs/install.md)

## License

Proprietary. All rights reserved.
