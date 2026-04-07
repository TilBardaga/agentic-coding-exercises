# Exercise 6: Build an `/execute` command

**Goal:** Create a reusable **`/execute`** command that takes a **structured plan file** (like the ones produced in **exercise 5**) and drives implementation **task-by-task**, with validation aligned to that plan—so “implement from plan” is not ad-hoc chat every time.

---

## Where this sits in the loop

```
/plan-feature  →  writes plans/[feature].md
      ↓
/execute       →  reads that file, implements tasks in order, runs checks
      ↓
validate / code-review / …  (e.g. exercise 7)
```

You are automating the **Implement** step of **Plan → Implement → Validate** when the plan already exists on disk.

---

## Prerequisites

- [ ] You have a **plan document format** you trust (from **exercise 5** Part A, or your own template). The execute command assumes that file contains ordered tasks, file paths, and validation commands—or you define how to interpret it.  
- [ ] You can add command files (e.g. `commands/execute.md`) or your tool’s equivalent.  
- [ ] Optional: a real plan file in your repo to test against (from `/plan-feature` or hand-written).

---

## The problem

Without `/execute`, every implementation session starts fuzzy: the model might skip tasks, ignore your test commands, or edit files not listed in the plan. A good **execute** command:

- Loads the **plan as the source of truth**  
- Works **tasks in order**  
- Runs **validation** the plan specifies  
- **Reports** what changed and what is left  

---

## Your task

Create **`/execute`** (or `implement`, `run-plan`—pick one name and stick to it) that:

1. **Accepts** the path to a plan file (argument `$1` or your tool’s equivalent).  
2. **Reads** `AGENTS.md` (or your project rules) and the plan **in full** before editing code.  
3. **Implements** following the plan’s tasks (same order unless the plan says otherwise). If something **unexpected** shows up while implementing (missing file the plan assumes, a contradiction with the real codebase, a step that no longer applies), **pause**, report what happened, and wait for direction—do not improvise scope to “push through.”  
4. **Runs** the validation commands from the plan (lint, tests, typecheck—whatever the plan lists), at least at the end; optionally after each task if your plan supports that.  
5. **Outputs** a short summary: files touched, commands run, failures, open risks.

**Out of scope for a minimal v1:** fixing the plan file, auto-generating new tasks, or full CI—focus on **faithful execution** of what is written.

---

## Design checklist

| Question | Why it matters |
|----------|----------------|
| What if the plan is ambiguous? | Instruct the agent to **stop and ask** (or write a short “blocked” section) instead of guessing. |
| What if reality diverges mid-implementation? | **Pause and report**—unexpected deps, wrong paths, or conflicts with the repo are not something to silently work around by expanding scope. |
| What if validation fails? | Retry vs stop: define **one** default (e.g. fix and re-run once, then report). |
| Fresh context? | Many teams run execute in a **new** session with only the plan + rules—say so in the command. |
| Scope creep? | Instruct: **only** files/tasks in the plan unless the user explicitly expands scope. |

---

## Reference example

See **`example-solution/execute.example.md`** for a full command body you can adapt (paths, validation policy, tone).

---

## Testing

1. Create or pick a **real** `plans/…md` (from `/plan-feature` or minimal hand-written).  
2. Run **`/execute <path>`** in a context where the model can edit the repo.  
3. Check: task order respected? Validation commands from the plan actually run? Summary matches reality?

---

## Success criteria

- [ ] You can run **`/execute <plan>`** without re-explaining the feature in chat.  
- [ ] The agent **follows the plan structure** your exercise 5 template expects.  
- [ ] Validation from the plan is **not skipped silently**.  
- [ ] Output is **honest** about what completed vs what failed.

---

## Common pitfalls

- **Skipping the plan:** jumping to “I’ll just implement the feature” without anchoring on the file.  
- **Ignoring validation:** merging without running the plan’s commands.  
- **Over-building:** the first version should not try to chain ten other commands—keep execute **readable**.

---

## Next step

After execute works, use **exercise 7** (`/code-review`, execution report + `/system-review`) to tighten **quality** and **process** around the same loop.

---

## Takeaway

**Execute** is the contract between **planning** and **shipping**: same input/process/output idea as other commands, but the consumer is **your repo** and the **plan file** is the spec.
