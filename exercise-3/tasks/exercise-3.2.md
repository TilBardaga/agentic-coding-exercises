# Exercise 3.2 — Code review and fix

**Prerequisite:** **[`exercise-3.1.md`](exercise-3.1.md)** complete (filtering shipped).

**Command index:** [`../README.md`](../README.md).

**Assistant session:** Continue the **same chat** as **3.1** (not a new thread). See **[`../README.md` § Chat / assistant sessions](../README.md#chat--assistant-sessions)**.

**Workshop workflow:** This step completes the **technical** loop for the **3.1** change set: **`/code-review`** → **`/code-review-fix`**. See **[`../README.md` § Suggested agent workflow](../README.md#suggested-agent-workflow)**. **`/finish`** and **`/push`** are **out of scope** here.

---

## Goal

Improve **quality and safety** of the code from **3.1**.

---

## Steps

1. **`/code-review`** — [`.agents/commands/code-review.md`](../../.agents/commands/code-review.md). Use the **same job folder** as 3.1 (e.g. `docs/agent-jobs/catalog-filters-ex3/`) so **`code-review.md`** sits next to **`dev-plan.md`**.  
2. **`/code-review-fix`** — [`.agents/commands/code-review-fix.md`](../../.agents/commands/code-review-fix.md) to address findings, or document conscious deferrals.

---

## Done when

- [ ] **`code-review.md`** exists with concrete findings.  
- [ ] Fixes applied **or** deferrals documented; tests still green.

---

## Next

**[`exercise-3.3.md`](exercise-3.3.md)** (execution report, system review, docs).
