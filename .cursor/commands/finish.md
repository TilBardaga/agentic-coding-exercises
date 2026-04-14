---
description: Conclude a work session — sanity checks, validation if defined, atomic git commit (no push)
argument-hint: "[optional note for commit context]"
---

# Finish (`/finish`)

Use when you want to **land** session work: quick cleanup, run **this repo’s** checks if they exist, then **one clear commit**. **Do not push** from this command—use **`/push`** after.

> **Scope:** Workshop-friendly. This is **not** the fullstack template’s 14-step `/finish` loop (no forced `CHANGELOG` / semver unless your project already uses that workflow).

## Input: `$ARGUMENTS` (optional)

Short phrase for **commit intent** (e.g. `docs: prime directional focus`). If empty, derive the message from `git diff` and the task.

## Process

### 1. Light cleanup

On files you touched this session:

- Remove stray **debug** noise (`print`, `console.log` used for debugging, temporary comments).
- Remove **temporary** `TODO` / `FIXME` you added as placeholders—not every pre-existing todo in the repo.

If unsure whether something is intentional, **ask** instead of deleting.

### 2. Validation (if the repo defines it)

- Prefer following **`.cursor/skills/check-project-health/SKILL.md`** (**Advisory mode**: report-first unless you already asked to fix) for a structured pass, **or** manually check root **`README.md`**, **`AGENTS.md`**, and **`package.json` / `pyproject.toml` / `Makefile`** for documented lint, test, or typecheck commands.
- Run **what this repo documents** (nothing invented). If there is no standard check, skip and say so.

If validation fails, fix in scope or stop with a clear blocker—**do not commit broken checks** the project already enforces.

### 3. Git review

- `git status -sb`
- `git diff` (and `git diff --staged` if anything is already staged)

Summarize **what** changed and **risk** (low/med) in chat.

### 4. Staging decision

- List **staged** and **unstaged** paths.
- **Options:** (A) stage all intended files, (B) commit only what is already staged, (C) abort.
- If the user already said “stage all” / “option A”, proceed with **A** unless you see secrets (`.env`, keys), unexpected deletions, or huge unrelated churn—then pause.

### 5. Commit message

Use **Conventional Commits** style:

- `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:` — pick what matches the diff.
- **Subject:** imperative, ~50 chars, no trailing period.
- **Body** (optional but encouraged): bullets for non-obvious changes.

Example:

```text
docs(agents): add /finish and /push workflows

- Remove stub commit and template-only init-project command.
```

### 6. Commit

```bash
git add … # per staging decision
git commit -m "…"
```

Use a single **atomic** commit unless the user explicitly wants a split.

### 7. Handover

- Show **commit hash** (short) and the **message**.
- Say: _Local commit is ready; use **`/push`** to send it to the remote (after a clean tree and review)._

## Restrictions

- **Never** `git push` here.
- **Never** force-push, amend, or rewrite history unless the user explicitly asks.
