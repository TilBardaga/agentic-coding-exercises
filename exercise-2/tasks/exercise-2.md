# Exercise 2 — PIV loop (catalog filtering)

Apply the **PIV loop** to the **same** filtering feature as **[Exercise 1](../../exercise-1/tasks/exercise-1.md)**: **P**lan → **I**mplement → **V**alidate → iterate.

**Code location:** [`../app/`](../app/) (under **`exercise-2/`**).

---

## Overview

> Scope your assistant to **`exercise-2/app/`**.

### Quick start

From **`exercise-2/`**:

```bash
cd app/backend
uv venv --python 3.12
uv sync
uv run python run_api.py
```

```bash
cd app/frontend
bun install
bun dev
```

### Goals

1. Apply **PIV** to a real full-stack implementation  
2. Compare smoothness, control, and trust vs. your Exercise 1 baseline  
3. Build **rich context** (your plan) before/with implementation  

### Assignment

#### Step 1 — Plan

Produce a **written implementation plan** using the **ticket-style specs** below (requirements, acceptance criteria, technical notes). Your plan should include success criteria, references to patterns in the codebase, work breakdown, and conventions.

#### Step 2 — Implement

Implement with the plan as context; keep the assistant aligned with your approach.

#### Step 3 — Validate

- `cd app/backend && uv run pytest tests/ -v`  
- Manual UI checks; iterate  

### Catalog specs (use in your plan)

#### Backend — [FEAT-1234] Catalog API filtering

**Description:** Users must filter and search via `GET /api/products` (today: all 30 products, unfiltered).

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

**Technical notes**

- Validate query parameters  
- Appropriate types for money  
- Log filter operations  

**Definition of done**

- All acceptance criteria met  
- `uv run pytest` passes  

#### Frontend — [FEAT-1235] Product filter UI

**Description:** Backend exposes filters on `GET /api/products` via query parameters; build UI to drive them.

**Requirements**

- Price range, category, search, sort, apply/clear  
- Loading states, empty results, validation errors  

**Acceptance criteria**

- [ ] Price filter sends correct query parameters  
- [ ] Category, search, sort work; filters combine  
- [ ] Clear shows all products again  
- [ ] Validation errors visible to users  
- [ ] Empty and loading states  
- [ ] Filter interactions logged (structured JSON)  

**Technical notes**

- Extend API client for filter parameters and query string  
- React Hook Form + Zod where appropriate  
- Follow logging patterns; prefer existing shadcn components  

**Definition of done**

- All acceptance criteria met; manual checklist complete  

### Tracking

Compare to Exercise 1: prompts, rework, control, understanding, confidence, alignment, plan drift.

### Success criteria

- ✅ Detailed plan **before** coding  
- ✅ Tests green; API + UI behave as specified  
- ✅ Code matches your planned patterns  
- ✅ You can explain how PIV differed from baseline  

### Tips

Don’t skip planning; be specific; validate often; update the plan when you learn.
