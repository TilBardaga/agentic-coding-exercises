# Exercise 4: `/prime` command (context loading)

**Goal:** Build a **`/prime`** command that loads **codebase context** into the agent before planning or implementation (Pattern 1: context loading — output optimized for **you**).

---

## Folder layout

```
exercise-4/
├── README.md                 # This file
├── exercise-4.1/             # `/prime` — codebase context command
│   ├── README.md             # Instructions
│   └── prime.example.md      # Reference: one fullstack-shaped example (adapt paths)
└── example-solution/         # Optional reference for facilitators / self-check
    ├── README.md
    └── exercise-4.1/SOLUTION.md
```

---

## Overview

**Exercise 4.1 — `/prime`**

Load **layout, governance, enforcement tooling, and repo state** into the agent. **Context retrieval only**—no edits to production code or shared rules during the command. Output is a **short, scannable report** for you.

**Best done in your own repo**; see `exercise-4.1/prime.example.md` for one rich reference shape.

**Designing the plan document** for a future executor agent (what used to be a separate “4.2”) is now **part of exercise 5** together with the `/plan-feature` command.

---

## Prerequisites

- [ ] You are comfortable with **input → process → output** for commands.  
- [ ] You have a **real project** to point at (recommended).  
- [ ] You can add command files (e.g. `commands/` in the repo or your tool’s equivalent).

---

## Order of work

1. Open **`exercise-4.1/README.md`** and build **`/prime`** (optionally skim **`prime.example.md`**).  
2. Run it and skim the output.  
3. Continue with **`exercise-5/README.md`** — plan output shape + planning command.

---

## What you get out of this

- Practice **Pattern 1**: prime the session with **real** repo context; tune the report for a **human**.

---

## Facilitator note

Reference write-ups live under **`example-solution/`**. Participants can ignore that folder during the exercise.
