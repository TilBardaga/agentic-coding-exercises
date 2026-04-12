---
description: Fix issues listed in a code-review.md from the same agent job folder (or an inline issue list)
---

You ran **`/code-review`** (or a human review) and have findings to address.

**Code review artifact:** `$1` — prefer **`docs/agent-jobs/<job-name>/code-review.md`** (same folder as `dev-plan.md`). If `$1` is not a path, treat it as a short description of issues and proceed from context.

**Scope:** `$2` — files, directories, or “all issues in the review file” (default: fix everything listed in the review).

For each issue:

1. Explain what was wrong.  
2. Implement the fix.  
3. Run the smallest relevant tests or checks to verify.

When done, follow **[`.agents/skills/check-project-health/SKILL.md`](../skills/check-project-health/SKILL.md)** in **Implementation mode** (simple fixes + re-run until checks pass), or follow root **`README.md`** / **`AGENTS.md`** if the skill does not apply, then summarize results.
