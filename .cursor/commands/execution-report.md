---
description: >-
  After /implement, write a factual execution report next to dev-plan.md (same agent job folder):
  scope, validation, divergences, and lessons—input for /system-review and retros.
argument-hint: <job-name> | <path-to-dev-plan.md> | <path-to-docs/agent-jobs/<job>/>
---

# Execution Report (`/execution-report`)

You **just finished** implementing from a plan. Before moving on, produce a **structured, honest record** of what happened: what shipped, how it was validated, where reality differed from `dev-plan.md`, and what should improve next time.

This artifact is **not** code review (bugs in code) and **not** system review (bugs in process). It is the **implementation journal**: the single source of truth for “what we actually did,” stored **with the job** that owns the plan.

## Input: `$ARGUMENTS`

Resolve the **job directory** `docs/agent-jobs/<job-name>/` (same folder as `dev-plan.md`):

1. If `$ARGUMENTS` points to an existing **directory** under `docs/agent-jobs/`, use it.
2. If it points to a file **`dev-plan.md`** (or any `*.md`) inside `docs/agent-jobs/<job-name>/`, use that file’s **parent** directory.
3. Otherwise treat `$ARGUMENTS` as **`<job-name>`** and use **`docs/agent-jobs/<job-name>/`**.
4. If **`dev-plan.md`** is missing there, stop and ask the user for the correct job or path.

## Output file (required)

Write **`docs/agent-jobs/<job-name>/execution-report.md`** (overwrite if it already exists for this run).

Do **not** write under `.cursor/` for this report—the job folder is the SSOT for plan + implementation artifacts.

## Context to capture

Reflect on:

- What you implemented vs what `dev-plan.md` described
- Validation you ran (commands and outcomes)
- Challenges and surprises
- Every **divergence** from the plan (with reasons)
- Anything **skipped** or deferred

## Report template

Use this structure (fill all sections; use “N/A” only when truly not applicable):

### Meta Information

- **Job / folder:** `docs/agent-jobs/<job-name>/`
- **Plan file:** `docs/agent-jobs/<job-name>/dev-plan.md`
- **Files added:** [paths]
- **Files modified:** [paths]
- **Lines changed (approx.):** +X −Y (from `git diff --stat` if helpful)

### Validation Results

- **Syntax & linting:** pass / fail / skipped — [commands run, outcome]
- **Type checking:** pass / fail / skipped — [if applicable]
- **Unit tests:** pass / fail / N/A — [counts]
- **Integration / e2e:** pass / fail / N/A — [counts]

### What Went Well

- [Concrete bullets]

### Challenges Encountered

- [What was hard and why]

### Divergences from Plan

For each divergence:

**[Short title]**

- **Planned:** [from dev-plan / checklist]
- **Actual:** [what shipped]
- **Reason:** [why it changed]
- **Type:** Better approach found | Plan assumption wrong | Security | Performance | Blocked by environment | Other

### Skipped Items

- [Checklist or plan item not done] — **Reason:** …

### Recommendations (optional, quick)

- **`/plan` / template:** …
- **`/implement`:** …
- **`AGENTS.md` / rules:** …

## Important

- Be **specific** (paths, commands, checklist items)—this file feeds **`/system-review`**.
- Do **not** invent work that did not happen.
- **No edits** to production code in this command—**write the report only** (unless the user explicitly asked to fix something else in the same turn).
