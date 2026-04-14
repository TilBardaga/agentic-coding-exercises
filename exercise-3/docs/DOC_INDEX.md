# Exercise 3 — documentation index

Single-screen **hub** for navigation docs and where to record changes. Normative “when to update” lives in the table below; commands **`/prime`**, **`/plan`**, and **`/implement`** point here when scope includes **Exercise 3**.

## Quick links

| Topic | Path |
| ----- | ---- |
| **Codebase map** (where things live) | [`CODEBASE_MAP.md`](CODEBASE_MAP.md) |
| **Architecture** (flow + boundaries) | [`ARCHITECTURE.md`](ARCHITECTURE.md) |
| **Changelog** (what shipped) | [`../CHANGELOG.md`](../CHANGELOG.md) |
| **Agent commands** (workshop) | [`.cursor/commands/`](../../.cursor/commands/) (from repo root: `agentic-coding-exercises/.cursor/commands/`) |
| **Job artifacts** (`dev-plan.md`, reviews) | [`docs/agent-jobs/`](../../docs/agent-jobs/README.md) |

## When to update (lightweight SSOT)

| Artifact | Update when… |
| -------- | -------------- |
| **`CODEBASE_MAP.md`** | You add or move **meaningful** paths (packages, routers, client, tasks) under `exercise-3/`. |
| **`ARCHITECTURE.md`** | Data flow or **layer boundaries** change (e.g. repository vs service after **3.4**). |
| **`CHANGELOG.md`** (root) | You complete a **learner-visible** slice (feature, refactor, fix) — at least **[Unreleased]** bullets. |
| **`DOC_INDEX.md`** | You add a **new** global navigation doc or change hub structure (rare). |
| **Optional `README.md`** next to a new module | **3.4+** introduces a distinct boundary (e.g. repository package) and facilitators want a one-screen card. |

**Plans:** When using **`/plan`**, add **`Doc:`** lines to the **Implementation checklist** in `dev-plan.md` for each row you touch here. **`/implement`** completes those in the **same** change set as code.
