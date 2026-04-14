# Exercise 1 — Baseline

In this exercise you will build a **product filtering feature** — backend API and frontend UI — using your AI coding assistant however you normally would. No special techniques, no required workflow. Just you and your assistant, the way you would work on a real task.

**Why?** The later exercises introduce structured approaches. To feel the difference, you need an honest starting point. This exercise _is_ that starting point.

> This is not a test or a competition. There are no wrong answers. The goal is to capture how you work _today_ so you can compare it to what comes next.

**Code location:** [`app/`](app/)

---

## Step 1 — Get the app running

Before you write any code, make sure the demo app starts up. You need **two terminal windows** — one for the backend, one for the frontend.

**Terminal 1 — Backend:**

```bash
cd app/backend
uv venv --python 3.12
uv sync
uv run python run_api.py
# → http://localhost:8000
```

**Terminal 2 — Frontend:**

```bash
cd app/frontend
bun install
bun dev
# → http://localhost:3000
```

Open http://localhost:3000 in your browser. You should see a grid of 30 products with no filtering. That is the starting point — your job is to add the filters.

> **Something not working?** Check the [troubleshooting section](../README.md#troubleshooting) in the main README. You can also ask your AI assistant — it tends to be faster at diagnosing PATH and dependency issues than scrolling through docs.

---

## Step 2 — Understand the codebase

Before jumping into implementation, take a moment to understand what you are working with. The app is small, but knowing the layout will save you time.

There are two ways to go about this — pick whichever suits you:

**Ask your assistant:** Open this exercise folder in your IDE and try something like:

```
Look at the code in exercise-1/app/. Walk me through the project structure —
what does the backend do, what does the frontend do, and where would I need
to make changes to add product filtering?
```

**Explore it yourself:** Here is the layout:

```
app/
├── backend/
│   ├── app/
│   │   ├── api/products.py            ← the API endpoint (you will edit this)
│   │   ├── services/product_service.py ← business logic (you will edit this)
│   │   ├── models/product.py          ← Pydantic models
│   │   └── data/seed_products.py      ← 30 sample products (do not edit)
│   ├── tests/
│   │   ├── test_products_basic.py     ← baseline tests (already passing)
│   │   └── test_products_filtering.py ← filtering tests (skipped — your goal)
│   ├── run_api.py
│   └── pyproject.toml
└── frontend/
    ├── src/
    │   ├── App.tsx
    │   ├── components/ProductGrid.tsx  ← product list (add filter UI here)
    │   └── lib/api-client.ts          ← API calls to the backend
    └── package.json
```

Two things worth noting:
- The **backend tests** for filtering already exist in `test_products_filtering.py` — they are just skipped. Your implementation needs to make them pass.
- The **API docs** are available at http://localhost:8000/docs once the server runs. Useful as a reference while you work.

---

## Step 3 — Build the feature

Now for the actual work. Implement **catalog filtering** for the product API and the frontend UI.

> **Scope your assistant to `exercise-1/app/`** so it focuses on the right files.

### What to build

**Backend — add filtering to the products API:**

- **Price filtering** — min and max price query parameters
- **Category filtering** — filter by product category
- **Keyword search** — search in product names and descriptions
- **Sorting** — sort by price or name, ascending or descending
- All filters are optional and must work when combined

**Frontend — add a filter UI:**

- Price range inputs, category selector, search field, sort controls
- Apply and clear buttons
- Handle loading states, empty results, and validation errors

### How to approach this

This is the baseline exercise — work however feels natural to you. A few approaches people commonly take:

- **Hand the requirements to your assistant** — copy the list above into your chat and let it propose an implementation. See how far it gets before you need to intervene.
- **Start with the backend** — read the test file, get the tests green, then build the frontend to match. Methodical, test-driven.
- **Start with the frontend** — sketch the UI you want, figure out what API shape you need, then build the backend to support it.
- **Read the code first, plan in your head, then write it yourself** — with or without AI assistance on specific parts.

There is no required order or method. The point is to see how _you_ work, not to follow a prescribed path.

> **Stuck or unsure about the expected API contract?** The skipped tests in `test_products_filtering.py` define exactly what the API should do. You can read them yourself, or ask your assistant: _"Read the tests in test_products_filtering.py and tell me what API contract they expect — what query parameters, what responses."_

---

## Step 4 — Validate your work

Once you think you are done, verify that everything works.

**Run the backend tests:**

```bash
cd app/backend
uv run pytest
```

The filtering tests that were previously skipped should now pass. If some fail, read the error output — it tells you exactly what the test expected vs. what it got. You can also paste the failing test output into your assistant and ask it to help diagnose the issue.

**Check the UI manually:**

- Do the filters work in the browser?
- Does combining multiple filters give correct results?
- Does clearing filters bring back all 30 products?
- What happens when no products match?

If the tests pass but something in the UI feels off, the issue is likely in the frontend's API client or how it sends query parameters — not in the backend logic.

---

## Step 5 — Record your baseline

Take a minute to write down how this went. You will compare these numbers to Exercise 2, so be honest — there is no right answer.

| Metric | Your answer |
|--------|-------------|
| **Time spent** (backend / frontend / total) | |
| **Number of prompts** sent to your assistant | |
| **Iterations** — how many times did you go back and change something? | |
| **Confidence** (1–10): how correct is your code? | |
| **Confidence** (1–10): how well do you understand what was generated? | |
| **Confidence** (1–10): how maintainable is the result? | |
| **Control** — were _you_ driving, or was the AI? | |
| **Issues** — anything the AI got wrong, debugging you had to do | |

Think about: what worked well? What was slow or frustrating? What would you do differently if you had to do this again?

---

## Reference — ticket-style specs (optional reading)

The bullet points in Step 3 are enough to complete this exercise. The tickets below contain the **exact same requirements** written as formal specs — the same wording used in [Exercise 2](../exercise-2/README.md). They are here so you can compare your baseline approach to the structured approach later.

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

## Done?

Check these before moving on:

- [ ] `uv run pytest` passes in `app/backend` (including the filtering tests)
- [ ] Filters work end-to-end in the browser
- [ ] You filled in the baseline tracking table in Step 5

**What happens next:** Before we move on, we will do a short Q&A round as a group. If you finish early, think about what stood out — anything surprising, frustrating, or interesting about how you and your assistant worked together. Observations, questions, tips for others — all fair game.

**After that: [Exercise 2 — PIV loop](../exercise-2/README.md).** You will build the exact same feature again, but this time with a structured Plan-Implement-Validate approach. Having your baseline fresh in mind will make the comparison meaningful.
