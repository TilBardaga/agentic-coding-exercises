# Exercise 3.4 — Repository abstraction (backend)

**Prerequisite:** **[`exercise-3.1.md`](exercise-3.1.md)** and **[`exercise-3.2.md`](exercise-3.2.md)** are done: **filtering** works end-to-end. This step is a **refactor in place**—behavior and tests stay the same; structure improves.

**Command index:** [`../README.md`](../README.md).

**Assistant session:** **New chat** (do not continue the 3.1–3.3 thread). Run this refactor’s **full technical cycle** in this chat: **`/prime`** first, then **`/plan` → `/implement` → `/code-review` → `/code-review-fix`**. **`/execution-report`** and **`/system-review`** are **optional**; keep them in this same chat if you use them. **3.5** → **another new chat**. See **[`../README.md` § Chat / assistant sessions](../README.md#chat--assistant-sessions)**.

**Workshop workflow (this step):** Follow **[`../README.md` § Suggested agent workflow](../README.md#suggested-agent-workflow)**. For **3.4** you must run at least **`/prime` → `/plan` → `/implement` → `/code-review` → `/code-review-fix`**. **`/execution-report`** and **`/system-review`** are **optional** here (you already did a full retro in **3.3**); use them if you want another process pass on this refactor. **`/finish`** and **`/push`** are **out of scope** for this workshop repo.

---

## Why a repository layer?

Today, product data and filtering logic often share the same module: a **module-level list** holds data; the **service** reads and filters it directly. That is fine for a workshop seed, but it **couples** “how we fetch rows” to “what we do with products.”

A **repository** is the seam where **persistence** lives:

- **Service** = business rules (filtering, sorting, validation of domain invariants).
- **Repository** = how products are **loaded and stored** (in-memory list now; a database later).

Benefits you should be able to explain after this exercise:

- **Swap storage** (e.g. SQLite/Postgres) without rewriting filtering rules in the service.
- **Test the service** with a **fake or in-memory repository** instead of touching global state.
- **One place** that knows about `get_seed_products()` or any future connection string.

---

## What you build

### 1. `ProductRepository` (contract)

Define a **`typing.Protocol`** (preferred) or an **ABC** that describes what the **service** needs. After **3.1**, that is **not** only `get_all_products()`—it must include whatever the service uses for **filtered** access, for example:

- A method that returns products matching filter criteria (query object, separate args, or a small **criteria** model—match what you already have in `product_service` and the API).
- Names and signatures should mirror your **current** service API so the refactor is mostly **moving** code, not redesigning behavior.

Keep the protocol **narrow**: only methods the service actually calls.

### 2. `InMemoryProductRepository` (implementation)

- Holds the **in-memory** list (the data that today lives in `_PRODUCTS_DATABASE` or equivalent).
- **Single place** that calls **`get_seed_products()`** (or builds the initial list).
- Implements every method on **`ProductRepository`**.

No real database, no ORM, no async I/O in this exercise.

### 3. `product_service` (consumer)

- **No** direct reads of a global product list for “the catalog.”
- All data access goes through an instance of **`ProductRepository`** (passed in or resolved as below).
- **Filtering / sorting** logic can stay in the service **or** move into the repository—**pick one** approach and document it in [`docs/ARCHITECTURE.md`](../docs/ARCHITECTURE.md) (one short paragraph). Workshop default: **keep business rules in the service**, repository returns **raw or lightly filtered** lists **only** if you already structured it that way; otherwise repository = “list + load” and service keeps filter rules—**consistency beats dogma**.

### 4. Wiring (choose one pattern)

Document the choice in **`docs/ARCHITECTURE.md`**:

| Pattern                  | When it fits                                                                                                           |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------- |
| **Module-level default** | e.g. `_repo: ProductRepository = InMemoryProductRepository()` set once; functions use `_repo`. Simple for a small API. |
| **FastAPI `Depends()`**  | Inject a repository provider into the router or a service factory; easier to swap in tests via dependency overrides.   |

Either is valid; **do not** leave multiple hidden globals for the same data.

### 5. API layer

**Routers** should stay thin: they already delegate to **`product_service`**. After the refactor, they must **not** import the repository directly unless you chose **Depends** at the router—then only wiring lives there.

---

## Suggested migration order

1. **Prime** — refresh layout under `app/backend` (where service, data, API live).
2. **Plan** — new job folder under `docs/agent-jobs/` (e.g. `repo-abstraction-ex3`); phases: introduce protocol → implement in-memory → rewire service → run tests.
3. **Implement** — tick the plan; keep **pytest** green after each meaningful chunk.
4. **Code review** + **code review fix** — same job folder as this refactor’s plan/artifacts (or the folder your facilitator specifies).
5. **(Optional)** **Execution report** + **system review** — if you want to practice the meta loop again on this change set.

---

## Testing and validation

- **`uv run pytest`** for **`app/backend`** — **all** tests, including filtering tests, must pass.
- Optionally add **one** test that uses a **fake** repository (not required).
- Run **[`check-project-health`](../../.agents/skills/check-project-health/SKILL.md)** (or `ruff` + `pytest`) on the backend root you changed.

---

## Docs

- **[`docs/ARCHITECTURE.md`](../docs/ARCHITECTURE.md):** repository + service boundary; wiring pattern (`Depends` vs module).
- **[`docs/CODEBASE_MAP.md`](../docs/CODEBASE_MAP.md):** file path(s) for `ProductRepository` / `InMemoryProductRepository`.
- **[`CHANGELOG.md`](../CHANGELOG.md):** short entry under **[Unreleased]** for this refactor.

---

## Out of scope

- Real SQL/ORM, migrations, connection pools.
- Async database drivers, full DDD, event sourcing.
- Changing **HTTP** contracts or **frontend** behavior (unless a tiny fix is required for green tests).

---

## Done when

- [ ] **`ProductRepository`** + **`InMemoryProductRepository`** exist; **service** has **no** ad hoc global list access for catalog data.
- [ ] **`uv run pytest`** passes for **`exercise-3/app/backend`**.
- [ ] **Architecture** (and map or changelog) updated.
- [ ] You completed at least **`/prime` → `/plan` → `/implement` → `/code-review` → `/code-review-fix`** for this work.

---

## Next

**[`exercise-3.5.md`](exercise-3.5.md)** (free feature).
