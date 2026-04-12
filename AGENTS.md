# Agent Constitution & Operating Procedures

## 0. Core operating environment

- Assume training knowledge may be outdated; prefer current library and tool documentation when behavior matters.
- On **Windows / PowerShell**, favor PowerShell-native or cross-platform commands over Unix-only assumptions.

## 1. The AI Brain (Rules SSOT)

Normative coding and architecture guidance lives in **`.agents/rules/`** — not duplicated here.

- **Mission control:** **[`README.md`](README.md)** — exercise order (**1 → 2 → 3**), layout, and where assignments live. For **Exercise 3** navigation docs, use **[`exercise-3/docs/DOC_INDEX.md`](exercise-3/docs/DOC_INDEX.md)**; learner-visible shipping notes go in **[`exercise-3/CHANGELOG.md`](exercise-3/CHANGELOG.md)**.
- **The Map:** **[`.agents/rules/INDEX.mdc`](.agents/rules/INDEX.mdc)** — which numbered rule file to open (**routing only**; the index is not the full rule text).
- **The Laws:** **`01`–`06`** `*-workshop-*.mdc` in **`.agents/rules/`** — backend/frontend exercise apps (**`01`–`05`**) and **Exercise 3** documentation discipline (**`06`**). Maintainer expectations: **[`.agents/rules/README.md`](.agents/rules/README.md)**.
- **Repo shape:** Demo apps under **`exercise-*/app/backend/`** (FastAPI, **uv**) and **`exercise-*/app/frontend/`** (Bun, React). This **public** tree is the **1 → 2 → 3** learner path only.

## 2. Project governance & session memory

- **Agent commands:** **[`.agents/`](.agents/)** — `/prime`, `/plan`, `/implement`, `/finish`, `/push`, reviews. Overview: **[`.agents/README.md`](.agents/README.md)**.
- **Implementation plans:** **`/plan`** writes **`docs/agent-jobs/<job>/dev-plan.md`** only — **[`docs/agent-jobs/README.md`](docs/agent-jobs/README.md)**.

## 3. Planning discipline (workshop)

Use **`/plan`** and an approved **`dev-plan.md`** before **substantive**, multi-file work on an exercise **app**; quick doc or typo fixes do not require a plan. When scope includes **Exercise 3**, plans should list **`Doc:`** checklist items for artifacts described in **`exercise-3/docs/DOC_INDEX.md`**.

## 4. Operational excellence

After meaningful code changes, follow **`.agents/skills/check-project-health/SKILL.md`** (Implementation mode when executing a plan) to discover and run the right **`uv` / `pytest` / `ruff`** and **`bun`** checks for the app roots you touched — not a single global command from repo root.

**Tooling setup (new machine):** **[`setup/README.md`](setup/README.md)**.
