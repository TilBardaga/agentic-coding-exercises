# Exercise 3.5 — Free feature

**Prerequisite:** **[`exercise-3.4.md`](exercise-3.4.md)** complete (or your facilitator agrees to skip **3.4**).

**Command index:** [`../README.md`](../README.md).

**Assistant session:** **New chat** (separate from **3.4**). Run the **whole** capstone cycle here, starting with **`/prime`**, then **`/plan` → `/implement` → `/code-review` → `/code-review-fix`**; optional **`/execution-report`** / **`/system-review`** in this same chat. See **[`../README.md` § Chat / assistant sessions](../README.md#chat--assistant-sessions)**.

**Workshop workflow:** Follow **[`../README.md` § Suggested agent workflow](../README.md#suggested-agent-workflow)**. At minimum: **`/prime` → `/plan` → `/implement` → `/code-review` → `/code-review-fix`**. **`/execution-report`** and **`/system-review`** are **optional** for this capstone unless you want another full meta pass. **`/finish`** and **`/push`** are **out of scope** in this repo.

---

## Goal

Add **one small feature** you choose (API tweak, UI polish, extra filter, developer UX—keep scope **small and finishable in one sitting**) in **`exercise-3/app/`**.

---

## Steps

1. Describe the feature briefly (chat or [`CHANGELOG.md`](../CHANGELOG.md)).
2. Run **`/prime`** (optional focus: the area you will touch).
3. **`/plan`** → **`/implement`** if the change is multi-file or non-trivial; otherwise facilitator may allow a lighter path—still do **code review** + **code-review-fix** before calling the step done.
4. Run **[`check-project-health`](../../.agents/skills/check-project-health/SKILL.md)** (Implementation mode) for **`app/backend`** and **`app/frontend`**, or equivalent **`uv` / `pytest` / `ruff`** and **`bun check`**.

---

## Done when

- [ ] Feature works; checks you rely on are green.
- [ ] [`CHANGELOG.md`](../CHANGELOG.md) updated.
- [ ] **Code review** (and fixes as needed) completed for this change set.

---

You have completed the **3.1 → 3.5** chain for Exercise 3.
