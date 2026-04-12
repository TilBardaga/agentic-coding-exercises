# CODEBASE_MAP (Exercise 3)

> Keep updated as you change **`app/`** or add docs. One-screen overview; deeper narrative: [`ARCHITECTURE.md`](ARCHITECTURE.md). Hub: [`DOC_INDEX.md`](DOC_INDEX.md).

## Purpose

Where **code and workshop files** live under `exercise-3/`.

## Top-level layout

| Area | Path | Role |
| ---- | ---- | ---- |
| Demo app (backend) | `app/backend/` | FastAPI + uv; run via `run_api.py` |
| Demo app (frontend) | `app/frontend/` | React + bun/vite; UI + API client |
| Assignment steps | `tasks/exercise-3.1.md` … `exercise-3.5.md` | 3.1 = catalog + filters; 3.2–3.5 = review, meta, repo, capstone |
| Navigation docs | `docs/` | This file, architecture, doc index |
| Release notes | `../CHANGELOG.md` | Learner-visible changes (exercise root) |

## Backend (`app/backend/`)

| Path | Notes |
| ---- | ----- |
| `run_api.py` | Dev entrypoint (starts uvicorn; port aligns with frontend client default **8000**). |
| `app/main.py` | FastAPI app: lifespan logging, optional CORS, **`/health`**, mounts **`products`** router. |
| `app/api/products.py` | **`APIRouter`** prefix **`/api/products`**. **`GET ""`** → `product_service.get_all_products()` → **`ProductListResponse`**. *(Filtering query params are the **3.1** target; see `tests/test_products_filtering.py`.)* |
| `app/services/product_service.py` | Service layer: in-memory **`_PRODUCTS_DATABASE`** seeded once from **`get_seed_products()`**; **`get_all_products()`**. |
| `app/data/seed_products.py` | **`get_seed_products()`** — 30 sample **`Product`** rows (five categories). |
| `app/models/product.py` | **`Product`**, **`ProductListResponse`**, **`ProductCategory`** literal. |
| `app/models/error.py` | **`ErrorResponse`** (and related) for consistent JSON errors—wire into routes when returning **4xx** (e.g. invalid filter range in **3.1**). |
| `app/core/config.py` | Settings (app name, version, log level, CORS flag). |
| `app/core/logging_config.py` | Structured JSON logging (**`StructuredLogger`**). |
| `tests/conftest.py` | **`TestClient`** fixture for API tests. |
| `tests/test_products_basic.py` | Baseline API tests (unskipped). |
| `tests/test_products_filtering.py` | Filtering contract tests (**stub / skipped** until **3.1** implements query params + service rules). |

## Frontend (`app/frontend/src/`)

| Path | Notes |
| ---- | ----- |
| `App.tsx` | Root UI: load catalog via **`fetchProducts()`**, loading/error state, **`ProductGrid`**. |
| `components/ProductGrid.tsx` | Grid layout; uses **`ProductCard`**. |
| `components/ProductCard.tsx` | Single product presentation. |
| `components/ui/*` | Shared UI primitives (button, card, form, input, label, select). |
| `lib/api-client.ts` | **`fetchProducts()`** (`GET /api/products`), **`checkHealth()`** (`GET /health`); **`API_BASE_URL`** default `http://localhost:8000`. |
| `lib/logger.ts` | Frontend structured logging helper. |
| `lib/utils.ts` | Small shared helpers (e.g. `cn`). |
| `types/product.ts` | Mirrors **`ProductListResponse`** / product fields for TypeScript. |
| `types/error.ts` | **`ApiError`**, backend error payload typing. |
| `APITester.tsx` | Optional/dev API probing UI (if used in your build). |
| `index.tsx` / `frontend.tsx` | Entry/bootstrap (per project setup). |

## Integration points

- **HTTP:** Browser → **`GET /api/products`** (and after **3.1**, **`?min_price_usd=`** etc. per tests) → JSON **`ProductListResponse`**.
- **Health:** **`GET /health`** — used by **`checkHealth()`** in **`api-client.ts`**.
- **After § 3.4:** Add rows here for **`ProductRepository`** / **`InMemoryProductRepository`** and update [`ARCHITECTURE.md`](ARCHITECTURE.md) for service vs repository boundary.

## Facilitator note

Learners should **sync this map** when they add modules (e.g. repository package) or move endpoints; **`ARCHITECTURE.md`** should describe *why* layers exist, this file *where* they are.
