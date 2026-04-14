---
description: Prime agent with codebase understanding (context retrieval only)
argument-hint: "[optional focus — e.g. user detail page, checkout API]"
---

# Prime (`/prime`)

> **Context-only:** gather information. Do **not** modify production code, project rules, or tooling config during this workflow unless the user explicitly asks for a change.

## Input: `$ARGUMENTS` (optional)

- **Empty or omitted:** **Broad prime** — light scan of the whole repo (layout, docs, tooling, rules, git).
- **Non-empty:** **Directional prime** — treat the text as a **focus topic** (feature, screen, module, path fragment, or concept). Spend most of your exploration **in that direction**: search, open relevant files, and summarize how that slice fits the repo. Still record git history and minimal global anchors (root `README`, `AGENTS.md`) so nothing important is invisible.

If the topic is ambiguous, state your interpretation and what you searched; still **no edits**.

## Objective

Build a **short, scannable** picture of this repository—global or **focused**—plus **recent history with full commit messages**, so the next step (`/plan`, `/implement`, or ad-hoc work) aligns with **this** tree.

## Process

### 1. Repository layout

**Broad prime**

- List tracked files (e.g. `git ls-files`; on huge repos, cap output sensibly).
- Summarize top-level folders and what they are for (infer from names + READMEs).
- Note where the “working” app or exercise code lives (e.g. `exercise-*/app/`, `src/`, `apps/*`) **from what actually exists**, not from assumptions.

**Directional prime** (`$ARGUMENTS` set)

- Infer likely paths from the topic (routes, feature folders, component names, API segments). Use search tools: filename glob, ripgrep on the user’s phrase and synonyms, imports/references.
- Read the **most relevant** files first (handlers, pages, hooks, tests next to the feature). Sketch how this slice connects to neighbors (one short paragraph).
- Only expand to a whole-repo file listing if the topic stays unclear after targeted search.

### 2. Discover documentation (if present)

**Do not require** specific files globally. **Look for** common entry points and read what you find:

- Root `README.md`, `AGENTS.md`, `CONTRIBUTING.md`, or similar.
- `setup/` or `docs/` (any index or overview files).
- README in the folder tied to the focus (directional) or the user’s current exercise (broad).
- **Exercise 3 (example):** when scope includes **`exercise-3/`**, prefer **`exercise-3/docs/DOC_INDEX.md`** for a one-screen hub (map, architecture, changelog path, agent jobs)—still skip if missing.

If a file is missing, say so briefly and continue—exercises may be minimal on purpose.

### 3. Tooling and commands

From config files that **exist** (e.g. `pyproject.toml`, `package.json`, `Makefile`, task runners)—prefer configs **in or above** the focused area when directional—extract:

- How to install deps and run the app or tests.
- Lint / typecheck / test commands **this repo** actually defines.

### 4. Rules and conventions

- If `AGENTS.md` (or other project rule files, e.g. under `.cursor/rules` if present) exists, note where Layer-1 guidance lives and one-line what it emphasizes.
- Otherwise: state that rules are chat-only or exercise-local.

### 5. Git history and working tree

Run these **every time** (broad or directional):

- **Last 10 commits with full messages:** use default **medium** format so **subject + full body** appear (do **not** use only `--oneline`). Example: `git log -10 --format=medium` (or plain `git log -10` with the same effect). Read the output; use it to infer recent themes and risky areas.
- **Working tree:** `git status -sb` (branch + clean/dirty).

**Directional (optional extra):** if some of those 10 commits clearly touch files under your focus paths, call that out when summarizing.

### 6. Directional deep dive (only when `$ARGUMENTS` is set)

- Prefer depth over breadth: tests, types, config, and entrypoints that mention the topic.
- If the user’s phrase does not match the codebase, report dead ends and the closest matches you found—still **no edits**.

**Optional:** if the task looks multi-session, glance for in-flight plan artifacts (e.g. `docs/agent-jobs/*/dev-plan.md` or `docs/jobs/` if your repo uses them).

## Output

Produce a **compact** summary (bullet lists, not an essay). Adjust emphasis:

**Always include**

- **Recent history** — in your own words: what the **last 10 commits** were about (you read **full** messages, not one-liners only). Note branch + dirty state.
- **How to run / validate** — concrete commands from this repo.
- **Rules location** — or “none found”.

**Broad prime also**

- **Layout** — what matters for typical work in this repo.
- **Suggested scope** — which directory the user should `@` or scope the agent to, if obvious.

**Directional prime also**

- **Focus** — restate `$ARGUMENTS` and what in the tree maps to it.
- **Findings** — key files, data flow, dependencies, open questions for `/plan`.
