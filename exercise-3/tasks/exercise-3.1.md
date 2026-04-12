# Exercise 3.1 — `/prime` → `/plan` → `/implement`

Workflow step **3.1** for Exercise 3: ship **product filtering** (backend + frontend) in **`exercise-3/app/`** using the repo’s **committed commands** under **`.agents/commands/`** (open or **@** those files in your IDE).

**Command index:** [`../README.md`](../README.md) (table of paths).

**Assistant session:** Use **one chat through 3.3**—after this step’s **`/implement`**, continue in the **same** conversation for **3.2** (review + fix) and **3.3** (execution report + system review). See **[`../README.md` § Chat / assistant sessions](../README.md#chat--assistant-sessions)**.

---

## Goal

Implement **catalog filtering** with **`/prime`**, **`/plan`**, and **`/implement`**, producing a real **`dev-plan.md`** under **`docs/agent-jobs/<job-name>/`**. Continue with **3.2** for **`/code-review`** and **`/code-review-fix`** on the same change set. Full loop: see **[`../README.md` § Suggested agent workflow](../README.md#suggested-agent-workflow)**. **`/finish`** and **`/push`** are **out of scope** for this workshop repo.

---

## Catalog assignment (backend + frontend)

Use this as the **source of truth** for **`/plan`** and **`/implement`**.

### Backend — [FEAT-1234] Catalog API filtering

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

**Technical notes**

- Validate query parameters  
- Appropriate types for money  
- Log filter operations  

**Definition of done:** acceptance criteria met; `uv run pytest` passes.

### Frontend — [FEAT-1235] Product filter UI

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

**Technical notes**

- Extend API client and query string  
- React Hook Form + Zod where appropriate  
- Follow logging patterns; prefer shadcn components  

**Definition of done:** acceptance criteria met; manual checklist complete.

---

## Steps

1. **`/prime`** — follow [`.agents/commands/prime.md`](../../.agents/commands/prime.md). Optional focus: `exercise-3/app`, filtering, products API.  
2. **`/plan`** — follow [`.agents/commands/plan.md`](../../.agents/commands/plan.md). Job name e.g. **`catalog-filters-ex3`** → **`docs/agent-jobs/catalog-filters-ex3/dev-plan.md`**. Base the plan on the **catalog assignment** above plus patterns in **`app/`**.  
3. **Review** `dev-plan.md` (open questions resolved, gates clear).  
4. **`/implement`** — follow [`.agents/commands/implement.md`](../../.agents/commands/implement.md) with that job/path.

Scope implementation to **`exercise-3/app/`**; use **repo root** for `.agents` / `docs/agent-jobs` paths.

---

## Done when

- [ ] Backend + frontend match the **acceptance criteria** above.  
- [ ] `cd app/backend && uv run pytest` passes (including filtering tests).  
- [ ] Manual smoke: filters work in the browser.  
- [ ] `dev-plan.md` checklist reflects reality (or note intentional gaps).

---

## Next

Continue with **[`exercise-3.2.md`](exercise-3.2.md)** (code review).
