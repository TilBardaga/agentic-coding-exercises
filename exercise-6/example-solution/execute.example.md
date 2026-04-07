---
description: Execute a structured implementation plan from disk (task order + validation)
argument-hint: "[path-to-plan.md]"
---

# Execute (`/execute`)

> **Contract:** The plan file is the specification. Do not invent scope beyond it unless the user explicitly adds instructions in this session.

## Objective

Read the implementation plan at **`$1`**, implement the work **in task order**, run the **validation commands** listed in the plan, and report what you did.

## Context to load first

1. **`AGENTS.md`** (repo root) — project rules and conventions.  
2. **Plan file** — `$1` (read completely before editing application code).  
3. Optional: **`README.md`** or architecture notes **only if** the plan references them.

## Process

### 1. Parse the plan

- Identify **tasks** (numbered sections, checklist, or whatever structure your plan template uses).  
- Extract **files to create or modify** per task.  
- Extract **validation commands** (lint, typecheck, tests) and when to run them (end-only vs per task—follow the plan; if unclear, run at least once before finishing).

### 2. Implement task by task

For each task in order:

- Do the **smallest change** that satisfies the task.  
- Keep edits **limited** to paths and concerns described in the plan.  
- If a task is **impossible**, **ambiguous**, or you hit something **unexpected** while implementing (file missing, API or layout differs from what the plan assumes, step that contradicts the current codebase), **stop**. Write a short “Paused / blocked” note: what you expected, what you found, and what you need from the user—do not silently skip or expand scope to “fix” the surprise.

### 3. Validate

- Run the plan’s validation commands in the order given.  
- If something fails: attempt a **reasonable fix** if it is clearly in scope; otherwise document the failure and remaining work.

### 4. Report

Produce a concise summary with headings:

- **Plan:** path to `$1`  
- **Tasks completed** — bullet list or checkmarks  
- **Files changed** — paths  
- **Commands run** — including validation  
- **Failures / blockers** — or “none”  
- **Follow-ups** — optional improvements not in the plan  

## Important

- **Do not** refactor unrelated modules “while you’re here.”  
- **Do not** change the plan file unless the user asked you to update the spec.  
- Prefer a **new session** with only plan + rules loaded if your workflow allows—reduces drift from old chat context.
