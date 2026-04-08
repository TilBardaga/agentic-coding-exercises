---
description: Prime agent with codebase understanding (Context Retrieval Only)
---

# Prime: Load Project Context (`/prime`)

> [!NOTE]
> **Context-only mode:** Gather information only. Do not modify production code, rules, or protected config during `/prime`.

## Objective

Build a concise picture of **layout**, **governance**, **enforcement tooling**, and **repo state** so the next steps match **this** repository. **Resolve paths from the live tree** (`git ls-files`, directory listings)—do not assume a particular layout beyond what you verify.

## Process

### 1. Tracked layout and documentation

- **Inventory:** Run `git ls-files`. On huge repos, cap at the first **200** paths for the initial pass.
- **Root narrative:** Read **`README.md`** at the repository root.
- **Documentation hub:** Identify where long-form docs live:
  - List paths under **`docs/`** and **`documentation/`** from the inventory.
  - Read the **documentation index** in this **priority order**—stop at the **first file that exists**:  
    `docs/README.md` → `docs/DOC_INDEX.md` → `docs/index.md` → `docs/INDEX.md` → the first `*.md` directly under `docs/` whose title or first lines indicate it links to other documents.
  - **Attempt to read** **`CONTRIBUTING.md`** at the repo root; note **present** or **absent** in the report.
  - **Discover** architecture filenames from `git ls-files`: read **`ARCHITECTURE.md`** at root and any **`docs/architecture*.md`** matches.
- **Package manifests:** Collect **every** path to **`pyproject.toml`**, **`requirements*.txt`**, and **`package.json`** using `git ls-files` (or equivalent search). Read each file you found.
- **Source layout:** From the README and manifests, name the **actual** directories that hold application code, tests, and tooling—cite paths you saw in the inventory.

### 2. Governance

- **Attempt to read** **`AGENTS.md`** at the repository root. In the report, state **present** or **absent** explicitly.
- **Rule bundles:** Locate **`.cursor/rules/`** (or the project’s stated rules directory). Read the **routing entry** in this order: **`INDEX.mdc`** → **`README.md`** → the first file in that folder that lists other rule files.
- **Layer / ownership maps:** Search the tracked tree for **`CODEBASE_MAP.md`**, **`CODEOWNERS`**, and a rules **matrix** under `docs/`. Read every match. **In the report:** list files read, or **no dedicated map files found**.

### 3. Enforcement (independent failure modes)

- Extract scripts and checks from **each** `pyproject.toml`, **`package.json`**, and **`Makefile`** found in the inventory.
- **Read** every path returned by `git ls-files` for **`.github/workflows/`** and for **`.gitlab-ci.yml`** at the repository root.
- Build a **numbered list** of distinct checks: format, lint, typecheck, tests, structure, custom project scripts.
- State explicitly: **passing one step does not guarantee the others**—each line item can fail alone.
- Copy **verbatim** the documented commands for running checks (the strings in those config files).

### 4. Active project state

- Run **`git log -n 10`**; use full subject lines (avoid `--oneline` so scope stays visible).
- Run **`git status -sb`** for branch and working tree.
- **In-flight plans:** List tracked files under **`plans/`** and **`docs/jobs/`** via `git ls-files`. Summarize each **`plan.md`** (and similarly named planning files) in that list. **Report `none`** when **zero** paths match those prefixes.

### 5. User-directed focus

- **Topic from the prompt:** With a user-supplied focus (e.g. “authentication”), restrict reads to files and directories tied to that topic; still **no edits**.

---

## Output report

Use clear headings and bullets:

- **Project overview** — purpose, main stack (from README + manifests).
- **Architecture & boundaries** — directories, packages, how pieces connect (grounded in files you read).
- **Documentation** — where the doc hub lives and what the index points to.
- **Governance** — rules location (`AGENTS.md`, rule indexes) and how they are organized.
- **Enforcement** — separate checks and exact commands; what can fail independently.
- **Current state** — branch, `git status`, recent commits.
- **In-flight plans** — paths found under `plans/` / `docs/jobs/`, or **none**.
- **Risks / ambiguities** — gaps to close before `/plan` or `/implement`.

Keep the report scannable (short paragraphs, bullets).
