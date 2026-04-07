# Reference solution: `AGENTS.md` analysis

**Note:** This is one reasonable categorization. Some sections are debatable—the thinking process matters more than a single correct answer.

---

## Auto-load (keep in `AGENTS.md`)

### Sections to keep

1. **Project overview** (opening lines)  
   - **Why every session:** Frames the codebase and architecture for all work.  
   - **Applies to:** All files and tasks.

2. **Core principles**  
   - **Why every session:** Type safety, KISS, YAGNI apply to almost every change.  
   - **Applies to:** Every function and file.

3. **Architecture**  
   - **Why every session:** Vertical-slice layout affects where new code lives.  
   - **Applies to:** Structure and navigation.

4. **Documentation style**  
   - **Why every session:** Consistent docstrings across the codebase.  
   - **Applies to:** Most code you touch.

5. **Logging rules**  
   - **Why every session:** Logging conventions apply broadly; errors need consistent handling.  
   - **Applies to:** Operations, debugging, and “fix from logs” workflows.

6. **Development workflow commands**  
   - **Why every session:** Server, lint, typecheck, and tests are used often.  
   - **Trade-off:** Could live in README; many teams still keep a short copy in rules for convenience.

7. **Testing structure**  
   - **Why every session:** Tests mirror `src/`; important whenever you add or change code.  
   - **Applies to:** New files and refactors.

**Rough size after cleanup:** on the order of **200–250 lines** for the “always loaded” file, depending on how terse you keep each block.

**Reasoning:** These define foundations that apply across tasks. Without them in global rules, the assistant is more likely to violate project conventions.

---

## On-demand (load when needed)

### Sections to move out

1. **Tool docstrings for agents** (the very large section)  
   - **When:** Creating or modifying agent-facing tools.  
   - **Why on-demand:** Hundreds of lines only relevant for that task type.  
   - **Trigger:** e.g. “Add a new tool”, “Improve tool docstrings for X”.  
   - **Savings:** This one block is most of the bloat.

2. **Adding features** (step-by-step slice workflow)  
   - **When:** Adding a new feature slice, not small bugfixes or docs-only edits.  
   - **Why on-demand:** Stable process, but not every session.  
   - **Note:** Reasonable people disagree—some keep a short version in global rules. Grey areas are normal.

**See also:** `../reference/adding_features_guide.md` as an example of an extracted on-demand doc. A long tool-docstring section would be extracted the same way into its own `reference/*.md` file.

**How to load on demand**

- **@ mention** the guide file in your AI tool when starting that kind of work.  
- **Reusable prompt** (“Read `reference/<your-guide>.md`, then…”).  
- **Short workspace rule** that says: when editing tools, attach the tools guide.

**Reasoning:** These are stable Layer-1-style knowledge, but scoped to a **task type**, not every keystroke.

---

## Redundant (remove or consolidate)

### Candidate: “AI agent notes” (debugging bullets)

- **Why redundant:** Often repeats points already covered under logging (correlation IDs, `duration_ms`, stack traces).  
- **Action:** Remove or fold any *unique* nuggets into **Logging rules** so there is a single source of truth.

**Reasoning:** Duplication increases maintenance and confusion.

---

## Summary

| | Lines (approx.) |
|---|-----------------|
| **Original** | ~600 auto-loaded every time |
| **After** | ~160–250 auto-loaded; large blocks on-demand; small redundant slice removed |
| **Effect** | Much smaller default context; long guidance still available when needed |

### Debatable areas

- **Dev commands:** Auto-load vs README-only is a judgment call (frequency vs duplication).  
- **Documentation style:** Some teams on-demand it if they rarely write new public APIs.

---

## Applying this in your own project

Ask:

1. What is **your** “tool docstrings” equivalent—one huge section that rarely applies?  
2. What is truly **universal** for your repo?  
3. What duplicates **README** or other docs?  
4. What do you use **every session** vs **monthly**?

Strategic loading keeps default context small while preserving depth where it matters.
