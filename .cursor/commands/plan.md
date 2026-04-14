---
description: Create a comprehensive feature plan with deep codebase analysis and research
argument-hint: <job-name-or-short-topic> — optional; used for folder name under docs/agent-jobs/
---

# Plan (`/plan`)

## Feature / job: $ARGUMENTS

> [!IMPORTANT]
> **Research and planning only.** Do **not** modify production code, tests, or shared rules while running `/plan`. All proposed work is captured in **`docs/agent-jobs/<job-name>/dev-plan.md`** only.
>
> **Naming:** The **command definition** is this repo’s **`commands/plan.md`**; the **plan artifact** you write is always **`dev-plan.md`** so the two are not confused.
>
> **Do not** create a separate mandatory `task.md` (or duplicate checklist elsewhere). **`/implement`** will tick **`[ ]` → `[x]`** on the **Implementation checklist** inside **`dev-plan.md`**.

## Artifact location

- **Directory:** `docs/agent-jobs/<job-name>/`
- **File:** `docs/agent-jobs/<job-name>/dev-plan.md`
- **`<job-name>`:** short `kebab-case` slug. If `$ARGUMENTS` is empty or vague, derive a sensible name from the user’s last message (e.g. `add-search-api`, `exercise-2-catalog`). Create the directory if it does not exist.

**Optional:** `docs/agent-jobs/<job-name>/developer-notes.md` — only if the user wants scratch notes; keep the **single source of truth** for task checkboxes in **`dev-plan.md`**.

---

## Mission

Transform a feature request into a **comprehensive implementation plan** through systematic codebase analysis, external research, and strategic planning.

**Core principle:** We do **not** write implementation code in this phase. The goal is a **context-rich** plan so an execution agent can succeed with minimal extra research.

**Philosophy:** **Context is king.** The plan must contain what the executor needs—patterns, files to read, links, validation commands—grounded in **this** repository (not a generic template).

**Discovery rule:** Do **not** assume specific docs exist (e.g. `CODEBASE_MAP.md`, `DOC_INDEX.md`). Use what is present; infer the rest from the tree and configs.

### Terminology: two different “phase” ideas (avoid confusion)

| Name                                        | Meaning                                                                                                                      | Where                     |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| **Planning workflow**                       | How **you** run **`/plan`**: Clarification gate → **Phase 1–5** in **Planning workflow** below.                              | Only this command file.   |
| **Implementation phases** (in the artifact) | How work is split in **`dev-plan.md`**: **Phase D1, D2, …** — each phase has a **Gate** (exit checks) before the next phase. | Inside **`dev-plan.md`**. |

Say **“planning Phase 2”** (research) vs **“implementation Phase D2”** (build) so nobody mixes the two.

### What goes in `dev-plan.md` (artifact)

- **Context** — feature, story, problem/solution, **CONTEXT REFERENCES**, patterns.
- **Implementation phases (Phase D1, D2, …)** — the phased plan for **building** the feature; **risk-first** order; after **each** phase a **Gate** (checkbox exit criteria: tests, commands, proven assumptions); **incremental** verification every phase.
- **Open questions (resolved during planning)** — asked and answered while running **`/plan`**; recorded in the artifact so **`/implement`** does not inherit ambiguity.
- **STEP-BY-STEP TASKS** — atomic work in **D1 → D2 → …** order.
- **Implementation checklist** — one **`- [ ]`** per atomic task; **`/implement`** ticks these.
- **Validation / acceptance** — definition of done for the whole job.

---

## Clarification gate (do this before research or `dev-plan.md`)

**No plan file until the ask is clear.**

1. **Judge the request:** If it is vague, incomplete, contradictory, or missing essentials (goal, scope boundaries, who it’s for, what “done” means, constraints), **do not** start codebase deep-dives or draft **`dev-plan.md`** yet.
2. **Back-and-forth with the user:** Ask concrete questions (batch them if that’s easier). Offer a short restatement of what you understood; flag open choices. Continue until ambiguities that would change the plan are resolved—or the user explicitly approves named assumptions you list.
3. **Then proceed:** Only when the problem statement and success criteria are **sharp enough** that a different engineer would not need the chat history → continue with **planning Phase 1** onward and eventually write **`dev-plan.md`**.

If new gaps appear during research, **pause**, clarify with the user, then resume—don’t guess your way through scope.

---

## Planning workflow (Phase 1–5 — not the same as implementation Phase D1… in `dev-plan.md`)

### Phase 1: Feature understanding

**Deep feature analysis:**

- Extract the core problem being solved.
- Identify user value and (if applicable) business impact.
- Determine feature type: New Capability / Enhancement / Refactor / Bug Fix.
- Assess complexity: Low / Medium / High.
- Map affected systems and components.

**User story** (create or refine):

```text
As a <type of user>
I want to <action/goal>
So that <benefit/value>
```

### Phase 2: Codebase intelligence gathering

Use thorough search and reads (parallel where helpful).

**1. Project structure**

- Primary languages, frameworks, runtime versions.
- Directory layout and architectural patterns **as they appear in this repo**.
- Boundaries (modules, exercises, services) and integration points.
- Config files (`pyproject.toml`, `package.json`, etc.) and how to run/install.
- Environment setup (see `setup/`, READMEs) when relevant.

**2. Pattern recognition**

- Similar implementations; naming (camelCase, snake_case, kebab-case); file layout.
- Error handling, logging, and conventions to mirror.
- Anti-patterns to avoid.
- Project rules: read **`AGENTS.md`**, **`CLAUDE.md`**, or equivalents **if they exist**.

**3. Dependency analysis**

- External libraries relevant to the feature; how they are wired (imports, configs).
- In-repo docs under `docs/`, `ai_docs/`, or other folders **if present**—cite real paths only.
- Versions and compatibility when it matters.

**4. Testing patterns**

- Test framework and layout; similar tests; unit vs integration; coverage expectations if stated.

**5. Integration points**

- Files to update vs create; routers/API registration; data models; auth, if applicable.

**6. Documentation impact (navigation docs)**

- When scope includes **`exercise-3/`** (app or `exercise-3/docs/` or `exercise-3/CHANGELOG.md`), read **`exercise-3/docs/DOC_INDEX.md`** if it exists and note which pillars (**`CODEBASE_MAP.md`**, **`ARCHITECTURE.md`**, **`CHANGELOG.md`**, optional module **`README.md`**) need updates for this job.
- In **`dev-plan.md`**, capture that as **`## Documentation impact`** plus **`- [ ] Doc: …`** lines in the **Implementation checklist**—same change set as code, not a vague “update docs later.”

**Emerging gaps:** if new ambiguities show up here, loop back to **Clarification gate** before finalizing **`dev-plan.md`**.

### Phase 3: External research and documentation

When the feature depends on libraries or APIs not fully documented in-repo:

- Official docs with section anchors; examples; gotchas; migrations/breaking changes.
- Security and performance notes when relevant.

**Compile references** (in the plan body) using this shape:

```markdown
## Relevant Documentation

- [Library Official Docs](https://example.com/docs#section)
  - Specific area: …
  - Why: …
```

### Phase 4: Deep strategic thinking

- Fit with existing architecture; dependencies and ordering.
- Edge cases, failure modes, race conditions.
- Performance; security; maintainability.
- **Design decisions:** alternatives, rationale, extensibility, backward compatibility.
- **Risk-first phased implementation (for the implementer):** identify assumptions that could invalidate the approach. **Phase D1** in `dev-plan.md` should **validate or kill** those assumptions (spikes, minimal vertical slice, contract tests, data-shape checks) **before** large surface-area coding. Prefer **thin end-to-end** feedback early over a long “foundation only” stretch with no tests.
- **Testing in the flow:** each **implementation phase** ends with a **Gate** backed by **observable checks** (automated tests, manual script, or demo)—not only one big test phase at the end unless scope is trivial.

### Phase 5: Generate `dev-plan.md` content

Fill the **template below** into **`docs/agent-jobs/<job-name>/dev-plan.md`**.

**Implementation phases in `dev-plan.md` (required):**

1. The artifact must contain a clear **phased implementation plan**: **3–6 phases** named **Phase D1, D2, …** (logical, merge-sized). Each phase title = **outcome** (e.g. “Phase D1 — Prove API contract + storage spike”).
2. **Order:** **highest risk / fuzziest assumptions first** (within dependencies). What cheaply de-risks the rest belongs in **Phase D1**.
3. **After every phase, a Gate:** use the heading **`#### Gate`** under that phase. The Gate is the **exit checklist** (tests, commands, “assumption X proven”) the implementer must satisfy **before** starting the **next** implementation phase. The **last** phase’s Gate is “before marking the job done”. Gates = quality control between phases.
4. **STEP-BY-STEP TASKS** follow **Phase D1 → D2 → …**; group under **`### Implementation phase D1`** (etc.), same boundaries as in the phased plan above.
5. **Open questions:** **You** (the planning agent) must **ask the user** during `/plan` and **record every decision** in `dev-plan.md` under **## Open questions (resolved during planning)**. Nothing should be left for “the implementer to guess.” If there are no open topics, write **None — no open questions; all decisions recorded during planning.** **`/implement`** will **refuse to start** if that section still looks unresolved.

**Checklist rule for `/implement`:** After **STEP-BY-STEP TASKS**, include **## Implementation checklist**: one **`- [ ]`** per atomic task, same order. Optional prefix **`D1 —`** / **`D2 —`** matching the phase.

**Documentation impact in `dev-plan.md`:** When the job touches **`exercise-3/`** or its navigation docs, the artifact MUST include **`## Documentation impact`** (which files change and why) and at least one **`- [ ] Doc: …`** checklist item per touched doc (**`exercise-3/docs/DOC_INDEX.md`** explains when each file applies). For repos without Exercise 3 scope, omit the section or write **None — no Exercise 3 / navigation doc updates.**

---

### Template to fill (implementation agent consumes this)

```markdown
# Feature: <feature-name>

The following plan should be complete; validate documentation, codebase patterns, and task sanity before implementing.

Pay special attention to existing names, types, and models—import from the correct files.

## Feature Description

<Detailed description, purpose, and value>

## User Story

As a <type of user>
I want to <action/goal>
So that <benefit/value>

## Problem Statement

<Specific problem or opportunity>

## Solution Statement

<Approach and how it solves the problem>

## Feature Metadata

**Feature Type**: [New Capability/Enhancement/Refactor/Bug Fix]
**Estimated Complexity**: [Low/Medium/High]
**Primary Systems Affected**: [components/services]
**Dependencies**: [libraries or services]

---

## Documentation impact

**Required when scope touches `exercise-3/` or its navigation docs.** Otherwise replace with: **None — no Exercise 3 / navigation doc updates.**

- **Files to update:** (e.g. `exercise-3/docs/CODEBASE_MAP.md`, `exercise-3/docs/ARCHITECTURE.md`, `exercise-3/CHANGELOG.md`, optional module `README.md`)
- **Checklist:** mirror these as **`- [ ] Doc: …`** entries in **## Implementation checklist** below.

---

## CONTEXT REFERENCES

### Relevant Codebase Files — READ BEFORE IMPLEMENTING

<List files with line ranges and why>

- `path/to/file.py` (lines 15-45) - Why: …

### New Files to Create

- `path/to/new_file` - Why: …

### Relevant Documentation (external)

- [Doc](https://example.com#section) - Why: …

### Patterns to Follow

<Concrete patterns from this project>

**Naming Conventions:**

**Error Handling:**

**Logging:**

**Other:**

---

## Phased implementation plan

Implementation is **split into phases** (Phase D1, D2, …). Each phase has an **objective**, **scope summary**, and a **Gate** — the exit checklist before the next phase. **Phase D1** addresses the **riskiest** unknowns first (within dependencies). **Do not** defer all verification to the last phase unless scope is trivial.

### Phase D1 — <short outcome name; e.g. validate API + persistence spike>

**Objective:** <what this phase proves or delivers>

**Scope (summary):**

- …

#### Gate

**Pass all of these before starting Phase D2:**

- [ ] <e.g. contract test passes / spike reviewed>
- [ ] <commands: e.g. `pytest tests/test_x.py -q`>
- [ ] <assumption proven or revised: e.g. “DB supports JSON field”>

### Phase D2 — <next outcome>

**Objective:** …

**Scope (summary):**

- …

#### Gate

**Pass all of these before starting Phase D3:**

- [ ] …

### Phase D3 — <…> (add Phase D4… as needed)

**Objective:** …

**Scope (summary):**

- …

#### Gate

**Pass all of these before marking the overall job complete:**

- [ ] …

---

## Open questions (resolved during planning)

**Required section** — `/implement` aborts if this heading is missing or if decisions are incomplete. Always include it (table **or** the single **None — …** line below).

**While running `/plan`:** ask the user anything that would change the shape of implementation. **Record the decision** in the last column. Do **not** leave blanks—`/implement` treats unresolved rows as a blocker.

| Topic             | Question (asked during planning) | Decision / answer                 |
| ----------------- | -------------------------------- | --------------------------------- |
| <e.g. pagination> | <what you asked>                 | <user’s answer or agreed default> |

If there are **no** open topics after Clarification + research, replace the table with a single line:

**None — no open questions; all decisions recorded during planning.**

---

## STEP-BY-STEP TASKS

IMPORTANT: **Strict order Phase D1 → D2 → …**, matching **Phased implementation plan** above. One task = one atomic change; prefer a **VALIDATE** line per task.

Use action keywords: **CREATE** / **UPDATE** / **ADD** / **REMOVE** / **REFACTOR** / **MIRROR**.

Repeat this block for **each** task (under the right phase heading):

### {ACTION} {target_file}

- **IMPLEMENT**: …
- **PATTERN**: `file:line`
- **IMPORTS**: …
- **GOTCHA**: …
- **VALIDATE**: `{command}`

### Implementation phase D1

<…all Phase D1 tasks, each using the block above…>

### Implementation phase D2

<…all Phase D2 tasks…>

---

## Implementation checklist

- [ ] D1 — <short label; matches first D1 task>
- [ ] D1 — <…>
- [ ] D2 — <first D2 task>
      <…one `- [ ]` per atomic task, same order as STEP-BY-STEP…>

---

## TESTING STRATEGY

### Unit Tests

### Integration Tests

### Edge Cases

---

## VALIDATION COMMANDS

Execute as appropriate for this repo (discovered from configs/README).

### Level 1: Syntax & Style

### Level 2: Unit Tests

### Level 3: Integration Tests

### Level 4: Manual Validation

### Level 5: Additional (optional)

---

## PROJECT HEALTH (`check-project-health` skill)

The executor should follow **`.cursor/skills/check-project-health/SKILL.md`** in **Implementation mode** **after** Gates and plan-listed validation, **before** treating the job as done (simple fix + re-run loop until checks pass, per that skill).

**In this plan, make “green” unambiguous:**

- [ ] **Scope:** Which trees does this job touch? (e.g. `…/app/backend`, `…/app/frontend`, repo docs only, …)
- [ ] **Commands:** Paste the **exact** shell lines for this job (copy from **VALIDATION COMMANDS** above and/or the **This repository — commands for relevant app folders** section in the skill when `app/backend` / `app/frontend` trees are involved).
- [ ] **When:** Implementer runs the skill (same commands) once implementation + plan validation are complete; non-simple failures block handover until resolved in chat or the plan is revised.

---

## ACCEPTANCE CRITERIA

- [ ] …
- [ ] …

---

## COMPLETION CHECKLIST

- [ ] Every **Gate** under **Phased implementation plan** satisfied before the next **implementation phase** was started
- [ ] All STEP-BY-STEP tasks done in order
- [ ] Validation commands pass
- [ ] **check-project-health skill** (or equivalent commands listed under **PROJECT HEALTH**) pass for the scope of this job
- [ ] Acceptance criteria met

---

## NOTES

<Trade-offs, decisions, context>
```

---

## Quality criteria (before handoff)

### Context completeness

- [ ] Patterns and integration points documented with real paths.
- [ ] External dependencies documented with links where used.
- [ ] Gotchas and anti-patterns captured.
- [ ] Atomic tasks have executable **VALIDATE** commands where applicable.

### Implementation ready

- [ ] Another agent could **implement** from this file + repo, without the planning chat.
- [ ] **Phased implementation plan** present: **Phase D1, D2, …** each with a **`#### Gate`** (concrete exit criteria).
- [ ] **Risk-first:** Phase D1 addresses the scariest unknowns; **Gates** enforce **incremental** verification, not only at the end.
- [ ] **Open questions:** table complete with **Decision / answer** per row, or exact **None — no open questions; all decisions recorded during planning.**
- [ ] **Implementation checklist** `- [ ]` items match STEP-BY-STEP order and count (optional **`Dx —`** prefixes).
- [ ] Pattern references use **file:line** where helpful.

### Pattern consistency

- [ ] Tasks follow this codebase’s conventions.
- [ ] Testing approach matches how this repo tests.
- [ ] **Documentation impact:** for Exercise 3 scope, **`## Documentation impact`** and **`Doc:`** checklist items are present and match **`exercise-3/docs/DOC_INDEX.md`** guidance (or explicitly **None**).

### Information density

- [ ] Specific and actionable—not generic placeholders.
- [ ] Validation commands are non-interactive where possible.
- [ ] **PROJECT HEALTH** section lists scope + exact commands (or defers explicitly to the **check-project-health** skill for discovered `app/backend` / `app/frontend` roots).

---

## Success metrics

- **One-pass implementation:** executor can finish without extra research or clarification (goal).
- **Validation complete:** every atomic task has validation where meaningful.
- **No prior knowledge test:** someone unfamiliar could implement from the plan + repo.

**Confidence score:** report `#/10` for first-pass success after writing the plan.

---

## Report (in chat after writing the file)

- Summary of feature and approach.
- **Full path:** `docs/agent-jobs/<job-name>/dev-plan.md`
- Complexity and key risks.
- Confidence score.
- Say: **“Please review `docs/agent-jobs/<job-name>/dev-plan.md`. When approved, run `/implement` with that path or job name.”**
