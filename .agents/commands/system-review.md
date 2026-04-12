---
description: >-
  Meta retrospective: compare dev-plan.md + execution-report.md for one job, classify divergences,
  and propose updates to plan template, /implement, and AGENTS.md—process quality, not code bugs.
argument-hint: <job-name> | <path-to-dev-plan.md> | <path-to-docs/agent-jobs/<job>/>
---

# System Review (`/system-review`)

Perform a **meta-level** analysis: how well did **implementation** follow **planning**, and what should change in your **system** (commands, templates, rules)—not a line-by-line bug hunt in application code.

## Purpose

**System review is NOT code review.** You are looking for **process** gaps: unclear plans, missing validation, repeated manual steps, bad divergence patterns.

**Your job:**

- Analyze plan adherence and divergence patterns (using the execution report’s honesty)
- Label divergences **justified** vs **problematic**
- Recommend concrete updates to **`AGENTS.md`**, **`/plan`** output, **`/implement`**, or new commands

**Philosophy:**

- Good divergence → improve planning or templates
- Bad divergence → improve clarity, constraints, or checks
- Repeated pain → automate or document

## Input: `$ARGUMENTS`

Resolve the **job directory** `docs/agent-jobs/<job-name>/` (same rules as **`/execution-report`**):

1. Directory under `docs/agent-jobs/`, or
2. Path to any file in that directory → use parent, or
3. `<job-name>` → `docs/agent-jobs/<job-name>/`

**Required inputs in that folder:**

- **`dev-plan.md`**
- **`execution-report.md`** (generate with **`/execution-report`** first if missing—if absent, stop and tell the user)

## Context & Inputs (four artifacts)

**Plan command (how planning was supposed to work):**  
`.agents/commands/plan.md`

**Implement command (how coding was supposed to work):**  
`.agents/commands/implement.md`

**Generated plan (what was specified):**  
`docs/agent-jobs/<job-name>/dev-plan.md`

**Execution report (what actually happened):**  
`docs/agent-jobs/<job-name>/execution-report.md`

## Analysis Workflow

### Step 1: Planned approach

From `dev-plan.md`:

- Scope, phases, gates, checklist intent
- Validation that was specified
- Patterns or files the plan assumed

### Step 2: Actual implementation

From `execution-report.md`:

- What shipped, what was validated
- Divergences and skips (already listed—**your** job is to **interpret** them)

### Step 3: Classify each divergence

**Good divergence (justified):** plan wrong about repo; better pattern; security/perf; environment block documented honestly.

**Bad divergence (problematic):** ignored explicit constraints; avoidable shortcuts; misunderstood requirements; silent skips.

### Step 4: Root causes (for bad divergences)

- Unclear or missing plan detail?
- Missing context in rules?
- Validation gap?
- Manual step repeated?

### Step 5: Process improvements

Actionable updates: **`AGENTS.md`**, plan template sections, **`/implement`** gates, new **`/validation`** steps, etc.

## Output

Save your analysis to:

**`docs/agent-jobs/<job-name>/system-review.md`**

(Overwrite prior system review for this job if you are re-running.)

### Suggested report structure

#### Meta

- **Job folder:** `docs/agent-jobs/<job-name>/`
- **Plan:** `dev-plan.md`
- **Execution report:** `execution-report.md`
- **Date:** [session date]

#### Overall alignment

Short score or narrative (e.g. **\_\_/10**) with one paragraph justification.

#### Divergence analysis

For each material divergence from the execution report:

- Planned / actual / reason / **classification** (good vs bad) / **root cause** (if bad)

#### Pattern compliance

Checklist: architecture, rules, testing, validation—as far as you can tell from the two documents (not a full re-audit of the codebase unless needed).

#### System improvement actions

Concrete checkboxes, e.g.:

- **Update `AGENTS.md`:** …
- **Update plan template / `plan.md`:** …
- **Update `implement.md`:** …
- **New command / automation:** …

#### Key learnings

- What worked in the **process**
- What to change **before the next job**

## Important

- Be **specific** (“which section of the plan was ambiguous,” not “plan was vague”).
- Focus on **repeatable** lessons.
- Prefer **suggested wording** for rule or command updates when possible.
