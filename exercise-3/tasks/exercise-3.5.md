# Exercise 3.5 — Free feature (capstone)

This is the final exercise. No hand-holding, no prescribed feature — you pick something, scope it, and run the full workflow yourself.

You have now used the agent commands multiple times across different types of work: a new feature (3.1), a code review cycle (3.2), process reflection (3.3), and a backend refactor (3.4). This is where you prove the workflow sticks — by applying it independently to something you choose.

**Start a new chat session.** Clean context, clean start.

**Code location:** [`../app/`](../app/)

---

## Step 1 — Pick a feature

Choose one small feature to add to the app. The key word is **small** — the point is to run the full command cycle, not to build something ambitious. A feature you can finish in one sitting is the right scope.

Here are some ideas, but feel free to come up with your own:

| Feature | What it involves | Scope |
|---------|-----------------|-------|
| **Pagination** | Add `page` and `page_size` query params to the API; show page controls in the UI | Larger — touches backend and frontend |
| **Stock status badge** | Show "In Stock" / "Low Stock" / "Out of Stock" on product cards based on a quantity field | Smaller — mostly frontend |
| **Product detail view** | Click a product card to see a detail page or modal with full description | Larger — new route or component |
| **Search highlighting** | Highlight the matched keyword in product names/descriptions in the UI | Smaller — frontend only |
| **Sort indicator in UI** | Show which column is currently sorted and in which direction (arrow icons) | Smaller — frontend only |
| **Price range slider** | Replace min/max price inputs with an interactive range slider component | Medium — frontend component swap |

Simpler features leave more time for the review cycle. Larger features stress-test the full workflow. Pick what interests you.

---

## Step 2 — Run the full cycle

You know the workflow by now. Run it end to end:

**1. `/prime`** — Orient the assistant to the area you will be working in. Focus on the files relevant to your chosen feature.

**2. `/plan`** — Describe your feature and let the command build a plan. Give it a job name (e.g. `pagination-ex3` or `stock-badge-ex3`). Review the plan before moving on — same discipline as 3.1 and 3.4.

**3. `/implement`** — Let the agent execute the plan. Review what it built.

**4. `/code-review`** — Review the changes. Read the findings.

**5. `/code-review-fix`** — Address the findings or document deferrals.

**Optional: `/execution-report` and `/system-review`** — If you want one more round of process reflection. Not required, but valuable if you have the time.

> By now this sequence should feel familiar. If it does, that is the point — a repeatable workflow that works the same way regardless of what you are building.

---

## Step 3 — Validate and document

**Run the checks:**

```bash
# Backend tests
cd app/backend
uv run pytest

# Frontend linting (if you changed frontend code)
cd app/frontend
bun check
```

`bun check` runs Biome (the project's linter and formatter) across the frontend source. It catches style issues, unused imports, and other code quality problems.

Everything that was green before should still be green. Your new feature should work in the browser — open http://localhost:3000 and test it manually.

**Update [`CHANGELOG.md`](../CHANGELOG.md)** with a short entry under `[Unreleased]` describing what you built.

---

## Done?

- [ ] Your feature works and checks are green
- [ ] `CHANGELOG.md` updated
- [ ] Code review completed (and fixes applied)

---

## That is it

You have completed exercises 3.1 through 3.5.

Over the course of this exercise, you ran the full agentic coding workflow multiple times — on a new feature, a refactor, and something you scoped yourself. Each time, the same cycle: prime, plan, implement, review, fix. And each time, you were the one steering.

**Final reflection — think about these:**

- At what point in the workshop did the workflow start feeling natural rather than forced?
- Which command gave you the most value? Which felt like overhead?
- How would you adapt this workflow for your own projects? Would you use all the commands, or pick a subset?
- What is the one thing you will do differently on Monday?

The commands and the workflow are not specific to this workshop. They work on any codebase, any team, any stack. The `/prime` → `/plan` → `/implement` → `/code-review` cycle is the same whether you are building a product filter or shipping a production feature. Take them with you.
