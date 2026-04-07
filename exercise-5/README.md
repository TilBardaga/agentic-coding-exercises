# Exercise 5: Plan shape + planning command

**Goal:** (1) Design the **markdown shape** of an implementation plan so an **executor agent** can run without chat history (Pattern 2). (2) Turn your **manual planning workflow** into a **reusable command** (e.g. `/plan-feature`) that **researches** and **fills** that shape—so every new feature does not start from a blank prompt.

---

## Background

A typical planning cycle looks roughly like this:

1. **Initial exploration** — orient in the repo  
2. **Steer direction** — engineering judgment, scope  
3. **Research and scoping** — docs, libraries, patterns  
4. **Constraint-driven planning** — fit the codebase and non-negotiables  
5. **Plan review** — tighten before implementation  

That works well, but it is easy to repeat the same conversational steps for every feature. This exercise asks: can you **encode** what you always do into **one command**, without losing quality—and can you **define the plan file** so another session or agent can **execute** it?

---

## Pattern you are templating

Conceptually:

```
/prime                          # Load project context (optional)
↓
Explore PRD / backlog / ticket   # What should we build next?
↓
Steer (accept or adjust scope)  # Human judgment
↓
Research (codebase + docs)      # Patterns, libraries, constraints
↓
/plan-feature "<request>"       # Produce an implementation-ready plan file
↓
Review and refine               # Still human; command does not remove this
```

**Exercise question:** How much of this can you fold into **one** command without losing quality—and what must the **plan document** contain for a clean handoff?

---

## What you already have in this repo

| File | Role |
|------|------|
| **`reference/plan-template.md`** | Minimal **structure-only** template (sections to fill, no research steps baked in). |
| **`reference/PlanningPrompts.md`** | Sample **multi-prompt** “vibe planning” flow; see especially the final plan step—what should that output contain? |
| **`inspiration.md`** | Example front matter + flow for a planning-style command (argument hint, research, handoff). |
| **`example-solution/planning-output-structure.example.md`** | One **example** full plan template (Python-flavored)—illustrative only. |
| **`example-solution/`** (`template-driven/`, `phased-variant/`) | Example **`plan-feature`** command bodies—**not** official answers. |

You do **not** have to use these verbatim; they are references.

---

## Your task

### Part A — Plan output shape (Pattern 2)

**Consumer:** Another AI agent (or you in a **new** session) that did **not** see the planning conversation.

1. **Name** your template file (e.g. `planning-output-structure.md`) and list **sections** the plan must include so implementation can succeed end-to-end: feature context, approach, relevant files/patterns, tasks in order, tests, validation commands, etc.  
2. Skim **`reference/PlanningPrompts.md`** — what does the last “create plan” step imply for structure?  
3. Compare with **`reference/plan-template.md`** and **`example-solution/planning-output-structure.example.md`**; steal ideas, adapt paths to **your** stack.

### Part B — Planning command

**Create your own planning command** that combines **research + filling Part A’s template** for your repo.

1. **Recall your manual workflow** — What do you always do? What do you sometimes skip?  
2. **Design** — How much research is always in the command vs optional? Where do plan files land (`plans/`, `.agents/plans/`, …)?  
3. **Implement** — e.g. `commands/plan-feature.md`, or your tool’s equivalent. Wire real paths: `AGENTS.md`, tests, lint.  
4. **Test** — Run on a **real** feature idea; the emitted file should match Part A’s contract.

---

## Design constraints (minimum)

At minimum, your **command** should:

- **Understand** the feature request (clarify if needed).  
- **Analyze** the codebase enough to point at real files and patterns.  
- **Research** external docs when needed.  
- **Emit** a plan document that matches **Part A** and that another session or agent could **execute** without the original chat.

---

## Success criteria

- **Template** — Sections are explicit enough that an executor would not need to guess scope or validation.  
- **Command** — Reusable for more than one feature without rewriting the whole prompt.  
- **Quality** — Plans are at least as good as your ad-hoc manual runs.  
- **Fits you** — Depth and style match how you want to work.

---

## Testing

1. Add your command file under your tool’s conventions (e.g. `commands/plan-feature.md`).  
2. Reload the tool if required.  
3. Run it on a concrete feature, e.g.:

   `/plan-feature Add another LLM provider using your stack’s agent framework (name the provider and default model).`

4. Check the file: enough context? Actionable tasks? Validation steps? Does it follow **Part A**?  
5. Iterate.

---

## Reflection (after you try it)

1. Which manual steps did you keep—and why?  
2. What did you drop or simplify?  
3. What did you add that the manual flow did not have?  
4. Does the **emitted plan** match the **structure** you defined in Part A? What would you change?  
5. Would you use this on a real project? If not, what is missing?

---

## Hints

- Start **small**, then extend after 2–3 real uses.  
- Separate **always** vs **optional** phases in the command.  
- **Parallel** where safe (codebase search vs web docs) if your tool supports it.

---

## Bonus levels (optional)

- Branch by feature type: new / enhancement / refactor / bug.  
- Multiple depths: quick vs standard vs deep.  
- Subagent or tool-specific research steps.  
- Built-in checks before writing the plan file.

---

## Example implementations (optional)

| Location | Contents |
|----------|----------|
| **`example-solution/planning-output-structure.example.md`** | Example plan **document** shape (reference). |
| **`example-solution/template-driven/`** | `plan-feature.md`, `alternative_solution.md` — template-driven flow. |
| **`example-solution/phased-variant/`** | `plan-feature.md`, `optimal_planning.md` — phased variant + meta notes. |

Read **`example-solution/README.md`** and each subfolder’s **`README.md`**.

---

## Takeaway

The best planning command is the one **you actually reuse**. The best plan template is one an **executor** can follow without your chat history. Treat both as first versions and iterate from real features.

**Next:** [**exercise 6**](../exercise-6/README.md) — build an **`/execute`** command that consumes that plan file and implements it with validation (closes the loop from “plan on disk” to “code shipped”).
