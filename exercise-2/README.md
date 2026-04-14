# Exercise 2 — PIV loop

In Exercise 1 you built product filtering the way you normally would — your process, your instincts. Now you will build the **exact same feature** again, but with the **PIV loop**: **Plan → Implement → Validate**.

**Why the same feature twice?** Because that is the only way to feel the difference. Same codebase, same requirements, same tests — the only variable is _how_ you work. By the end you will have two data points to compare.

> The `app/` folder is a **fresh copy** — identical to Exercise 1's starting point. You are not continuing your previous work. This is a clean slate.

**Code location:** [`app/`](app/)

---

## Step 1 — Start a fresh instance

You are starting a new exercise, so you need a **new** dev environment. Do not reuse the servers from Exercise 1 — stop them and start fresh from the `exercise-2/` folder.

**Option A — Let your assistant handle it.** Copy this into your AI assistant:

```
Stop any servers still running from exercise-1 (kill processes on ports 8000
and 3000). Then start a fresh dev environment for exercise-2:

Backend (from exercise-2/app/backend/):
- uv venv --python 3.12
- uv sync
- uv run python run_api.py

Frontend (from exercise-2/app/frontend/):
- bun install
- bun dev

These must run from the exercise-2 folder, not exercise-1.
Verify both are running and tell me when ready.
```

**Option B — Do it yourself.** Stop your old servers (Ctrl+C in each terminal window), then open two new terminals:

```bash
# Terminal 1 — Backend (from exercise-2/)
cd app/backend
uv venv --python 3.12
uv sync
uv run python run_api.py
# → http://localhost:8000
```

```bash
# Terminal 2 — Frontend (from exercise-2/)
cd app/frontend
bun install
bun dev
# → http://localhost:3000
```

Either way, verify the app loads at http://localhost:3000 — you should see 30 unfiltered products, just like before.

---

## Step 2 — Plan before you code

This is the core of PIV. Before you touch any code, build a plan. Not a vague idea of what you will do — a real plan that you would be comfortable handing to a colleague.

### Why planning matters

Think about how you would approach a change in a large, production codebase — one where a careless edit could break something three layers away. You would not just start typing. You would:

1. **Map the territory** — Read the code. Trace the data flow. Understand how the pieces connect. Which functions call which? Where does data come from, where does it go? What patterns did the previous developers use, and why?

2. **Assess the impact** — If you change the API signature, what else breaks? If you add a new component, where does it fit in the existing hierarchy? What assumptions does the current code make that your change might violate?

3. **Sequence the work** — What needs to happen first? What can you build and verify independently before wiring things together? Where are the natural checkpoints where you can confirm things work before moving on?

This codebase is small, but the thinking is the same. The habit of planning _before_ coding scales to any codebase, any team, any level of complexity. Practice it here where the stakes are low.

### Writing the plan

You have the ticket specs further below — these describe _what_ needs to be built. Your job is to turn those specs into a plan that accounts for _how_ this specific codebase works.

**Option A — Build the plan with your assistant.** Give it the specs and the codebase, and ask it to think with you — not to generate code, but to help you understand and strategize:

```
I need to implement product filtering for this e-commerce app. Before we
write any code, I need to understand what we are working with and build an
implementation plan.

Phase 1 — Map the codebase:
Read the code in exercise-2/app/. For both backend and frontend, tell me:
- How is the code structured? What are the key files, functions, and models?
- How does data flow from the database/seed data through the API to the UI?
- What patterns and conventions does the existing code follow?
- What does the test file test_products_filtering.py expect from the API?

Phase 2 — Build the plan:
Here are the ticket specs for what we need to build:

[paste the backend and frontend specs from below]

Based on what you found in the codebase, write an implementation plan that
covers:
- What files we will change and what each change involves
- The order of implementation and why that sequence makes sense
- What could break or be affected by our changes
- A validation checkpoint after each meaningful step

Write this as a markdown document I can reference while we implement.
Do not write any code yet.
```

**Option B — Plan on your own.** Read through the codebase, the test file, and the specs below. Sketch out your approach — on paper, in a text file, however you think best. The important thing is that you have mapped the code and thought through the sequence before you start changing things.

Either way, keep the plan accessible. You will refer back to it throughout implementation.

### Review the plan before you start coding

You would not merge a pull request without reviewing it. Apply the same standard to your plan — especially if your assistant wrote most of it. Read through it like you would review a colleague's PR:

- **Spot the code smells early.** Does the plan propose a 200-line function where three smaller ones would be cleaner? Is it hardcoding values that should be configurable? Are there signs of spaghetti — logic tangled across layers that should be separate? These are cheaper to catch in the plan than during implementation.
- **Check the assumptions.** Does the plan reference functions, parameters, or patterns that you have not confirmed actually exist in the code? An AI-generated plan can be confidently wrong about what is in the codebase.
- **Think about edge cases.** What happens with negative prices? Empty search strings? A category that does not exist? These are easy to forget in a plan but painful to discover three files into implementation.
- **Watch for technical debt.** Is the plan taking shortcuts that will cost you later? Quick fixes compound — if the plan feels like it is cutting corners, push back now.
- **Do you actually agree with the approach?** If something feels off, it probably is. Change it now, not after the code is written.

Think of this as rubber duck debugging for your plan — except your AI assistant is the duck. Explain the plan back to yourself (or to the assistant). Does it hold up? The plan is _your_ plan. If the AI wrote it, that does not make it correct — it makes it a first draft. You are the reviewer, the architect, the one who decides what gets built. The more you own the plan now, the smoother implementation will go.

### The specs

These are the same requirements as Exercise 1, but this time you are using them as **input for your plan** — not jumping straight to code.

<details>
<summary><strong>Backend — [FEAT-1234] Add product filtering to the Catalog API</strong></summary>

**Description:** Users must be able to filter and search products in the catalog API. Today, `GET /api/products` returns all 30 products with no filtering.

**Requirements:** Add filtering and search to `GET /api/products`:

- **Price filtering:** min and max price query parameters
- **Category filtering:** filter by product category
- **Keyword search:** search in product names and descriptions
- **Sorting:** sort by price or name (ascending and descending)

All filters must be optional and work when combined.

**Acceptance criteria**

- [ ] All filter-related tests pass
- [ ] Invalid input returns correct HTTP 400 responses
- [ ] Backward compatible (no filters = all products)
- [ ] Follows existing patterns and conventions

**Technical notes:** validate query parameters; appropriate types for money; log filter operations.

**Definition of done:** all acceptance criteria met; `uv run pytest` passes.

</details>

<details>
<summary><strong>Frontend — [FEAT-1235] Add product filter UI to the frontend</strong></summary>

**Description:** Backend filtering is available on `GET /api/products` via query parameters. Users need a frontend to drive those filters and see filtered results.

**Requirements:** build a product filter UI wired to the backend:

- **Price range controls:** min and max price
- **Category selector**
- **Search field:** keyword search on names and descriptions
- **Sort controls:** sort by price or name
- **Filter actions:** apply and clear filters

The UI must handle loading states, empty results, and validation errors.

**Acceptance criteria**

- [ ] Price filter works and sends correct query parameters
- [ ] Category selection filters correctly
- [ ] Search field filters by keyword
- [ ] Sort options reorder results as expected
- [ ] Multiple filters work together
- [ ] Clearing filters shows all products again
- [ ] Validation errors are shown to users
- [ ] Empty state when no products match
- [ ] Loading state during filter operations
- [ ] All filter interactions logged to the console (structured JSON)

**Technical notes:** extend the API client for filter parameters and query strings; React Hook Form + Zod where appropriate; follow logging patterns; prefer existing shadcn components.

**Definition of done:** all acceptance criteria met; backend called with correct query parameters; manual checklist complete.

</details>

---

## Step 3 — Implement

This is where you hand off the coding to your assistant. You spent time building and reviewing the plan — now let the AI do what it is good at: writing code. Your job shifts from writing to steering.

> **Scope your assistant to `exercise-2/app/`** so it stays focused on the right files.

**Option A — Hand the full plan to your assistant and let it implement:**

```
Here is the implementation plan we built for product filtering:

[paste your plan, or reference it if the assistant already has it in context]

Implement the full plan. Follow the sequence we defined and the patterns
from the existing codebase. When you are done, give me a summary of every
file you changed and what you did in each.
```

This is the recommended approach. You already did the hard work — understanding the codebase, sequencing the changes, catching code smells and edge cases in the plan. The plan _is_ your control. Let the agent execute it.

**Option B — Implement step by step if you want tighter control.** If you prefer to review each change before the next one happens, break it up:

```
Start with step 1 of the plan only. Implement it, then stop and show me
what you changed. I want to review before we move to step 2.
```

This gives you more control at the cost of speed. It is useful when you are working in an area you are less familiar with, or when a step has high blast radius. But for most cases, a good plan means you can trust the execution and review the result as a whole.

**Either way, notice the difference from Exercise 1.** In the baseline, you may have given the AI the requirements and let it figure out everything — structure, sequence, approach. Here, you defined all of that in the plan. The AI is implementing _your_ design, not making its own decisions. That is the shift: you are the architect, the AI is the builder.

> **Plan not matching reality?** That happens — and it is fine. If your assistant runs into something unexpected, do not just let it improvise. Update the plan first, then continue. Refactoring your approach mid-flight is normal. Losing track of your approach is not.

---

## Step 4 — Validate

Once you have worked through your plan, do a final validation pass to make sure everything holds together end-to-end.

**Option A — Let your assistant run the checks and report back:**

```
We have finished implementing product filtering. Run a full validation:

1. Run the backend tests: cd app/backend && uv run pytest -v
2. Report which tests pass and which fail
3. If any tests fail, compare the failure to our implementation plan —
   is this something we planned for but got wrong, or something we missed?
4. Check that the frontend at http://localhost:3000 can reach the API
   and list any issues you can spot in the API client or components

Do not fix anything yet — just report what you find.
```

**Option B — Run it yourself:**

```bash
cd app/backend
uv run pytest -v
```

The `-v` flag gives verbose output so you can see each test individually. All filtering tests should pass.

**Check the UI manually** (both options):

- Do all filter types work individually?
- Do combined filters produce correct results?
- Does clearing filters reset to all 30 products?
- Are loading and empty states handled?

**If something fails**, go back to your plan. Was the issue in execution (you planned for it but implemented it wrong) or in planning (you missed it entirely)? That distinction is valuable — it tells you where your process needs tightening.

---

## Step 5 — Compare to your baseline

This is where the exercise pays off. Pull up your notes from Exercise 1 and compare.

| Metric | Exercise 1 (baseline) | Exercise 2 (PIV) |
|--------|----------------------|-------------------|
| **Time spent** (backend / frontend / total) | | |
| **Number of prompts** | | |
| **Iterations / rework** | | |
| **Confidence** (1–10): correctness | | |
| **Confidence** (1–10): understanding | | |
| **Confidence** (1–10): maintainability | | |
| **Control** — who was driving? | | |

Think about these questions:

- Was the planning step worth the time it took?
- Did the AI produce better output when you gave it a plan vs. broad instructions?
- Did you feel more in control of what was being built?
- How much did your plan change during implementation?
- Would you use this approach on real work?

---

## Done?

Check these before moving on:

- [ ] You wrote a plan before coding
- [ ] `uv run pytest` passes in `app/backend` (including the filtering tests)
- [ ] Filters work end-to-end in the browser
- [ ] You filled in the comparison table in Step 5

**What happens next:** We will do another short Q&A round. Think about what changed compared to Exercise 1 — was the plan useful? What surprised you? Did anything go _worse_ with PIV?

**After that: [Exercise 3 — Agent commands](../exercise-3/README.md).** You have now experienced unstructured and structured AI-assisted coding. In Exercise 3, you will use pre-built agent commands that take PIV further — with automated priming, planning, code review, and retrospectives.
