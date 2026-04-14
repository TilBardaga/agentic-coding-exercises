# Workshop rules (maintenance)

**Audience:** Humans and agents **editing** project rules—not a substitute for reading the rules themselves.

Committed location: **`.cursor/rules/`** (same folder as this file).

## SSOT per file

| File                                        | Owns                                                                                       |
| ------------------------------------------- | ------------------------------------------------------------------------------------------ |
| `INDEX.mdc`                                 | **Routing only** (`alwaysApply: true`). Which numbered file to open; glob reference table. |
| `01-workshop-backend-architecture.mdc`      | Backend layers (`api`, `services`, `models`, `core`, `data`), boundaries, edge validation. |
| `02-workshop-backend-style-and-quality.mdc` | Typing, Ruff alignment, Pydantic boundaries, async, logging, KISS/SOLID.                   |
| `03-workshop-testing.mdc`                   | pytest, AAA, isolation, fakes vs mocks, TDD.                                               |
| `04-workshop-security-and-config.mdc`       | Secrets, env, paths, bulk ops; frontend public env, XSS, Zod, storage, CSP.                |
| `05-workshop-debugging.mdc`                 | RCA template + short durable patterns.                                                     |
| `06-workshop-exercise-3-documentation.mdc` | Exercise 3 navigation docs SSOT; **`alwaysApply`**—inactive when scope excludes **`exercise-3/`**. |

**Constitution:** [AGENTS.md](../../AGENTS.md) at repo root—keep it thin; do not paste long excerpts from `.mdc` files there.

## Consistency matrix (lightweight)

| You edit…   | Re-read or verify…                                                  |
| ----------- | ------------------------------------------------------------------- |
| `01`        | Layout under `exercise-*/app/backend/app/` (`api`, `services`, …).  |
| `02`        | `**/app/backend/pyproject.toml` `[tool.ruff]` (line length, rules). |
| `03`        | Test layout under `**/app/backend/tests/`.                          |
| `04`        | `setup/README.md` for env/tooling; frontend `package.json` scripts. |
| `05`        | Nothing mandatory—keep new entries short and reproducible.          |
| `06`        | `exercise-3/docs/DOC_INDEX.md`, `exercise-3/CHANGELOG.md`, commands **`/plan`** / **`/implement`** doc bullets. |
| `INDEX.mdc` | Only when **when-to-read** routing or **glob table** changes.       |

## DRY

- One canonical place per policy: the numbered `.mdc` file.
- **`INDEX.mdc`** must not accumulate long policy prose.
