# Exercise 4: `/prime` command (context loading)

**Pattern:** Context loading (Pattern 1)

**Difficulty:** Beginner–intermediate

**Goal:** Build a **`/prime`** command that loads **codebase context** into the agent before planning or implementation (Pattern 1: output optimized for **you**). The agent gathers facts (layout, rules, tooling, repo state) and produces a **short report**—optimized for scanning, not for editing files.

**Intent of `prime`:** *Context retrieval only.* No changes to production code, global rules, or protected config during the command unless you explicitly scope otherwise later.

---

## What's in this folder

```
exercise-4/
├── README.md              # This file
├── prime.example.md       # Reference: detailed command shape (adapt paths to your repo)
└── example-solution/      # Optional — facilitators / self-check
    ├── README.md
    └── SOLUTION.md
```

**Designing the plan document** for a future executor agent (what used to be a separate “4.2”) is now **part of exercise 5** together with the `/plan-feature` command.

---

## Why this exists

Without priming, every new session starts “cold”: the model guesses structure, misses your enforcement stack, or contradicts `AGENTS.md`. A good **`/prime`** fixes that by making the agent **read the real sources** (docs, config, git) and **summarize** what matters for the work ahead.

**Prefer doing this exercise in a codebase you actually use** (your app, your team repo, or a side project). The workshop demo app is fine if you have nothing else, but the command is most valuable when paths and tooling are *yours*.

---

## Prerequisites

- [ ] You are comfortable with **input → process → output** for commands.  
- [ ] You have a **real project** to point at (recommended).  
- [ ] You can add command files (e.g. `commands/` in the repo or your tool’s equivalent).

---

## Your task

1. **Name and location** — Implement a command called **`prime`** (e.g. `commands/prime.md` or your tool’s equivalent so you can run `/prime`).
2. **Contract** — State clearly:
   - **Context-only:** gather information; do not modify production code or shared rules during `/prime`.
   - **What to read** — Which files/commands define layout, governance (`AGENTS.md`, rules), and quality gates (linters, tests, structure checks).
   - **What to output** — A structured report (headings + bullets) you can skim in under a minute.
3. **Adapt paths** — Copy the *idea*, not someone else’s folder names. Your repo might be single-package, monorepo, or frontend-only; your command should list **your** READMEs, configs, and scripts.

---

## Design checklist

Answer these before you write the command body:

| Question | Why it matters |
|----------|----------------|
| What defines “where things live”? | `git ls-files`, top-level dirs, `README`s |
| What defines “how we work”? | `AGENTS.md`, rule indexes, CONTRIBUTING |
| What can fail independently? | Lint, types, tests, structure—often not one “green” |
| What is the current situation? | `git status`, recent `git log` |
| What should the human see first? | Order sections so risks and ambiguities surface |

---

## Reference example (one real shape)

This folder includes **`prime.example.md`**: a **detailed command shape** with generic steps (discover manifests, governance, enforcement, git state).

- Use it for **structure and tone**; in **your** repo, replace paths with what you actually have.
- Smaller projects can use a shorter command; the non‑negotiable part is **faithfulness to your repo**, not length.

Open: [`prime.example.md`](prime.example.md)

---

## Suggested command skeleton

Use something like this and fill in **your** paths and tools:

```markdown
---
description: Prime agent with codebase understanding (context retrieval only)
---

# Prime (`/prime`)

> Context-only: gather information. Do not edit production code or project rules unless the user explicitly asks outside this command.

## Objective

[What mental model should exist after prime? e.g. layout + governance + enforcement + repo state]

## Process

1. **Layout & docs** — [git listing, key READMEs, architecture docs]
2. **Governance** — [AGENTS.md, rules, conventions]
3. **Enforcement** — [what checks exist; they may fail independently]
4. **Repo state** — [branch, status, recent commits; optional: in-flight plans]
5. **Optional focus** — [if the user named a topic, narrow reads; still no edits]

## Output report

[Headings you want: overview, architecture, enforcement, current state, risks/ambiguities]
```

---

## Testing

1. Run **`/prime`** in a **fresh** context (or after clearing irrelevant chat).
2. Confirm the output mentions **real paths** from your repo and **does not** claim edits were made.
3. Ask a follow-up that depends on that context (e.g. “Where should a new API route go?”) and check the answer matches what `prime` surfaced.

---

## Success criteria

- [ ] You can invoke **`/prime`** in seconds.
- [ ] Output is **scannable** (headings, bullets, no essay unless you want it).
- [ ] The agent’s later answers **align** with your actual layout and rules.
- [ ] **Context-only** behavior is explicit (no surprise file edits during prime).

---

## What you learned

**Pattern 1: context loading** — Input is your repo; process is targeted reading; output is for **you** (human) to verify the model “sees” the same system you do.

---

## Next step

Continue with **exercise 5**: design the **plan document shape** an executor agent needs (Pattern 2), then build your **`/plan-feature`** command that researches and fills it.

---

## Facilitator note

Reference write-ups live under **`example-solution/`**. Participants can ignore that folder during the exercise.
