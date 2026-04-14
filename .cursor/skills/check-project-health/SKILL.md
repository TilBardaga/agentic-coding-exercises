---
name: check-project-health
description: >-
  Discover and run applicable tests, type checks, lint, and other health commands for the roots you
  actually changed (README / AGENTS / manifests). In implementation mode, apply simple fixes and re-run
  until green; in advisory mode, report first unless the user asks to fix.
---

# `check-project-health` skill

This file is the **single workflow** for project health in this repo.

## Modes

**Implementation mode** — You are executing **`/implement`** Step 3 (or the user told you to fix until checks pass). You **may** apply **simple fixes** (see below), **re-run** the failed checks, and repeat until all required checks **PASS** or you **stop** with a clear blocker.

**Advisory mode** — Standalone request (“run health check”), **`/finish`** preview, or plan-only review. **Do not** change application code unless the user explicitly asks to apply fixes **after** you showed the report. End with what failed and what you’d change.

---

**Compatibility:** Works with **whatever code you are actually changing**—any exercise, sample, or folder with **`app/backend`** and/or **`app/frontend`** (or trees documented in **README** / **`dev-plan.md`**). Discover `<backend-root>` / `<frontend-root>` from **git**, **plan paths**, and **manifests**; run **that** tree’s tests, lint, and types (not one global command from repo root).

## Context discovery

**A. Plan vs implementation**

- **Plan / job:** If validating a **`dev-plan.md`**, use it for checklist alignment and **plan-only** checks.
- **Implementation:** If validating code, use **git** + scope to find roots.

**B. Rules and docs**

- **`AGENTS.md`**, root **`README.md`**, **`setup/README.md`**.

**C. Tooling discovery (do not invent)**

| Source                         | Look for                                         |
| :----------------------------- | :----------------------------------------------- |
| **`package.json`**             | `test`, `lint`, `typecheck`, `build`, `check`, … |
| **`pyproject.toml`**           | pytest, ruff, mypy, pyright, scripts             |
| **`Makefile` / `justfile`**    | `test`, `lint`, `check`                          |
| **`Cargo.toml`**               | `cargo test`, `clippy`                           |
| **CI** (`.github/workflows/*`) | Same commands as CI                              |

If nothing is documented, say so—don’t guess `pytest` paths.

## This repository — commands for relevant app folders

For a **Python API package**, the usual pattern is **`pytest`**, **`mypy app/`**, **`pyright app/`**, **`ruff`**, optionally **uvicorn** + HTTP checks—all from the directory that contains that package’s **`pyproject.toml`**. There are **no** such checks at **repo root**; packages live under paths like **`**/app/backend`**, **`**/app/frontend`**.

**Do not hardcode** a parent folder name. For **each** backend/frontend root this session affects:

### 1) Find the relevant roots

Use **`git status`**, **`git diff`**, **`@`** scope, **`dev-plan.md`** paths. Common layout: **`app/backend`** (`pyproject.toml`, Python package **`app`**) and **`app/frontend`** (`package.json`). Parent can be **`exercise-*`**, **`agentic-coding-course-samples/`**, etc.—**discover from the change set**.

### 2) Backend (`<backend-root>`)

```bash
cd <backend-root>
uv sync
uv run pytest -v
uv run ruff check .
```

**Expected:** tests pass; ruff clean. No tests collected → report **SKIPPED** / note (still **PASS** if exit 0).

### 3) Types — mypy / pyright (same `<backend-root>`)

Only if `uv run mypy` / `uv run pyright` works; else **SKIPPED**.

```bash
uv run mypy app/
```

**Expected:** success / no issues message.

```bash
uv run pyright app/
```

**Expected:** zero errors. Use **basedpyright** if documented.

### 4) Frontend (`<frontend-root>`)

```bash
cd <frontend-root>
# e.g. bun install && bun run check — or npm/pnpm per package README
```

**Expected:** documented check script exits 0.

### 5) Local server (optional)

Only if user/plan wants runtime smoke. **Port** from README.

**Variant A — `run_api.py`:** from `<backend-root>`, `uv run python run_api.py`, then curl `/docs` or `/`.

**Variant B — uvicorn `app.main:app` (example 8123):**

```bash
cd <backend-root>
uv run uvicorn app.main:app --host 0.0.0.0 --port 8123
```

Then `curl` `/`, `/docs` as appropriate; stop process on Unix with `lsof`/`kill` or on Windows via Task Manager / closing the terminal.

### Docs-only jobs

If changes are only **`docs/`**, **`.cursor/`**, **`docs/agent-jobs/`**, skip app commands unless the plan requires them.

## Execution order (full pass)

0. Affected **`app/backend`** / **`app/frontend`** → run **This repository — commands** for each root.
1. Other documented lint/format.
2. Static types (project-wide if needed).
3. Tests (unit → integration if documented).
4. Monorepo patterns (`pnpm -C …`, `uv run --directory …`).
5. Build only if README/CI treats it as routine.

**Plan-only** (no code run): open **`dev-plan.md`**; verify Open questions, phases, Gates, checklist quality—**report only** unless user asks to edit the plan.

## Simple fixes (Implementation mode only)

You may apply **without asking** (then **re-run** the check):

- **Documented auto-fix:** `ruff check --fix`, `ruff format`, `bun run check:fix`, etc.
- **Trivial mechanical:** remove unused import, formatting-only, obvious comment typo, newline/whitespace if linter requires.

**Stop and escalate** (per **`/implement`** “unexpected” flow or ask user in advisory mode):

- Failing **tests** (assertions, behavior).
- **Type errors** needing design.
- Same check fails **twice** after a simple-fix attempt.
- Missing tools, env, secrets.

## Self-correction loop

**Implementation mode:** run checks → on FAIL, if **simple fix** applies do it → re-run **that** check → repeat until PASS or escalate.

**Advisory mode:** run checks → report → wait for user unless they already said “fix it”.

## Report

Structured summary: **PASS** / **FAIL** / **SKIPPED** per area (tests, types, lint, server if any, overall), **commands run**, errors (concise). **Advisory mode** may end with: _What next? (1) Apply fixes, (2) Specific item, (3) Nothing._

## Troubleshooting

| Symptom      | Try                                                     |
| :----------- | :------------------------------------------------------ |
| Tests fail   | Smallest failing test; traceback; fix logic or data.    |
| Lint         | Documented auto-fix, then manual.                       |
| Types        | Fix at path; re-run.                                    |
| Missing tool | `setup/README.md`; install deps.                        |
| Wrong cwd    | Match README (`pnpm -C`, `uv run --directory …`).       |
| Plan drift   | Compare to **`dev-plan.md`** (report-only in advisory). |

## Notes

- Prefer the same checks **`/finish`** would use when documented.
- Minimal exercises may define few tests—honest **SKIPPED** beats inventing commands.
