# `.agents` — workshop command library

This folder holds **command definitions** and **scoped rules** for this repo’s agentic workflows. **Layer 1 coding norms** live under **[`rules/`](rules/INDEX.mdc)** (same `.agents/` tree) and **[`AGENTS.md`](../AGENTS.md)** at the repo root—invoke those when editing exercise app code; use **`commands/`** and **`skills/`** for PIV workflows.

## Core PIV commands

| Command          | File                                             | Role                                                                                       |
| ---------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| **`/prime`**     | [`commands/prime.md`](commands/prime.md)         | Context only—layout, docs, tooling, **last 10 commits (full messages)**; optional **focus** arg for directional exploration. |
| **`/plan`**      | [`commands/plan.md`](commands/plan.md)           | Research + write **`docs/agent-jobs/<job>/dev-plan.md`** (no production code).             |
| **`/implement`** | [`commands/implement.md`](commands/implement.md) | Implement from an approved **`dev-plan.md`**; respect **Gates**; tick checklist; validate. |

Plan files live under **`docs/agent-jobs/`** (see [`docs/agent-jobs/README.md`](../docs/agent-jobs/README.md)).

## Git handover

| Command       | File                                           | Role                                                                 |
| ------------- | ---------------------------------------------- | -------------------------------------------------------------------- |
| **`/finish`** | [`commands/finish.md`](commands/finish.md)     | Cleanup, run repo-documented checks, **one atomic commit** (no push). |
| **`/push`**   | [`commands/push.md`](commands/push.md)         | **Push-only:** clean tree, verify ahead/behind, confirm, `git push`. |

Flow: land work with **`/finish`**, then publish with **`/push`**. (Mirrors the split in **`.cursor-template`**: heavy validation + commit vs. separate push safety.)

## Using these in Cursor (and similar IDEs)

Cursor’s slash menu normally loads from **`.cursor/commands/`** only. In this repo, **invoke the same workflows** by:

- **@**-adding the command, skill, or rule file (e.g. [`commands/prime.md`](commands/prime.md), [`commands/plan.md`](commands/plan.md), [`rules/INDEX.mdc`](rules/INDEX.mdc), [`skills/check-project-health/SKILL.md`](skills/check-project-health/SKILL.md), [`commands/finish.md`](commands/finish.md), [`commands/push.md`](commands/push.md)) to the prompt, or
- Opening the file and asking the agent to follow it, or
- Creating a **local** `.cursor/commands/` or **`.cursor/rules/`** symlink to this folder’s **`commands/`** / **`rules/`** if you want native slash menus or rule auto-attach (optional; **`.cursor/`** is git-ignored here).

## Other commands

- **`commands/`** (review & retro) — **`/code-review`**, **`/code-review-fix`**, **`/execution-report`**, **`/system-review`**. Artifacts go next to **`dev-plan.md`** under **`docs/agent-jobs/<job>/`** (see **[`exercise-3/README.md`](../exercise-3/README.md)** §3.2–3.3).
- **`skills/check-project-health/`** — Discovery + checks + (in **Implementation mode**) simple-fix loop until green; **`/plan`** and **`/implement`** tell the agent when to run it; **`/finish`** may use **Advisory mode** for a pre-commit pass.

## Legacy template folder

**`.agents-template/`** (if present) is an optional upstream-style bundle—extra commands, reference notes, PRD template. **`/.agents`** in this repo is the slim workshop set actually in use.
