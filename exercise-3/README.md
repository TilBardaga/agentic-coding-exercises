# Exercise 3: Clean up a bloated `AGENTS.md`

**Goal:** Split an overloaded project rules file into **always-loaded global rules** and **on-demand context** (task-type specific), using the two-question framework (constant vs task-specific; needed every session vs only for some work).

---

## The challenge

You are given a sample **`AGENTS.md`** in this folder. It is based on a realistic (but not ideal) **Obsidian CoPilot**-style agent API: OpenAI-compatible endpoints, FastAPI, strict typing, structured logging, vertical-slice layout.

**The problem:** The file is bloated. It would auto-load 600+ lines every session, including long sections that only matter for certain kinds of work (for example, detailed guidance for **agent tool docstrings**).

**Your job:** Decide what stays in global rules, what should load **on demand**, and what is redundant. Use the framework below to separate **Layer 1** (stable project knowledge: always vs task-type) from **Layer 2** (task-specific work, which does not belong in `AGENTS.md`).

---

## The two-question framework

**Question 1:** Is this **constant** (stable, reusable) or **task-specific** (one concrete task)?  
- Constant → Layer 1 → go to Q2  
- Task-specific → Layer 2 (does not belong in `AGENTS.md`)

**Question 2** (Layer 1 only): **Needed every session?**  
- **Yes** → Auto-load in `AGENTS.md`  
- **No** → Load on demand (when that type of work shows up)

---

## The file

Open and read: **`AGENTS.md`** in this directory.

It includes things like:

- Core principles and architecture  
- Documentation style  
- Long section on **tool docstrings for agents**  
- Logging rules  
- Development commands  
- Testing patterns  
- Feature-add workflow  
- Debugging notes  

---

## Your task

### Step 1: Categorize each section (about 10–15 minutes)

Work section by section using the framework.

For each section:

**Q1:** Constant or task-specific?  
- Here, sections are mostly **constants** (stable project knowledge).  
- Nothing is “one-off task intel” that belongs only in Layer 2.

**Q2:** Needed every session?

Build three buckets:

#### Auto-load (keep in `AGENTS.md`)

“Needed in **every** session.”

- Used across many file types  
- Applies to most coding tasks  
- Would break conventions if the assistant did not know them  

#### On-demand (load when needed)

“Constants for a **specific task type**.”

- Only relevant when doing that kind of work  
- Stable pattern, but not always applicable  
- Example: only when creating or editing **agent tools**  

#### Redundant (remove or consolidate)

“Duplicate, obvious, or better documented elsewhere.”

- Repeats another section  
- Universal knowledge the model already has  
- Better in README or separate docs  

---

### Step 2: Write your analysis (about 10–15 minutes)

Create **`your-analysis.md`** in this folder (your AI assistant can help structure it):

```markdown
# My AGENTS.md analysis

## Auto-load (keep in AGENTS.md)

**Sections to keep:**
- [Section name]: [Why it is needed every session]
- ...

**Reasoning:**
[Your thinking]

## On-demand (load when needed)

**Sections to load on-demand:**
- [Section name]: [When you would load this / what triggers it]
- ...

**Reasoning:**
[Your thinking]

**How I would load these:**
[Slash command, rule, @-file, or short instruction in the prompt]

## Redundant (remove or consolidate)

**Sections to remove or merge:**
- [Section name]: [Why / where it should live instead]

**Reasoning:**
[Your thinking]

## Summary

**Original:** 600+ lines auto-loaded every session  
**After cleanup:** [X] lines auto-loaded, [Y] on-demand, [Z] removed  
**Approximate context savings:** [percentage]
```

---

## Hints

Ask yourself for each major block—**core principles**, **architecture**, **tool docstrings** (often hundreds of lines), **documentation style**, **logging**, **dev commands**, **testing**, **adding features**, **AI agent notes**—whether it belongs auto-loaded, on-demand, or is redundant with another section or the README.

---

## Optional reference material

This workshop standardizes on **`AGENTS.md`** at the repo root for project-wide agent rules. Some stacks use a different filename for the same role—use whatever your environment expects; the exercise is the same.

Under **`reference/`** you will find an example extracted guide that illustrates what **on-demand** files might look like after you split a big section out:

- `reference/adding_features_guide.md` — vertical-slice feature workflow  

Long sections you move out of `AGENTS.md` (for example detailed tool-docstring rules) would follow the same idea: a dedicated file under `reference/` loaded only when that work appears. You do **not** have to merge the sample guide into your analysis; it is support material.

---

## Takeaway

**Not everything belongs in auto-loaded project rules.**

The two-question framework helps you:

- Keep what is truly always needed  
- Move task-type constants to on-demand loading  
- Drop duplication and noise  

**Result:** A cleaner context window and faster, more focused assistance—without losing access to the long-form guidance when you need it.

---

## Facilitator note

An example categorization is under **`example-solution/SOLUTION.md`** for comparison only; learners can ignore that folder during the exercise.
