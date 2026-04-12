# Exercise 1 — Baseline

Establish your **baseline** workflow with AI on the catalog filtering feature. When you are done reflecting, continue with **Exercise 2** (PIV) in the next folder.

## Quick start

From **`exercise-1/`**:

**Backend**

```bash
cd app/backend
uv venv --python 3.12
uv sync
uv run python run_api.py
```

**Frontend**

```bash
cd app/frontend
bun install
bun dev
```

Install tools: [`../setup/README.md`](../setup/README.md).

## Assignment

**→ [`tasks/exercise-1.md`](tasks/exercise-1.md)** — baseline only; work in **`exercise-1/app/`**.

## Next

**→ [`../exercise-2/README.md`](../exercise-2/README.md)** — same feature with a structured **Plan → Implement → Validate** loop; assignment **[`../exercise-2/tasks/exercise-2.md`](../exercise-2/tasks/exercise-2.md)**.

## Project layout

```
exercise-1/
├── tasks/
│   └── exercise-1.md
└── app/
```
