# Exercise 3 — Agent commands

In Exercises 1 and 2 you experienced the difference between unstructured and structured AI-assisted coding. You learned that planning before coding gives you more control and better results. But you also did a lot of that work manually — writing prompts, reviewing output, deciding what to validate.

In this exercise, that entire workflow is **operationalized**. Instead of crafting prompts yourself, you use pre-built **agent commands** that handle priming, planning, implementation, code review, and retrospectives. The commands encode the best practices you have been learning — but in a repeatable, consistent format.

**What changes:** You are no longer writing prompts from scratch. The commands do the prompting. Your job shifts to steering the process: picking the right command at the right time, reviewing what comes out, and deciding what to do next.

**What stays the same:** You are still the architect. The AI still builds what you tell it to. The difference is that the instructions are now codified — which means they work the same way every time, and you can improve them over time.

---

## How this exercise is structured

Exercise 3 has **five parts** that build on each other. You will work through them in order.

| Part | What you do | Assignment |
|------|------------|------------|
| **3.1** | Prime, plan, implement — ship the filtering feature | [`tasks/exercise-3.1.md`](tasks/exercise-3.1.md) |
| **3.2** | Code review and fix — improve what you built | [`tasks/exercise-3.2.md`](tasks/exercise-3.2.md) |
| **3.3** | Execution report, system review, update docs — reflect on the process | [`tasks/exercise-3.3.md`](tasks/exercise-3.3.md) |
| **3.4** | Repository abstraction — a backend refactor using the full cycle | [`tasks/exercise-3.4.md`](tasks/exercise-3.4.md) |
| **3.5** | Free feature — pick something and run the full workflow yourself | [`tasks/exercise-3.5.md`](tasks/exercise-3.5.md) |

**Parts 3.1–3.3** are one continuous flow on the same feature. Keep them in the **same chat session** — the assistant benefits from having the plan, code changes, and review history all in context.

**Parts 3.4 and 3.5** are separate features. Start a **new chat** for each one to avoid context pollution from earlier work.

---

## Step 1 — Start a fresh instance

Stop any servers still running from Exercise 2 and start fresh from the `exercise-3/` folder. This is a new exercise with a clean copy of the app.

**Option A — Let your assistant handle it:**

```
Stop any servers from previous exercises (kill processes on ports 8000 and
3000). Then start a fresh dev environment for exercise-3:

Backend (from exercise-3/app/backend/):
- uv venv --python 3.12
- uv sync
- uv run python run_api.py

Frontend (from exercise-3/app/frontend/):
- bun install
- bun dev

These must run from the exercise-3 folder, not exercise-1 or exercise-2.
Verify both are running and tell me when ready.
```

**Option B — Do it yourself.** Stop your old servers (Ctrl+C in each terminal window), then:

```bash
# Terminal 1 — Backend (from exercise-3/)
cd app/backend
uv venv --python 3.12
uv sync
uv run python run_api.py
# → http://localhost:8000
```

```bash
# Terminal 2 — Frontend (from exercise-3/)
cd app/frontend
bun install
bun dev
# → http://localhost:3000
```

Verify the app loads at http://localhost:3000 before moving on.

---

## Step 2 — Understand the agent commands

Before you start using the commands, it helps to know what they do and why they exist. Each command is a markdown file in `.agents/commands/` that contains detailed instructions for the AI. You do not need to read the full files — here is what each one does:

### The technical cycle (you will use these in every part)

| Command | What it does | What it produces |
|---------|-------------|-----------------|
| **`/prime`** | Scans the codebase and builds context — file structure, patterns, conventions, recent changes. Think of it as onboarding your assistant to the repo before it starts working. | Context in the chat (no file output) |
| **`/plan`** | Takes a feature request and turns it into a detailed, phased implementation plan. Maps the codebase, identifies affected files, sequences the work, flags risks. | `docs/agent-jobs/<job>/dev-plan.md` |
| **`/implement`** | Executes an approved plan. Follows the checklist, applies conventions, validates as it goes. | Code changes + updated checklist in dev-plan.md |
| **`/code-review`** | Reviews your recent changes for defects — logic errors, security issues, code smells, naming, duplication. | `docs/agent-jobs/<job>/code-review.md` |
| **`/code-review-fix`** | Fixes the issues found in the code review. | Code changes |

### The meta cycle (used in 3.3, optional in 3.4 and 3.5)

| Command | What it does | What it produces |
|---------|-------------|-----------------|
| **`/execution-report`** | Compares what you planned to what actually happened. Documents divergences, surprises, and what you learned. | `docs/agent-jobs/<job>/execution-report.md` |
| **`/system-review`** | Analyzes your process — not your code. Finds patterns in what went wrong and proposes improvements to the workflow itself. | `docs/agent-jobs/<job>/system-review.md` |

### How to use a command

The commands are markdown files. You feed them to your AI assistant:

- **Cursor:** Type `@` in the chat input, navigate to `.agents/commands/prime.md` (or whichever command), select it, and press Enter. The assistant reads the file and follows its instructions.
- **Other assistants:** Open the command file, copy its content into your chat, and let the assistant execute it.

Some commands need input (a job name, a path). The task files for each part will tell you exactly what to provide.

---

## Step 3 — Work through parts 3.1 to 3.5

Each part has its own task file with specific instructions. Read the task file for the part you are working on — it will tell you which commands to run, in what order, and what to look for.

### Part 3.1 — Prime, plan, implement

**[`tasks/exercise-3.1.md`](tasks/exercise-3.1.md)**

You will build the same filtering feature as Exercises 1 and 2, but this time using `/prime` → `/plan` → `/implement`. The command handles the prompt engineering — your job is to review the plan before approving implementation.

This is the same PIV loop from Exercise 2, but operationalized. Notice how the `/plan` command produces a more structured, more thorough plan than what you wrote manually — and how `/implement` follows that plan systematically.

### Part 3.2 — Code review and fix

**[`tasks/exercise-3.2.md`](tasks/exercise-3.2.md)**

Stay in the **same chat** as 3.1. Run `/code-review` on what you just built, then `/code-review-fix` to address the findings. This is the quality gate — the step that catches code smells, edge cases, and technical debt before they ship.

### Part 3.3 — Execution report, system review, docs

**[`tasks/exercise-3.3.md`](tasks/exercise-3.3.md)**

Still the **same chat**. Step back and reflect: run `/execution-report` to compare plan vs. reality, then `/system-review` to analyze your process. Update the project docs to reflect what you built. This is the meta layer — learning from the work, not just doing the work.

### Part 3.4 — Repository abstraction

**[`tasks/exercise-3.4.md`](tasks/exercise-3.4.md)**

**New chat.** A backend refactor: introduce a repository layer to separate data access from business logic. Run the full technical cycle: `/prime` → `/plan` → `/implement` → `/code-review` → `/code-review-fix`. This is where the workflow becomes second nature.

### Part 3.5 — Free feature (capstone)

**[`tasks/exercise-3.5.md`](tasks/exercise-3.5.md)**

**New chat.** Pick a small feature, run the full cycle yourself. No hand-holding — you decide the scope, you run the commands, you own the outcome. This is the test of whether the workflow sticks.

---

## Reference

### Folder structure

```
exercise-3/
├── README.md              ← you are here
├── CHANGELOG.md           ← add entries as you complete parts
├── tasks/                 ← assignment for each part (3.1–3.5)
├── docs/
│   ├── DOC_INDEX.md       ← navigation hub for exercise-3 docs
│   ├── CODEBASE_MAP.md    ← map of what lives where (you update this)
│   └── ARCHITECTURE.md    ← architecture overview (you update this)
└── app/                   ← fresh starting code (same as exercises 1 and 2)
```

Folders outside `exercise-3/` that you will use:

```
.agents/
├── commands/              ← the agent command files (do not modify)
│   ├── prime.md
│   ├── plan.md
│   ├── implement.md
│   ├── code-review.md
│   ├── code-review-fix.md
│   ├── execution-report.md
│   └── system-review.md
└── rules/                 ← coding conventions (loaded automatically by commands)

docs/agent-jobs/           ← where commands write their output
└── <your-job-name>/
    ├── dev-plan.md
    ├── code-review.md
    ├── execution-report.md
    └── system-review.md
```

### Command definitions

The full command definitions live in `.agents/commands/`. You do not need to read them to use them — the task files tell you what to do — but if you are curious about what the AI is being told, they are there.

| Command | File |
|---------|------|
| `/prime` | [`.agents/commands/prime.md`](../.agents/commands/prime.md) |
| `/plan` | [`.agents/commands/plan.md`](../.agents/commands/plan.md) |
| `/implement` | [`.agents/commands/implement.md`](../.agents/commands/implement.md) |
| `/code-review` | [`.agents/commands/code-review.md`](../.agents/commands/code-review.md) |
| `/code-review-fix` | [`.agents/commands/code-review-fix.md`](../.agents/commands/code-review-fix.md) |
| `/execution-report` | [`.agents/commands/execution-report.md`](../.agents/commands/execution-report.md) |
| `/system-review` | [`.agents/commands/system-review.md`](../.agents/commands/system-review.md) |

Commands not used in this workshop: `/finish` (commit) and `/push` (publish). These exist for use in your own projects after the training.

---

## Done with all five parts?

If you have completed 3.1 through 3.5, you have run the full agentic coding workflow multiple times — from priming and planning through implementation, review, and retrospective. The patterns you practiced here are the same ones that work on real codebases, real teams, and real deadlines.

**What happens next:** Final Q&A round and wrap-up.
