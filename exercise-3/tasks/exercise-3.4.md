# Exercise 3.4 — Repository abstraction (backend)

In 3.1 through 3.3 you built filtering, reviewed it, and reflected on the process. Now you are going to refactor the backend — without changing what it does.

The goal is to introduce a **repository layer** that separates _how products are loaded_ from _what you do with them_. Right now, the product data and the filtering logic probably live in the same place. That works for a small app, but in a real codebase it is a code smell — it couples your business rules to your data source, which means you cannot swap one without rewriting the other.

**Start a new chat session.** This is a separate piece of work — do not continue from the 3.1–3.3 thread. The assistant needs a clean context for this refactor.

**Code location:** [`../app/backend/`](../app/backend/)

---

## What you are building

This is a **refactor** — behavior stays the same, tests stay green, but the structure improves. You are introducing a clean seam between two concerns:

- **Service** = business rules. Filtering, sorting, validation — the _what_ you do with products.
- **Repository** = data access. Loading products, storing products — the _how_ you get them.

### The pieces

**1. `ProductRepository` (contract)** — A `typing.Protocol` (preferred) or ABC that defines what the service needs from data access. Keep it narrow: only methods the service actually calls. The names and signatures should mirror your current service API so the refactor is mostly _moving_ code, not redesigning it.

**2. `InMemoryProductRepository` (implementation)** — Implements the protocol using the in-memory product list. This is the single place that calls `get_seed_products()` — no other module should know where the initial data comes from. No database, no ORM, no async I/O.

**3. `product_service` (consumer)** — Rewire the service to use a `ProductRepository` instance instead of directly accessing a global product list. Filtering and sorting logic can stay in the service or move to the repository — pick one approach and be consistent. The workshop default: keep business rules in the service, let the repository handle loading and raw data access.

**4. Wiring** — Choose how the repository gets into the service:
- **Module-level default:** `_repo: ProductRepository = InMemoryProductRepository()` — simple, good for a small API
- **FastAPI `Depends()`:** Inject it — easier to swap in tests via dependency overrides

Either is valid. Document your choice in [`docs/ARCHITECTURE.md`](../docs/ARCHITECTURE.md).

**5. API layer** — Routers stay thin. They delegate to the service, not the repository (unless you chose `Depends` at the router level for wiring — then only the wiring lives there).

### Why this matters

After this refactor, you can:
- **Swap storage** (SQLite, Postgres) without rewriting your filtering logic
- **Test the service** with a fake repository instead of touching global state
- **Find data access code** in one place, not scattered across modules

These are not hypothetical benefits — they are the difference between a codebase that scales and one that turns into spaghetti as it grows.

---

## Step 1 — Prime

Start your new chat by running **`/prime`** with a focus on the backend:

- Focus on `exercise-3/app/backend` — specifically the service, data, and API layers

Read the output. You already know this codebase from 3.1, but the assistant in this new chat does not. Make sure it has an accurate picture of the current state — including the changes you made in 3.1 and 3.2.

---

## Step 2 — Plan

Run **`/plan`** with a new job name (e.g. `repo-abstraction-ex3`). Describe the refactor using the requirements above.

The plan should cover:
- Introduce the protocol
- Implement the in-memory repository
- Rewire the service
- Update the wiring
- Run tests after each meaningful step

### Review the plan

This is a refactor — the risk is breaking something that currently works. Read the plan carefully:

- **Does it preserve existing behavior?** The tests should pass at every step, not just at the end. If the plan has a step where tests _would_ break temporarily, that is a red flag.
- **Is the migration path clean?** You should be able to introduce the repository alongside the existing code, wire it up, and then remove the old approach — not rip everything apart at once.
- **Is the protocol narrow enough?** If it has methods the service does not actually call, push back. Unnecessary abstraction is its own form of technical debt.

---

## Step 3 — Implement

Run **`/implement`**. The command will follow the plan and keep tests green after each phase.

Since this is a refactor, the validation is straightforward: **the tests that were passing before must still pass after.** No new behavior, no new edge cases — just cleaner structure.

> **This is a good test of the workflow.** Refactoring is where bad process hurts most — you are changing the internals of working code, and every mistake is a regression. If the plan is solid and the implementation follows it, the tests stay green throughout. If they break, you know immediately where the process failed.

---

## Step 4 — Code review and fix

Run **`/code-review`** followed by **`/code-review-fix`**, both in the same job folder.

For a refactor, pay extra attention to:
- **Leftover references** to the old global product list — if the service still imports it directly somewhere, the refactor is incomplete
- **Leaky abstractions** — does the repository expose implementation details that the service should not know about?
- **Unnecessary complexity** — did the refactor introduce more indirection than needed? A repository layer should simplify, not complicate

---

## Step 5 — Validate and document

**Run the tests:**

```bash
cd app/backend
uv run pytest
```

All tests — including the filtering tests from 3.1 — must pass. If any test broke, the refactor changed behavior, which means something went wrong.

**Update the docs:**

- **[`docs/ARCHITECTURE.md`](../docs/ARCHITECTURE.md)** — Document the repository + service boundary and your wiring choice
- **[`docs/CODEBASE_MAP.md`](../docs/CODEBASE_MAP.md)** — Add the file paths for `ProductRepository` and `InMemoryProductRepository`
- **[`CHANGELOG.md`](../CHANGELOG.md)** — Short entry under `[Unreleased]`

**Optional:** Run `/execution-report` and `/system-review` if you want another round of process reflection. Not required — you already did a full meta cycle in 3.3.

---

## Out of scope

- Real SQL/ORM, migrations, connection pools
- Async database drivers, full DDD, event sourcing
- Changing HTTP contracts or frontend behavior

This is a backend refactor only. If the frontend breaks, something went wrong.

---

## Done?

- [ ] `ProductRepository` and `InMemoryProductRepository` exist
- [ ] The service uses the repository — no direct access to global product lists
- [ ] `uv run pytest` passes for `exercise-3/app/backend`
- [ ] Architecture docs and changelog updated
- [ ] Completed `/prime` → `/plan` → `/implement` → `/code-review` → `/code-review-fix`

**Quick reflection:** This was a refactor — no new functionality, just better structure. Was the agent workflow overkill for this, or did it catch things you would have missed? Would you use `/code-review` on refactors in your own projects?

**Next: [Exercise 3.5 — Free feature](exercise-3.5.md).** Start another **new chat session**.
