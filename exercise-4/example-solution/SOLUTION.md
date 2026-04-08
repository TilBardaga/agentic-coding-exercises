# Example solution: exercise 4 — `/prime` command

**Purpose:** Illustrate one possible **`/prime`** command: context retrieval only, output for the human.

---

## Important note

This is an **example**, not the only valid answer. Your repo may need fewer sections or different paths. The workshop ships a **richer** reference in **`../prime.example.md`**; this file stays shorter and generic.

---

## Example command file

**File:** `commands/prime.md` (example path; use your tool’s convention)

```markdown
---
description: Prime agent with codebase understanding (context retrieval only)
---

# Prime (`/prime`)

> **Context-only:** Gather information. Do not modify application code, tests, or `AGENTS.md` during this command unless the user explicitly asks outside `/prime`.

## Objective

Produce a concise picture of **repository layout**, **project rules**, **how quality is enforced**, and **current git state** so follow-up work stays aligned with this codebase.

## Process

### 1. Layout and entry points

- Run `git ls-files` (cap output on huge repos, e.g. first 200 paths).
- Read the root **`README.md`** and any **`docs/`** index or architecture note if present.
- Note main source directories and how the app is run (see `pyproject.toml`, `package.json`, or equivalent).

### 2. Governance

- Read **`AGENTS.md`** (or your project’s rule file at repo root).
- If the repo has editor/agent rules (e.g. `.cursor/rules/`), skim the index or README that explains how rules are organized.

### 3. Enforcement (independent checks)

- Identify linters, formatters, typecheck, and tests from config files (`pyproject.toml`, `package.json`, CI config).
- State clearly: **passing one check does not imply passing all**—list what can fail separately.

### 4. Repo state

- `git status -sb` — branch and working tree.
- `git log -n 8` — recent commit subjects.

### 5. Optional focus

If the user named a topic (e.g. “auth”), narrow file reads to that area; still **no edits**.

## Output report

Use clear headings:

- **Project overview** — purpose, main stack, how to run locally if documented.
- **Layout** — important directories and entry points.
- **Governance** — where rules live and what they emphasize.
- **Enforcement** — commands or CI steps that validate changes.
- **Current state** — branch, status, recent commits.
- **Risks / ambiguities** — what to clarify before planning or implementing.

Keep the report scannable (bullets, short paragraphs).
```

---

## Why this works

- **Explicit context-only** boundary reduces surprise edits.  
- **Governance + enforcement** sections match how real teams fail (lint vs test vs structure).  
- **Output for a human** matches Pattern 1: you verify the model “sees” the repo.

---

## Related file in this workshop

See **`../prime.example.md`** for a **detailed** command example (many concrete steps and checks).
