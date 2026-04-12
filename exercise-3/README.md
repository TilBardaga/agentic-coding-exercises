# Exercise 3 — Commands, reviews, meta, capstone

Long-form track: **same catalog filtering assignment** as Exercises 1–2, now with **`.agents/commands/`** (prime, plan, implement, reviews, health). Work in **`exercise-3/app/`**; **@** command files from [`.agents/commands/`](../../.agents/commands/).

**Setup:** [`../setup/README.md`](../setup/README.md).

## Quick start

From **`exercise-3/`**:

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

Scope assistants to **`exercise-3/app/`** for code; use **repo root** for **`docs/agent-jobs/`** and **`.agents/`**.

---

## Suggested agent workflow

The **3.1** feature ships after **3.2** (code review + fix). For **each** substantive change (especially the **3.1+3.2** chain, **3.4**, **3.5**), the **default** sequence is:

1. **`/prime`** — context on the repo slice you will touch ([`commands/prime.md`](../../.agents/commands/prime.md)).
2. **`/plan`** — write **`dev-plan.md`** under **`docs/agent-jobs/<job>/`** ([`commands/plan.md`](../../.agents/commands/plan.md)).
3. **`/implement`** — execute the plan ([`commands/implement.md`](../../.agents/commands/implement.md)).
4. **`/code-review`** — technical review of the change ([`commands/code-review.md`](../../.agents/commands/code-review.md)).
5. **`/code-review-fix`** — address findings ([`commands/code-review-fix.md`](../../.agents/commands/code-review-fix.md)).

**After that**, for a **full** learning cycle (required in **3.3**, optional for **3.4** / **3.5** unless you want extra practice):

6. **`/execution-report`** — plan vs what happened ([`commands/execution-report.md`](../../.agents/commands/execution-report.md)).
7. **`/system-review`** — process and bounded updates to rules/templates ([`commands/system-review.md`](../../.agents/commands/system-review.md)).

**Out of scope in this workshop repo:** **`/finish`** (commit) and **`/push`** are **not** part of the assignment; facilitators may mention them for **your own** projects later.

Step files **3.1–3.5** spell out which of the above apply to that segment.

### Chat / assistant sessions

How you **group steps in Cursor** (or any assistant) matters for context:

| Segment       | Chat                                                                                                                                                                                                                                                                            |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **3.1 → 3.3** | **One** conversation. After **`/plan`** and **`/implement`** in **3.1**, keep going in the **same chat** for **3.2** (`/code-review`, `/code-review-fix`) and **3.3** (`/execution-report`, `/system-review`). The assistant keeps the plan, code, and review history together. |
| **3.4**       | **New chat.** **Start with `/prime`** on the backend area you will refactor, then **`/plan` → `/implement` → `/code-review` → `/code-review-fix`**. **`/execution-report`** and **`/system-review`** are optional here; if you run them, still in **this** chat.                |
| **3.5**       | **New chat again.** Run the **full** suggested technical cycle from **`/prime`** through **`/code-review-fix`** in that single conversation; optional meta steps also stay in that chat.                                                                                        |

If a session gets too long, your facilitator may allow a handover—otherwise prefer the splits above.

---

## Command definitions

| Workflow              | File                                                                                                 |
| --------------------- | ---------------------------------------------------------------------------------------------------- |
| Context               | [`.agents/commands/prime.md`](../../.agents/commands/prime.md)                                       |
| Planning              | [`.agents/commands/plan.md`](../../.agents/commands/plan.md)                                         |
| Implement             | [`.agents/commands/implement.md`](../../.agents/commands/implement.md)                               |
| Code review           | [`.agents/commands/code-review.md`](../../.agents/commands/code-review.md)                           |
| Fix after review      | [`.agents/commands/code-review-fix.md`](../../.agents/commands/code-review-fix.md)                   |
| Execution retro       | [`.agents/commands/execution-report.md`](../../.agents/commands/execution-report.md)                 |
| Process / rules retro | [`.agents/commands/system-review.md`](../../.agents/commands/system-review.md)                       |
| Health checks         | [`.agents/skills/check-project-health/SKILL.md`](../../.agents/skills/check-project-health/SKILL.md) |

Job artifacts: **`docs/agent-jobs/<job-name>/`** — see [`../docs/agent-jobs/README.md`](../docs/agent-jobs/README.md).

---

## Workflow steps (do in order)

| Step    | Assignment                                                                                              |
| ------- | ------------------------------------------------------------------------------------------------------- |
| **3.1** | **[`tasks/exercise-3.1.md`](tasks/exercise-3.1.md)** — prime, plan, implement; full catalog spec inside |
| **3.2** | **[`tasks/exercise-3.2.md`](tasks/exercise-3.2.md)** — code review + fix                                |
| **3.3** | **[`tasks/exercise-3.3.md`](tasks/exercise-3.3.md)** — execution report, system review, docs            |
| **3.4** | **[`tasks/exercise-3.4.md`](tasks/exercise-3.4.md)** — repository abstraction                           |
| **3.5** | **[`tasks/exercise-3.5.md`](tasks/exercise-3.5.md)** — free feature                                     |

**Navigation docs (3.3+):** start at [`docs/DOC_INDEX.md`](docs/DOC_INDEX.md) — [`docs/CODEBASE_MAP.md`](docs/CODEBASE_MAP.md), [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md), [`CHANGELOG.md`](CHANGELOG.md) (exercise root).

---

## Layout

```
exercise-3/
├── README.md
├── CHANGELOG.md
├── tasks/
│   ├── exercise-3.1.md … exercise-3.5.md
├── docs/
└── app/
```
