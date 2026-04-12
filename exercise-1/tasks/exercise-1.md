# Exercise 1 — Baseline

Establish your **personal baseline** for AI-assisted coding **before** systematic techniques. Implement **product filtering** in the backend API and frontend of the e-commerce catalog **the way you would in a real project**.

**Code location:** [`../app/`](../app/) in this folder.

**Next (after this exercise):** **[`../../exercise-2/README.md`](../../exercise-2/README.md)** and **[`../../exercise-2/tasks/exercise-2.md`](../../exercise-2/tasks/exercise-2.md)** — same feature with a structured **PIV** loop.

---

## Overview

**Important:** This is a baseline, not a test. Use AI however feels natural—no required prompting style.

### Quick start

From **`exercise-1/`**:

**Terminal 1 — Backend**

```bash
cd app/backend
uv venv --python 3.12
uv sync
uv run python run_api.py
# → http://localhost:8000
```

**Terminal 2 — Frontend**

```bash
cd app/frontend
bun install   # install bun first if needed; see ../../setup/README.md
bun dev
# → http://localhost:3000
```

### Goals

1. **Ship a full-stack feature** from backend to frontend  
2. **Record your baseline** for time, effort, and confidence  
3. **Experience your current workflow** before later exercises  

**Reflect on:** smoothness, how much you understand, control, who is driving.

### Assignment

> Scope your assistant to **`exercise-1/app/`**.

Implement **catalog filtering** (you may build **without** treating the ticket text below as mandatory—you work ad hoc):

**Backend**

- **Price filtering:** min/max query parameters  
- **Category filtering**  
- **Keyword search** in names and descriptions  
- **Sorting** by price or name (asc/desc)  
- All filters optional and combinable  

**Frontend**

- Price range, category, search, sort, apply/clear  
- Loading, empty results, validation errors handled cleanly  

### Reference — ticket-style specs (optional)

For baseline you may stick to the bullets above. The tickets below are the **same** wording used in **[`../../exercise-2/tasks/exercise-2.md`](../../exercise-2/tasks/exercise-2.md)** (PIV), so you can compare later.

#### Backend — [FEAT-1234] Add product filtering to the Catalog API

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

#### Frontend — [FEAT-1235] Add product filter UI to the frontend

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

### Tracking

- Time (backend / frontend / total)  
- Prompts count, types, iterations  
- Confidence (1–10): correctness, practices, understanding, maintainability  
- Issues: AI mistakes, debugging, tests  

### Success criteria

- ✅ `uv run pytest` passes in `app/backend`  
- ✅ API applies filters correctly  
- ✅ Frontend filter UI works end-to-end in the browser  

### Notes

Not a competition—honest baseline. Reflect: what worked, what was slow, what you’d improve.

**Help:** [`../README.md`](../README.md) for entry; API docs at http://localhost:8000/docs when the server runs.
