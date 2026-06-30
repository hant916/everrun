# Impl Pack Schema — v3.convergence

The Impl Pack is the contract between you and EverRun for a single bounded task.
Write it as a `.todo.json` file; EverRun reads it, normalizes it, and executes it.

```json
{
  "schema_version": "impl-pack.v3.convergence",
  "identity": { ... },
  "human_pressure": { ... },
  "machine_core": { ... },
  "judge": { ... },
  "runtime_governance": { ... }    // optional
}
```

---

## `schema_version` — required, string

Must be exactly `"impl-pack.v3.convergence"`.

---

## `identity` — required, object

| Field | Type | Required | Description |
|-------|------|:---:|-------------|
| `id` | `string` | Yes | Unique pack ID. No slashes, no `..`. Example: `"0001.hello-world"`. |
| `title` | `string` | Yes | Human-readable title. Example: `"Hello World CLI"`. |
| `slug` | `string` | No | Short URL-safe identifier. Derived from filename if omitted. |
| `type` | `string` | No | Pack classification: `"documentation"`, `"release_evidence"`, `"boundary"`, `"validation_infrastructure"`, `"checker"`. |

```json
"identity": {
  "id": "0001.hello-world",
  "title": "Hello World CLI"
}
```

---

## `human_pressure` — required, object

Human intent in plain language. The coder and planner both read this.

| Field | Type | Required | Description |
|-------|------|:---:|-------------|
| `one_screen_brief` | `string` | **Yes** | One-paragraph task description. Must be non-empty. |
| `goal` | `string` | No | Specific goal. Falls back to `one_screen_brief`. |
| `non_goals` | `string[]` | No | Explicitly out of scope. |
| `red_lines` | `string[]` | No | Hard constraints — "do not touch X", "preserve Y". |
| `do_not_misread` | `string[]` | No | Clarifications to prevent common misinterpretations. |

---

## `machine_core` — required, object

Machine-readable boundaries. This is how EverRun enforces scope.

| Field | Type | Required | Description |
|-------|------|:---:|-------------|
| `goal` | `string` | **Yes** | Concret target. Must be non-empty. |
| `files` | `object` | **Yes** | File scope definition. |
| `files.allow` | `string[]` | No | Allowed file patterns. Supports glob: `"src/**"`, `"README.md"`. Default `[]`. |
| `files.create` | `string[]` | No | Files the coder is expected to create. Also treated as allowed. |
| `files.forbid` | `string[]` | No | Forbidden patterns. Touching these blocks ACCEPT. Default `[]`. |
| `files.external_read_roots` | `object[]` | No | Read-only external directories. Each entry: `{"path": "/abs/path", "description": "..."}`. Added to forbid automatically. |
| `validate` | `string[]` | Yes | Shell commands. Exit 0 = pass. Example: `["pytest tests -q", "ruff check ."]`. |
| `acceptance` | `string[]` | No | Acceptance criteria. Merged into `judge.must_check`. |
| `red_lines` | `string[]` | No | Hard constraints merged with `human_pressure.non_goals`. |
| `failure_semantics` | `string[]` | No | Failure categories the planner should recognise. |
| `invariants` | `string[]` | No | Invariants that must hold. |
| `evidence_matrix_required` | `boolean` | No | If `true`, coder must produce an Evidence Matrix for ACCEPT. |
| `type` | `string` | No | Same as `identity.type`, can force judge invocation. |

---

## `judge` — required, object

Planner/judge acceptance contract.

| Field | Type | Required | Description |
|-------|------|:---:|-------------|
| `must_check` | `string[]` | **Yes** | Items the planner must verify before ACCEPT. |
| `reject_if` | `string[]` | **Yes** | Conditions that block ACCEPT regardless of other evidence. |
| `required` | `boolean` | No | If `true`, forces judge invocation even for ordinary packs. |

---

## `runtime_governance` — optional, object

Fine-tune EverRun's runtime behavior per pack.

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `max_coder_executions_per_pack` | `int` | `5` | Max coder iterations. Cap: `8`. |
| `accept_checkpoint.enabled` | `boolean` | `true` | Auto-commit accepted changes as a git checkpoint. |
| `validation_debt_classification.enabled` | `boolean` | `false` | Track pre-existing vs new validation failures. |
| `simple_retry.ruff_f401_only` | `boolean` | `true` | Enable F401-only planner bypass for simple lint fixes. |

---

## `execution_policy` — optional, object

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `max_attempts` | `int` | `3` | Max retry attempts for pack execution. |

---

## Minimal valid pack

The smallest possible V3 pack EverRun will accept:

```json
{
  "schema_version": "impl-pack.v3.convergence",
  "human_pressure": {
    "one_screen_brief": "Add a hello world function."
  },
  "machine_core": {
    "goal": "Create src/hello.py with a hello() function.",
    "files": {
      "allow": ["src/"]
    },
    "validate": ["python -c \"from src.hello import hello; hello()\""]
  },
  "judge": {
    "must_check": ["src/hello.py exists", "hello() prints greeting"],
    "reject_if": ["Validation failed"]
  }
}
```

`identity` is auto-derived from the filename. `files.create` and `files.forbid` default to `[]`. `acceptance` is merged into `judge.must_check`.
