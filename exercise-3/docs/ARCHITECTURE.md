# Architecture (Exercise 3 catalog)

> **1–2 pages max.** Data flow and boundaries. When to touch which doc: [`DOC_INDEX.md`](DOC_INDEX.md).

## Context

Workshop **product catalog**: **FastAPI** backend (`uv`, Python 3.12), **React** frontend (`bun`). **No real database** — in-memory list seeded at import time. Exercise **3.1** adds **listing filters** (price, category, stock, search) aligned with **`tests/test_products_filtering.py`**; **3.4** introduces a **repository** seam without changing HTTP contracts.

## Runtime & entrypoints

| Surface | How it starts | Default URL |
| ------- | ------------- | ----------- |
| Backend | `python run_api.py` (or `uv run …`) from **`app/backend/`** | `http://localhost:8000` |
| Frontend | `bun dev` from **`app/frontend/`** | Vite dev server (client uses **`API_BASE_URL`** → **8000** in **`api-client.ts`**) |

**Cross-cutting:** **`app/main.py`** configures **lifespan** logging, optional **CORS**, registers **`products`** router, exposes **`GET /health`**. **`StructuredLogger`** (JSON) is used in API, service, and startup.

## Backend layers (current)

Thin **router → service → in-memory data** stack:

1. **`app/api/products.py`** — **HTTP only**: route **`GET /api/products`**, response model **`ProductListResponse`**, delegates to service. *(Today: no query parameters; **3.1** extends this with validated query params and passes filter criteria into the service.)*
2. **`app/services/product_service.py`** — **Business logic** home: **`get_all_products()`** reads module-level **`_PRODUCTS_DATABASE`**, initialized once from **`app.data.seed_products.get_seed_products()`**. *(After **3.1**: add functions or parameters that apply filter rules here—or document if any rule moves to a future repository.)*
3. **`app/data/seed_products.py`** — **Seed-only**: builds the canonical list of **`Product`** instances (30 rows, five categories).
4. **`app/models/`** — **Pydantic** API/domain models: **`Product`**, **`ProductListResponse`**, shared **`ProductCategory`**; errors in **`error.py`** as needed by routes.

**`app/core/`** — **Configuration and logging**, not product domain.

## Frontend structure

- **`App.tsx`** owns **data fetching** and **UI state** (loading, error, product list): calls **`fetchProducts()`** on mount/retry, renders **`ProductGrid`**.
- **`lib/api-client.ts`** is the **single place** for backend **`fetch`** calls and **`ApiError`** handling; keeps **`ProductListResponse`** typing aligned with the API.
- **`components/`** — Presentational pieces (**`ProductCard`**, **`ProductGrid`**) and **`ui/`** primitives.
- **`types/`** — TypeScript mirrors of API payloads.

*(After **3.1**, filter controls live in React state and should append query parameters to the same **`GET /api/products`** contract the tests expect.)*

## Data flow (happy path)

**Today (unfiltered list):**

1. User opens app → **`App`** calls **`fetchProducts()`** → **`GET /api/products`**.
2. Router → **`product_service.get_all_products()`** → returns full **`_PRODUCTS_DATABASE`** → **`ProductListResponse`**.
3. Frontend parses JSON → **`ProductGrid`** renders cards.

**Target after 3.1:**

1. User changes filters → client builds **`GET /api/products?...`** (see filtering tests for parameter names).
2. API validates query params → service applies rules on the in-memory list → filtered **`ProductListResponse`**.
3. UI re-renders grid.

## Boundaries & evolution

| Milestone | Change |
| --------- | ------ |
| **3.1** | Query params on **`products`** router; filtering logic in **service** (recommended); optional validation helpers in **`models`**; frontend **`api-client`** + **`App`** pass filters. |
| **3.4** | Introduce **`ProductRepository`** protocol + **`InMemoryProductRepository`**; **service** depends on repository for **loading/listing** raw data; **filtering** stays in service unless you explicitly document otherwise in this file. |

**Single sentence (fill after 3.4):** *The repository ends at …; the service begins at …* (e.g. repository returns iterables / loads by id; service applies catalog business rules and builds API-facing lists).

## Testing stance

- **`test_products_basic.py`** — green on baseline behavior.
- **`test_products_filtering.py`** — defines the **public contract** for filters; stubs are **skipped** until implementation lands. Architecture should not contradict those URLs and parameter names.
