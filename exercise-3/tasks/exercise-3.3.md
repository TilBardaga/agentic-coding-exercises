# Exercise 3.3 — Execution report, system review, and repo meta

**Prerequisite:** **[`exercise-3.2.md`](exercise-3.2.md)** complete.

**Command index:** [`../README.md`](../README.md).

**Assistant session:** Finish **3.1–3.3** in this **same** chat. **Start a new chat** when you begin **3.4**. See **[`../README.md` § Chat / assistant sessions](../README.md#chat--assistant-sessions)**.

**Workshop workflow:** This is the **meta** segment of the full cycle: **`/execution-report`** and **`/system-review`** (steps 6–7 in **[`../README.md` § Suggested agent workflow](../README.md#suggested-agent-workflow)**). **`/finish`** and **`/push`** are **out of scope** here.

---

## Goal

Reflect **plan vs reality**, improve **process** in a **bounded** way, and maintain **lightweight** navigation docs: **`exercise-3/docs/`** (map, architecture, hub) plus **[`CHANGELOG.md`](../CHANGELOG.md)** at the exercise root.

---

## Steps

1. **`/execution-report`** — [`.agents/commands/execution-report.md`](../../.agents/commands/execution-report.md). Compare **`dev-plan.md`** to what happened in **3.1** and **3.2**.
2. **`/system-review`** — [`.agents/commands/system-review.md`](../../.agents/commands/system-review.md). Write **`system-review.md`** in the same job folder.
3. **Bounded Layer 1 changes:** at most **2** small, concrete edits to root [`AGENTS.md`](../../AGENTS.md) **or** [`.agents/rules/`](../../.agents/rules/INDEX.mdc) **or** **one** command file—no full rewrites. Extra ideas → **`system-review.md`**.
4. **Docs:** update [`docs/CODEBASE_MAP.md`](../docs/CODEBASE_MAP.md), [`docs/ARCHITECTURE.md`](../docs/ARCHITECTURE.md), and add a meaningful **[Unreleased]** bullet in [`CHANGELOG.md`](../CHANGELOG.md) for work through **3.3** (see [`docs/DOC_INDEX.md`](../docs/DOC_INDEX.md)).

---

## Done when

- [ ] **`execution-report.md`** and **`system-review.md`** exist beside **`dev-plan.md`**.
- [ ] **≤2** Layer 1 / command edits **or** proposals deferred in writing.
- [ ] Map + architecture updated; changelog entry for **3.1–3.3**.

---

## Next

**[`exercise-3.4.md`](exercise-3.4.md)** (repository abstraction).
