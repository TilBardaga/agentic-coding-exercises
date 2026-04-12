---
description: Implement from an approved dev-plan on disk (respect phased plan and Gates)
argument-hint: <path-to-dev-plan.md> | <job-name> under docs/agent-jobs/
---

# Implement (`/implement`)

## Input: $ARGUMENTS

Resolve the plan file:

1. If `$ARGUMENTS` is a path to an existing `.md` file, use it.
2. Otherwise treat `$ARGUMENTS` as `<job-name>` and read **`docs/agent-jobs/<job-name>/dev-plan.md`**.
3. If unclear, ask the user for the exact path.

## Step 0 — Preconditions (open questions)

**Open questions are owned by `/plan`.** `/plan` must always emit this section (see template: **`## Open questions (resolved during planning)`**). This step is **mechanical**—no guessing.

1. **Locate** the section: the first `##` heading whose title **starts with** `Open questions` (after the `##` and optional space).
2. **If there is no such section → stop.** Tell the user: _`dev-plan.md` is missing the required “Open questions” section. Re-run or edit `/plan` so the template is complete._ Do not implement.
3. **If the section body contains** the exact all-clear sentence (allow leading/trailing whitespace on the line):  
   **`None — no open questions; all decisions recorded during planning.`**  
   → open-questions check **passes**; continue.
4. **Otherwise**, if the section has a **markdown table** whose header row includes **Decision** (e.g. **Decision / answer**):
   - For **each table body row**, the **Decision** column must be **non-empty** and must **not** be a placeholder (`…`, `...`, `<…>`, `TBD`, `TODO`, `?`).
   - If any row fails → **stop** and say: _Open questions in `dev-plan.md` are not fully resolved. Update decisions in the table or replace the table with the all-clear line above, then run `/implement` again._
5. **Otherwise** (no all-clear line and no valid table) → **stop**; treat as a malformed plan and ask the user to fix **`/plan`** output.

## Step 1 — Read

- Read **`AGENTS.md`** (or equivalent project rules) if present.
- Read the **entire** resolved plan file—especially **Phased implementation plan** (each **Phase D1, D2, …** and its **`#### Gate`**), **STEP-BY-STEP TASKS**, **Implementation checklist**, and validation.

Use the **Implementation checklist** as the **only** task list. Toggle `- [ ]` → `- [x]` as you complete items. **Do not** create a parallel `task.md`.

**Gates (stage boundaries):** After finishing all tasks for **Phase Dx**, satisfy that phase’s **Gate** (checkboxes under **`#### Gate`**) before starting **Phase D(x+1)**. If a Gate fails, **stop**, report, and wait—do not silently continue.

## Step 2 — Implement

- Follow checklist order unless the plan explicitly reorders.
- Touch **only** files and scope the plan describes.
- Apply project conventions from rules and existing code.

**Documentation:** Complete every **`Doc:`** item in the **Implementation checklist** (and any **Documentation impact** section in **`dev-plan.md`**) in the **same** change set as the code—do not defer a separate “doc-only” pass unless the user agrees. When scope includes **Exercise 3**, follow **`.agents/rules/06-workshop-exercise-3-documentation.mdc`** and **`exercise-3/docs/DOC_INDEX.md`**.

**Unexpected situations:** If something **not covered** by the plan appears (wrong paths, missing modules, failed assumptions, dependency/API drift, contradictory tests): **stop** changing product code (short read-only investigation is fine). Do a **brief, targeted** look (named files, one focused search). Then **tell the user** what you found, why it blocks following the plan as written, and give **2–3 logical options** (e.g. revise `dev-plan.md`, narrow scope, time-boxed spike). **Do not** improvise large scope changes without user choice.

## Step 3 — Validate

- Run every validation command the plan lists (lint, tests, typecheck, etc.).
- If the plan omits commands, run the **standard** checks documented in this repo’s README or configs (state what you ran).
- **Project health (skill):** When the plan includes **PROJECT HEALTH** or the change touches **`app/backend`** / **`app/frontend`** (under any parent), follow **`.agents/skills/check-project-health/SKILL.md`** in **Implementation mode**: discover roots, run the checks there (and any extra commands the plan’s **PROJECT HEALTH** section lists—**the plan wins** when more specific). If checks fail, apply **simple fixes** allowed by the skill, **re-run**, and repeat until all required checks **PASS** or you hit a **non-simple** failure—then stop and use the same escalation style as **Unexpected situations** in Step 2.
- If the job is **docs/rules only** and no app trees are in scope, skip the skill unless **PROJECT HEALTH** or the user requires it.

## Step 4 — Handover

- Append a **## Implementation summary** section to the **same** plan file you read (or add bullets under it if already present): what changed, commands run, results, open risks.
- In chat, give a short recap and point to that section.
