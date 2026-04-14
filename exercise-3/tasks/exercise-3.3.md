# Exercise 3.3 — Execution report, system review, and docs

This is the final part of the 3.1–3.3 flow. You have built a feature, reviewed it, and fixed the findings. Now you step back and look at the _process_ — not the code.

This is the meta layer: what did you plan vs. what actually happened? Where did the process help, and where did it get in the way? What would you change for next time?

**Stay in the same chat** as 3.1 and 3.2. This is the last part in this session — after this, you will start a new chat for 3.4.

---

## Step 1 — Execution report

Run the **`/execution-report`** command ([`.cursor/commands/execution-report.md`](../../.cursor/commands/execution-report.md)). Point it to your job folder (e.g. `catalog-filters-ex3`).

The command compares your `dev-plan.md` to what actually happened during 3.1 and 3.2. It documents:
- What shipped vs. what was planned
- Where the implementation diverged from the plan (and why)
- Challenges, surprises, and anything that was skipped
- Validation results

### Read the report

**Open `execution-report.md` and read through it.** This is where the learning happens. Pay attention to:

- **Divergences** — Where did reality differ from the plan? Was the plan wrong, or did the implementation make a better call? Understanding _why_ things diverged is more valuable than the divergence itself.
- **Surprises** — What did you not anticipate? These are the things your planning process did not catch. Next time, you might think about them earlier.
- **What went well** — Equally important. If the plan-to-implementation was smooth in certain areas, what made those areas work? Can you replicate that pattern?

> This is the rubber duck debugging equivalent for your _process_ — explaining what happened forces you to understand it.

---

## Step 2 — System review

Run the **`/system-review`** command ([`.cursor/commands/system-review.md`](../../.cursor/commands/system-review.md)). Same job folder.

This command goes one level deeper than the execution report. It is not about what happened — it is about _why_ it happened and what to improve in the workflow itself. The command will:

1. Classify each divergence as **good** (justified, the plan was wrong) or **bad** (problematic, the process failed)
2. Find root causes — unclear plan? Missing context? Validation gap?
3. Propose concrete improvements to the commands, rules, or workflow

### Read the review

**Open `system-review.md`.** The proposed improvements are the most interesting part. You do not have to accept them all — but they give you a sense of where the workflow has friction.

---

## Step 3 — Bounded improvements

The system review probably proposed several improvements to the workflow. Pick **at most 2** small, concrete edits to apply now. These can be:

- A small update to [`AGENTS.md`](../../AGENTS.md)
- A tweak to a rule in [`.cursor/rules/`](../../.cursor/rules/)
- A minor edit to one command file

The key word is **bounded** — no full rewrites, no big restructuring. If the system review suggests more than two changes, keep the rest as proposals in `system-review.md` for future reference.

For example: if the system review found that the plan missed input validation edge cases, you could add a reminder about boundary checks to the relevant rule file. Or if a command's output was unclear, a one-line clarification in that command file. Small, targeted, useful.

> The reason for the limit: workflow improvements should be incremental. Big changes to the process mid-project introduce their own risks — the same principle as refactoring production code in small, tested steps.

---

## Step 4 — Update the docs

Your implementation changed the codebase. The docs should reflect that. Update the following:

- **[`docs/CODEBASE_MAP.md`](../docs/CODEBASE_MAP.md)** — Add or update entries for files you created or changed
- **[`docs/ARCHITECTURE.md`](../docs/ARCHITECTURE.md)** — If your filtering implementation introduced new patterns or architectural decisions, document them
- **[`CHANGELOG.md`](../CHANGELOG.md)** — Add a meaningful entry under `[Unreleased]` covering what you built in 3.1 through 3.3

You can ask your assistant to help with the docs updates — it has the full context of what changed. But review what it writes. Docs that are wrong are worse than no docs.

> **See [`docs/DOC_INDEX.md`](../docs/DOC_INDEX.md)** for a guide on what goes where.

---

## Done?

- [ ] `execution-report.md` and `system-review.md` exist in your job folder
- [ ] At most 2 bounded improvements applied (or proposals deferred in writing)
- [ ] Codebase map and architecture docs updated
- [ ] Changelog entry for 3.1–3.3

**This wraps up the 3.1–3.3 flow.** You have now completed a full cycle: plan → implement → review → fix → reflect → improve.

Take a moment to think about what you just did. You shipped a feature, reviewed it, reflected on the process, and improved the workflow — all in one continuous session. In a real project, this cycle repeats for every meaningful change. The question is not whether it takes more time. The question is: does it save you from the kind of problems that cost _real_ time — debugging in production, refactoring spaghetti code, onboarding someone to a codebase nobody documented?

**Next: [Exercise 3.4 — Repository abstraction](exercise-3.4.md).** Start a **new chat session** — you are moving to a different feature and the assistant benefits from a clean context.
