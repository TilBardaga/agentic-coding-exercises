# Agentic Coding Workshop — exercises

This repository contains **hands-on exercises** for working systematically with AI coding assistants: baseline workflow, structured PIV, then a **single long-form track** with **commands, reviews, meta, and a capstone** on the same demo app. Each **`exercise-*`** folder has its own **`README.md`**.

**First:** install required tools using [`setup/README.md`](setup/README.md).

### Layer 1 rules (Cursor)

Stable, repo-wide agent guidance: **[`AGENTS.md`](AGENTS.md)** (constitution) and **[`.agents/rules/`](.agents/rules/INDEX.mdc)** (numbered workshop rules + routing index). Scoped rules apply when you edit files under **`exercise-*/app/backend/`** or **`exercise-*/app/frontend/`**.

### Agent commands (ready to use)

This repo includes **`.agents/`** command definitions (core PIV + optional validation workflows): **`/prime`**, **`/plan`**, **`/implement`**, plus **`/finish`** (commit) and **`/push`** (publish). **Exercise 3** does **not** require **`/finish`** or **`/push`**—see **[`exercise-3/README.md`](exercise-3/README.md)** § *Suggested agent workflow*. **Project health** (tests, lint, types—discovered from docs) lives in **`.agents/skills/check-project-health/SKILL.md`** and is run from **`/plan`** / **`/implement`** / **`/finish`** as described there—see [`.agents/README.md`](.agents/README.md).

|                   |                                                                                                                                                  |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Command files** | [`.agents/commands/`](.agents/commands/) (see [`.agents/README.md`](.agents/README.md))                                                          |
| **Job artifacts** | [`docs/agent-jobs/<job-name>/`](docs/agent-jobs/README.md) — `dev-plan.md`, optional `execution-report.md`, `code-review.md`, `system-review.md` |

`/plan` writes **`dev-plan.md`** under `docs/agent-jobs/`. Exercise **3** may introduce **optional** navigation docs under **`exercise-3/docs/`** (hub **`DOC_INDEX.md`**, map, architecture) and **`exercise-3/CHANGELOG.md`** as part of §3.3—plans should only **require** files that exist or that you create in the same job. **`/implement`** reads **`dev-plan.md`**, follows phased **Gates**, and updates the checklist in place (including **`Doc:`** items when listed).

---

## What you learn (overview)

### 1 — Baseline (`exercise-1/`)

- **Measure before you optimize:** build the full-stack **product catalog filtering** task the way you normally would with AI.
- **Reflect:** time, effort, confidence, and sense of control — capturing your **starting point**.

### 2 — PIV loop (`exercise-2/`)

- **Plan → Implement → Validate** on the **same** feature; instructions in **[`exercise-2/tasks/exercise-2.md`](exercise-2/tasks/exercise-2.md)**, code in **`exercise-2/app/`**.
- **Feel the difference:** more steering, richer context, and clearer expectations versus your baseline.

### 3 — Commands, reviews, meta, capstone (`exercise-3/`)

One **long-form** exercise on the **same** catalog app (**`exercise-3/app/`**), using **committed** definitions under **`.agents/commands/`**:

| Part | Focus |
| ---- | ----- |
| **3.1** | `/prime` → `/plan` → `/implement` for filtering |
| **3.2** | `/code-review` → `/code-review-fix` |
| **3.3** | `/execution-report` → `/system-review`, bounded Layer 1 edits, **Exercise 3** navigation docs (`exercise-3/docs/` + root **`CHANGELOG.md`**) |
| **3.4** | Backend **repository** abstraction (after filtering works) |
| **3.5** | Small **free-form** feature + validation |

Workflow steps: **[`exercise-3/tasks/exercise-3.1.md`](exercise-3/tasks/exercise-3.1.md)** … **[`exercise-3.5.md`](exercise-3/tasks/exercise-3.5.md)**. Index: **[`exercise-3/README.md`](exercise-3/README.md)**.

---

## Suggested order

```
1 → 2 → 3  (3.1 → 3.2 → 3.3 → 3.4 → 3.5)
```

---

## Repository layout (short)

| Path | Contents |
| ---- | -------- |
| [`AGENTS.md`](AGENTS.md) | Thin agent constitution; points to **`.agents/rules/`** |
| [`.agents/rules/`](.agents/rules/INDEX.mdc) | Workshop rule index + numbered `*-workshop-*.mdc` files |
| [`setup/`](setup/) | Installation (Python, uv, bun, etc.) |
| [`.agents/`](.agents/) | Agent command library ([`README`](.agents/README.md)) |
| [`docs/agent-jobs/`](docs/agent-jobs/) | Output for `/plan` → **`dev-plan.md`** per job |
| [`exercise-1/`](exercise-1/) | Baseline; assignment **[`tasks/exercise-1.md`](exercise-1/tasks/exercise-1.md)** |
| [`exercise-2/`](exercise-2/) | PIV on the same feature; assignment **[`tasks/exercise-2.md`](exercise-2/tasks/exercise-2.md)** |
| [`exercise-3/`](exercise-3/) | Command track: [`tasks/exercise-3.1.md`](exercise-3/tasks/exercise-3.1.md) … [`exercise-3.5.md`](exercise-3/tasks/exercise-3.5.md) |

---

## Demo app (exercises 1–3)

**Stack:** FastAPI / **uv** (backend), **bun** + React (frontend). Start commands are in each exercise’s **`README.md`**; scope your assistant to that exercise’s **`app/`** folder.

---

_Work through exercises in order, and use the reflection prompts in each README to learn deliberately from your own workflow._
