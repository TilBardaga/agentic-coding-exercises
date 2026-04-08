# Agentic Coding Workshop — exercises

This repository contains **hands-on exercises** for working systematically with AI coding assistants: from measuring your current workflow, through planning, commands, project rules, and reviews. Each `exercise-*` folder has its own `README.md` with the assignment and details.

**Workshop slides (Dyflexis):** [https://dyflexis-workshop.vercel.app/dyflexis](https://dyflexis-workshop.vercel.app/dyflexis)

**First:** install required tools using [`setup/README.md`](setup/README.md).

---

## What you learn (overview)

### 1 — Baseline (`exercise-1/`)

- **Measure before you optimize:** build the same full-stack task (product catalog) the way you normally would with AI.
- **Reflect:** time, effort, confidence, and sense of control — not pass/fail, but capturing your **starting point**.

### 2 — PIV loop (`exercise-2/`)

- **Plan → Implement → Validate** on the same feature as in exercise 1.
- **Feel the difference:** more steering, richer context, and clearer expectations versus your baseline.

### 3 — Project rules (`exercise-3/`)

- Split an overloaded **`AGENTS.md`** into what should **always** load versus **on-demand** (two-question framework: constant vs task-specific; every session vs sometimes).
- Sharpen **Layer 1:** stable knowledge for the whole project, without noise.

### 4 — `/prime` command (`exercise-4/`)

- Load **codebase** context (layout, rules, tooling, git state); **context-only**; output aimed at **you** (short, scannable).

### 5 — Plan shape + planning command (`exercise-5/`)

- **Part A:** design the **plan document** an executor agent needs (explicit steps, files, validation)—Pattern 2.  
- **Part B:** build **`/plan-feature`** (or equivalent): **research + template filling** in one reusable command.

### 6 — Execute command (`exercise-6/`)

- Build **`/execute`**: read a **plan file on disk**, implement **task-by-task**, run the plan’s **validation commands**, report what changed. Closes the gap between **planning** and **shipping**.

### 7 — Review commands (`exercise-7/`)

Exercise 7 has two parts (**7.1** and **7.2**), grouped under one folder so numbering stays aligned with exercises 1–6:

- **7.1 — Code review:** a `/code-review`-style command that reviews **changed code** for bugs, security, and quality, aligned with `AGENTS.md` and project patterns.
- **7.2 — System review:** after an **execution report** (plan vs what happened), a command that improves **process**: classify divergences, root causes, and updates to Layer 1 and templates.

Both live under [`exercise-7/`](exercise-7/): [`exercise-7.1/`](exercise-7/exercise-7.1/) and [`exercise-7.2/`](exercise-7/exercise-7.2/).

---

## Suggested order

For a full **PIV-style command chain**: do **exercise 6** (execute) **after** exercise 5 (plan) and **before** exercise 7 (reviews).

```
1 → 2 → 3 → 4 → 5 → 6 → 7 (7.1, then 7.2)
```

The order above matches **prime → plan → execute → review**.

You can swap 7.1 and 7.2 if you only care about process; the natural story is technical code review first, then system review.

---

## Repository layout (short)

| Path | Contents |
|------|----------|
| [`setup/`](setup/) | Installation (Python, uv, etc.) |
| [`exercise-1/`](exercise-1/) … [`exercise-6/`](exercise-6/) | Numbered exercises; often includes `app/` for the demo where relevant |
| [`exercise-7/`](exercise-7/) | Review exercises: [`exercise-7.1/`](exercise-7/exercise-7.1/), [`exercise-7.2/`](exercise-7/exercise-7.2/) |

---

## Demo app (exercises 1 and 2)

Stack and start commands are in the READMEs for **exercise 1** and **exercise 2** (FastAPI/uv backend, Bun frontend). Scope your assistant to that exercise’s `app/` folder.

---

*Work through exercises in order, and use the reflection prompts in each README to learn deliberately from your own workflow.*
