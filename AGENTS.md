# Agent Constitution & Operating Procedures

## 0. Core operating environment

- Assume training knowledge may be outdated; prefer current library and tool documentation when behavior matters.
- On **Windows / PowerShell**, favor PowerShell-native or cross-platform commands over Unix-only assumptions.

## 1. The AI Brain (Rules SSOT)

Normative coding and architecture guidance lives in **`.cursor/rules/`** — not duplicated here.

- **Mission control:** **[`README.md`](README.md)** — exercise order (**1 → 2 → 3**), layout, and where assignments live. For **Exercise 3** navigation docs, use **[`exercise-3/docs/DOC_INDEX.md`](exercise-3/docs/DOC_INDEX.md)**; learner-visible shipping notes go in **[`exercise-3/CHANGELOG.md`](exercise-3/CHANGELOG.md)**.
- **The Map:** **[`.cursor/rules/INDEX.mdc`](.cursor/rules/INDEX.mdc)** — which numbered rule file to open (**routing only**; the index is not the full rule text).
- **The Laws:** **`01`–`06`** `*-workshop-*.mdc` in **`.cursor/rules/`** — backend/frontend exercise apps (**`01`–`05`**) and **Exercise 3** documentation discipline (**`06`**). Maintainer expectations: **[`.cursor/rules/README.md`](.cursor/rules/README.md)**.
- **Repo shape:** Demo apps under **`exercise-*/app/backend/`** (FastAPI, **uv**) and **`exercise-*/app/frontend/`** (Bun, React).

## 2. Project governance & session memory

- **Agent commands:** **[`.cursor/`](.cursor/)** — `/prime`, `/plan`, `/implement`, `/finish`, `/push`, reviews. Overview: **[`.cursor/README.md`](.cursor/README.md)**.
- **Implementation plans:** **`/plan`** writes **`docs/agent-jobs/<job>/dev-plan.md`** only — **[`docs/agent-jobs/README.md`](docs/agent-jobs/README.md)**.

## 3. Planning discipline (workshop)

Use **`/plan`** and an approved **`dev-plan.md`** before **substantive**, multi-file work on an exercise **app**; quick doc or typo fixes do not require a plan. When scope includes **Exercise 3**, plans should list **`Doc:`** checklist items for artifacts described in **`exercise-3/docs/DOC_INDEX.md`**.

## 4. Operational excellence

After meaningful code changes, follow **`.cursor/skills/check-project-health/SKILL.md`** (Implementation mode when executing a plan) to discover and run the right **`uv` / `pytest` / `ruff`** and **`bun`** checks for the app roots you touched — not a single global command from repo root.

**Tooling setup (new machine):** **[`PREPARATION.md`](PREPARATION.md)** (steps 1–4).
