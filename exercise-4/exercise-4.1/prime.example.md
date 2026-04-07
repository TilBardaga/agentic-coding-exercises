---
description: Prime agent with codebase understanding (Context Retrieval Only)
---

# Prime: Load Project Context (`/prime`)

> [!NOTE]
> **Context-only mode:** Gather information only. Do not modify production code, rules, or protected config during `/prime`.

## Objective

Build a concise picture of **layout**, **governance**, **enforcement tooling**, and **repo state** so the next steps align with this **fullstack** template (Python API + web app).

## Process

### 1. Tracked layout and docs

- **Files:** Run `git ls-files` (large repos on PowerShell: `git ls-files | Select-Object -First 200` instead of `head`).
- **Doc hub:** Read [`docs/DOC_INDEX.md`](../../docs/DOC_INDEX.md) (quick links + SSOT map).
- **Architecture narrative:** Read [`docs/DOC_ARCHITECTURE.md`](../../docs/DOC_ARCHITECTURE.md).
- **Layer map:** Read [`docs/CODEBASE_MAP.md`](../../docs/CODEBASE_MAP.md).
- **Features:** List **`apps/api/src/features/`** (do not assume a fixed set beyond what exists).
- **Entry points:** Note **`apps/api/src/core/`**, **`apps/api/src/api/`**, and CLI entry in **`apps/api/pyproject.toml`** `[project.scripts]`.
- **Python API:** Read **`apps/api/README.md`**, **`apps/api/pyproject.toml`**, **`apps/api/tach.toml`**. Canonical commands from repo root: **`uv sync --directory apps/api`**, **`uv run --directory apps/api ps-check`**.
- **Web app:** Read **`apps/web/README.md`** and **`apps/web/package.json`**; note `ag-check`, Vite, and that norms **08–13** apply under **`apps/web/`** (Python API: **01–06**; cross-stack **07-debugging**: see **`.cursor/rules/INDEX.mdc`**).

### 2. Governance

- Read [`AGENTS.md`](../../AGENTS.md) and [`.cursor/rules/INDEX.mdc`](../rules/INDEX.mdc) (routing to numbered rules).
- If you will **edit** project rules, read [`.cursor/rules/README.md`](../rules/README.md) (SSOT matrix, DRY).
- Scan **`apps/api/tach.toml`** and **`apps/api/pyproject.toml`** for boundaries and tooling.

### 3. Multiple enforcers (know what fails independently)

- **Tree:** root `structure-whitelist.yaml` → **`uv run --directory apps/api ps-structure`**.
- **Imports:** **`apps/api/tach.toml`** → `tach check` (also inside **`ps-lint`**).
- **Style:** Ruff in **`apps/api/pyproject.toml`** → **`uv run --directory apps/api ps-format`** / **`ps-lint`**.
- **Features:** Feature `README` + `__init__.py` → **`uv run --directory apps/api ps-docs`**.
- **Map coverage:** [`docs/CODEBASE_MAP.md`](../../docs/CODEBASE_MAP.md) → **`uv run --directory apps/api ps-zombie`**.
- **Frontend:** `apps/web/structure-whitelist.yaml`, ESLint, `pnpm -C apps/web run ag-check` (also invoked from **`ps-check`** when `pnpm` is on `PATH`).

Do not assume one green check implies all others.

### 4. Active project state

- **History:** `git log -n 10` (prefer full subjects; avoid `--oneline` if messages carry detail).
- **Working tree:** `git status -sb` (branch + staged/unstaged).
- **Optional:** Scan `docs/jobs/` for in-flight **`plan.md`** when the task is multi-session or ambiguous.

### 5. Directional deep dive (optional)

If the user narrowed the topic (e.g. “e2e tests”), read only what matters; still **no edits**.

## Output report

Use clear headings and bullets:

- **Project overview** — purpose, stack (**`uv`** + Python from **`apps/api/pyproject.toml`**; **`apps/web`**: Node/pnpm + Vite/React per `apps/web/package.json`).
- **Architecture & boundaries** — features, **`apps/api`** `tach` layers, link to map/doc architecture.
- **Enforcement** — which of structure / tach / ruff / zombie / docs checks matter for this task.
- **Current state** — branch, status, recent commits.
- **Active jobs** (if any) — paths under `docs/jobs/` worth continuing.
- **Risks / ambiguities** — items to clarify before `/plan` or `/implement`.
