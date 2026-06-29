# Installation & Configuration

## Prerequisites

| Dependency | Minimum | Check |
|-----------|---------|-------|
| Python | 3.11+ | `python --version` |
| Git | 2.30+ | `git --version` |
| Backend CLI | — | `codex --version` / `claude --version` / `opencode --version` |

## Install

### From wheel

```bash
pip install everrun-0.1.0-py3-none-any.whl
```

Verify:

```bash
everrun --version
```

### From source (development)

```bash
git clone <private-repo-url> everrun
cd everrun
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -e .
```

## Backend Setup

EverRun supports three coding backends. At least one must be available on PATH.

### Codex

```bash
pip install openai-codex
codex --version
```

### Claude / OpenCode

Follow the respective CLI installation guides. Both must be available as shell commands:

```bash
claude --version
opencode --version
```

## Initialization

```bash
everrun init
```

Creates `.everrun/` with default configuration:

- `role-assignment.json` — backend chain order
- `impl-pack.system.txt` — pack generation prompt
- `validation.env` — default validation commands

### Configure backend chain

Edit `.everrun/role-assignment.json`:

```json
{
  "coder":  { "chain": ["codex", "opencode", "claude"] },
  "planner": { "chain": ["claude", "codex", "opencode"] },
  "judge":  { "chain": ["codex", "claude", "opencode"] }
}
```

Order matters — the first available backend is used, others serve as fallback.

### Configure validation

Edit `.everrun/validation.env`:

```bash
PYTEST_ARGS="tests -q"
```

Add any project-specific validation commands.

## Running

```bash
everrun todo          # select/define the next task
everrun run           # start the bounded pack loop
```

EverRun will:

1. Generate or load an implementation pack from the task
2. Launch the coder to implement changes
3. Run validation commands
4. Invoke the planner to review and decide
5. Accept, retry, or escalate to human review

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `EVERRUN_MAX_ITERATIONS` | 5 | Max coder executions per pack |
| `EVERRUN_TARGET_ROOT` | `.` | Workspace root |
| `PYTEST_ARGS` | `tests -q` | Default validation command |
| `DEBUG` | `false` | Enable verbose backend error output |
