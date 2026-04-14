# Exercise 3.1 — Prime, plan, implement

You are building product filtering one more time — same feature as Exercises 1 and 2. But this time, the workflow is fully operationalized. Instead of writing prompts yourself, you use **agent commands** that handle the priming, planning, and implementation for you.

This is the first part of a three-part flow. **Parts 3.1, 3.2, and 3.3 all happen in the same chat session** — do not start a new chat until you reach 3.4. The assistant needs the full context of your plan, implementation, and review to do its best work.

**Code location:** [`../app/`](../app/)

---

## Step 1 — Prime the assistant

Before the assistant can plan anything, it needs to understand the codebase. The `/prime` command does this — it scans the repo structure, reads key files, checks recent history, and builds a mental model of what it is working with.

Run the **`/prime`** command ([`.cursor/commands/prime.md`](../../.cursor/commands/prime.md)) with a focus on the area you will be working in:

- **Cursor:** Type `@` in the chat, navigate to `.cursor/commands/prime.md`, select it, and add a focus like: `exercise-3/app, filtering, products API`
- **Other assistants:** Open `prime.md`, copy its content into your chat, and add the focus area

**Take a moment to read the output.** The assistant will give you a summary of the project structure, patterns, conventions, and recent changes. Does it match your understanding from Exercises 1 and 2? If something looks off or incomplete, ask follow-up questions before moving on.

---

## Step 2 — Create the plan

Now run the **`/plan`** command ([`.cursor/commands/plan.md`](../../.cursor/commands/plan.md)). Same approach as `/prime` — in Cursor, use `@` to select the file; in other assistants, copy its content into the chat. Give it a job name (e.g. `catalog-filters-ex3`) and the feature specs below.

The command will:
1. Analyze the codebase in depth
2. Map out which files need to change
3. Create a phased implementation plan with validation checkpoints
4. Write everything to `docs/agent-jobs/catalog-filters-ex3/dev-plan.md`

Feed the command the **catalog specs** below as the feature description — these are the requirements for what needs to be built.

<details>
<summary><strong>Backend — [FEAT-1234] Catalog API filtering</strong></summary>

**Description:** Users must filter and search via `GET /api/products` (baseline: all products, no filters).

**Requirements**

- **Price filtering:** min and max price query parameters
- **Category filtering**
- **Keyword search** in product names and descriptions
- **Sorting** by price or name (ascending and descending)
- All filters optional and combinable

**Acceptance criteria**

- [ ] All filter-related tests pass
- [ ] Invalid input → correct HTTP 400
- [ ] Backward compatible (no filters = all products)
- [ ] Follows existing patterns and conventions

**Technical notes:** validate query parameters; appropriate types for money; log filter operations.

**Definition of done:** acceptance criteria met; `uv run pytest` passes.

</details>

<details>
<summary><strong>Frontend — [FEAT-1235] Product filter UI</strong></summary>

**Description:** Drive `GET /api/products` query parameters from the UI.

**Requirements**

- Price range, category, search, sort, apply/clear
- Loading states, empty results, validation errors

**Acceptance criteria**

- [ ] Filters send correct query parameters; combine correctly
- [ ] Clear restores full list
- [ ] Validation errors visible
- [ ] Empty and loading states
- [ ] Filter interactions logged (structured JSON)

**Technical notes:** extend API client and query string; React Hook Form + Zod where appropriate; follow logging patterns; prefer shadcn components.

**Definition of done:** acceptance criteria met; manual checklist complete.

</details>

### Review the plan before moving on

This is the most important moment in the workflow. The `/plan` command produces a detailed `dev-plan.md` — open it and **read it carefully**.

Think of this as a PR review for the work that _has not happened yet_. Check for:

- **Code smells in the approach** — Is it proposing a 300-line function? Hardcoding values? Mixing concerns across layers?
- **Incorrect assumptions** — Does it reference files, functions, or patterns that do not exist? The AI can be confidently wrong about what is in the codebase.
- **Missing edge cases** — Negative prices? Empty search strings? Categories that do not exist?
- **Sequence risks** — If step 3 depends on step 2, is that dependency explicit? Will you be able to validate after each phase?

If something looks off, tell the assistant. Ask it to revise the plan. The plan is your control mechanism — a bad plan means a bad implementation, no matter how good the commands are.

> **Remember from Exercise 2:** you are the architect, the AI is the builder. This is where you do the architecture work.

---

## Step 3 — Implement

Once you are satisfied with the plan, run the **`/implement`** command ([`.cursor/commands/implement.md`](../../.cursor/commands/implement.md)) the same way. Point it to your job (e.g. `catalog-filters-ex3`).

The command will:
1. Read the full plan
2. Work through the implementation checklist in order
3. Follow the codebase conventions it found during priming
4. Mark each item as done in `dev-plan.md`
5. Run validation after each phase

**Let it work.** The plan is your control — the implementation should follow it. You do not need to micromanage each step unless you want to. This is the payoff of good planning: you can trust the execution because you shaped the approach.

> **Think about this:** In Exercise 1, you might have spent most of your time _during_ implementation correcting the AI. Here, you spent that time _before_ implementation, reviewing the plan. Which felt more productive?

**When it finishes**, take a moment to review what happened:

- Open `dev-plan.md` and check the implementation summary the command appended
- Look at the files that changed — do they match what was planned?
- Are there any items that were skipped or changed from the plan?

If something diverged from the plan, that is not necessarily a problem — but you should understand _why_ it diverged. Was the plan wrong, or did the implementation take a shortcut?

---

## Step 4 — Validate

Before moving to the code review in 3.2, make sure everything actually works.

**Run the tests:**

```bash
cd app/backend
uv run pytest
```

All filtering tests should pass. If any fail, share the error output with your assistant (still in the same chat) and work through the fix together.

**Check the UI:**

- Open http://localhost:3000 — do the filters work?
- Try combining multiple filters
- Clear all filters — do all 30 products come back?
- What happens with no results?

---

## Done?

- [ ] Backend and frontend match the acceptance criteria
- [ ] `uv run pytest` passes (including the filtering tests)
- [ ] Filters work in the browser
- [ ] `dev-plan.md` checklist reflects what was actually built

**Before you move on**, quick reflection: compare this to how you built the same feature in Exercise 1 and 2. How much time did you spend writing prompts vs. reviewing output? Did the commands produce better results than your manual prompts, or different ones?

**Next: [Exercise 3.2 — Code review and fix](exercise-3.2.md).** Stay in the same chat session — the assistant already has your plan and implementation in context.
