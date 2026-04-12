---
description: >-
  Technical pre-commit review: logic, security, performance, and standards on changed files;
  write findings to code-review.md beside dev-plan.md for the same agent job (docs/agent-jobs/<job>/).
argument-hint: <job-name> | <path-to-dev-plan.md> | <path-to-docs/agent-jobs/<job>/>
---

# Code Review (`/code-review`)

Review **recent code changes** for **defects** (logic, security, performance, maintainability)—not for plan adherence (that is **system review**) and not for restating the linter.

## Input: `$ARGUMENTS`

Resolve the **job directory** `docs/agent-jobs/<job-name>/` (same as **`/plan`** / **`/implement`**):

1. If `$ARGUMENTS` points to an existing **directory** under `docs/agent-jobs/`, use it.
2. If it points to **`dev-plan.md`** (or another file) inside `docs/agent-jobs/<job-name>/`, use that file’s **parent** directory.
3. Otherwise treat `$ARGUMENTS` as **`<job-name>`** and use **`docs/agent-jobs/<job-name>/`**.
4. If the folder does not exist, stop and ask the user.

## Output file (required)

Save the review to **`docs/agent-jobs/<job-name>/code-review.md`** (overwrite for a fresh pass on the same job).

Do **not** default to `.agents/code-reviews/`—keep validation artifacts with the job.

## Core principles

- Simplicity: every line should earn its place.
- Optimize for **readers** of the code, not the author.
- Prefer fewer, **high-signal** findings over noise.

## What to review

Gather context from what **this repo** actually has:

- **`AGENTS.md`** (or equivalent rules), root **`README.md`**
- **`docs/`** or exercise READMEs if they define standards
- **Nearby modules** only as needed to judge patterns (there may be no `/core`—infer from the tree)

Then run:

```bash
git status
git diff HEAD
git diff --stat HEAD
git ls-files --others --exclude-standard
```

Read **changed and new** files in full (not only the diff) when size allows; if a file is huge, prioritize the diff plus surrounding context.

For each touched file, check:

1. **Logic** — edge cases, errors, races, off-by-one, wrong conditionals  
2. **Security** — injection, XSS, secrets, unsafe deserialization  
3. **Performance** — N+1, hot-path waste, unbounded work  
4. **Quality** — naming, duplication, complexity, typing where the project uses it  
5. **Standards** — matches documented patterns and tooling (lint/type/test) for this repo

## Verify issues

Where possible, corroborate with tests, types, or a minimal repro—avoid hypothetical bugs.

## Output format

**Path:** `docs/agent-jobs/<job-name>/code-review.md`

**Stats:**

- Files modified: …  
- Files added: …  
- Files deleted: …  
- New lines / deleted lines (approx.): …  

**For each issue:**

```text
severity: critical|high|medium|low
file: path/to/file
line: [number or range]
issue: [one line]
detail: [why it matters]
suggestion: [fix approach]
```

If nothing substantial: state clearly that **no blocking issues** were found (lint-only nits belong in the linter, not here).

## Important

- Line-level **specificity**; no vague “this is messy.”
- **Real bugs** over style.
- **Critical** for credible security issues.
