# Exercise 3.2 — Code review and fix

You shipped the filtering feature in 3.1. Now it is time to review it — not by eyeballing the code yourself, but by running a structured code review through the agent.

Think of this as having a senior colleague review your PR before it merges. The `/code-review` command checks for real defects: logic errors, security issues, code smells, naming problems, duplication, and violations of the project's conventions. It is not checking whether you followed the plan — it is checking whether the code is good.

**Stay in the same chat** as 3.1. The assistant has your plan and implementation in context, which makes the review more informed.

---

## Step 1 — Run the code review

Run the **`/code-review`** command ([`.agents/commands/code-review.md`](../../.agents/commands/code-review.md)). Point it to the same job folder you used in 3.1 (e.g. `catalog-filters-ex3`).

The command will:
1. Read the project conventions and standards
2. Diff all your changes
3. Check for logic errors, security issues, performance problems, code smells, and convention violations
4. Write its findings to `docs/agent-jobs/catalog-filters-ex3/code-review.md`

### Read the review

When the review is done, **open `code-review.md` and read through the findings.** This is where you learn — not just about this specific code, but about patterns you might be introducing without realizing it.

For each finding, ask yourself:
- **Do you agree?** Not every finding is valid. The AI can flag things that are actually fine, or miss context you have. You are the final judge.
- **Is this a real issue or a style preference?** Critical and high severity findings need fixing. Low severity findings might be worth noting but not worth the refactoring cost right now.
- **Would you have caught this yourself?** That is interesting information for your process.

> If you disagree with a finding, that is fine — document it as a conscious deferral in the next step. The point is not to fix everything blindly, but to make informed decisions about code quality.

---

## Step 2 — Fix the findings

Run the **`/code-review-fix`** command ([`.agents/commands/code-review-fix.md`](../../.agents/commands/code-review-fix.md)) to address the review findings.

The command will work through each issue, apply fixes, and run tests to make sure nothing breaks. If there are findings you intentionally want to skip (because you disagree or they are out of scope), mention that to the assistant so it can document the deferral.

> **Tip:** Deciding _not_ to fix something is a valid engineering decision — as long as it is a conscious one. "I disagree because X" is professional. "I will skip it because I am in a hurry" is technical debt. Know which one you are choosing.

**After the fixes, verify again:**

```bash
cd app/backend
uv run pytest
```

Tests should still be green. If the fix broke something, that is valuable feedback — the review found a real issue but the fix introduced a regression. Work through it with the assistant.

---

## Take a moment to reflect

You have now completed the full technical cycle for one feature: prime → plan → implement → review → fix. Before moving on, think about what just happened:

- How did the code review compare to reviews you have done or received on real projects?
- Did it catch anything you missed? Did it miss anything obvious?
- How does it feel to have the review built into the workflow rather than being a separate step someone has to remember?

You will formalize this reflection in 3.3 with the execution report and system review.

---

## Done?

- [ ] `code-review.md` exists in your job folder with concrete findings
- [ ] Fixes applied (or deferrals documented with reasoning)
- [ ] Tests still pass

**Next: [Exercise 3.3 — Execution report, system review, and docs](exercise-3.3.md).** Still the same chat — one more part before you start fresh.
