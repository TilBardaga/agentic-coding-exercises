# Agentic Coding Workshop

Welcome to the **Agentic Coding Workshop**. This guide walks you through the entire training from start to finish. Bookmark it — you can always come back here to see where you are and what to do next.

---

## What this workshop is about

You will build the **same feature** three times: product catalog filtering for a small e-commerce app (FastAPI backend + React frontend). Each time, you use a different level of structure with your AI coding assistant:

| Exercise | Approach | What you learn |
|----------|----------|----------------|
| **1 — Baseline** | Work however you normally would | Measure your starting point: speed, confidence, control |
| **2 — PIV loop** | Plan → Implement → Validate | Feel the difference when you add structure |
| **3 — Commands** | Use pre-built agent commands (`/prime`, `/plan`, `/implement`, reviews) | See what a fully operationalized workflow looks like |
| **4 — Your own codebase** | Apply the workflow to your own project | Take it from workshop to real world |

**Exercises 1–3** use the same feature built three times so you can compare apples to apples. The codebase is identical at the start of each — a fresh starting point every time. **Exercise 4** is where you take the workflow to your own code.

---

## Before you begin

### 1. Install required tools

Follow **[`setup/README.md`](setup/README.md)** to install Python, uv, Node.js, Bun, and Git.

The setup guide offers two approaches:
- **Option A — AI-first:** Paste a prompt into your AI assistant and let it install everything for you. This is a great warm-up for the workshop.
- **Option B — Manual:** Follow traditional step-by-step instructions for each tool.

Both get you to the same place. Pick whichever you prefer.

### 2. Verify everything works

Open a terminal and run:

```bash
python3 --version    # 3.10 or higher
uv --version         # any version
node --version       # any version
bun --version        # any version
git --version        # any version
```

All five commands should print a version number. If any says "command not found", go back to the setup guide for that tool.

### 3. Open the repo in your IDE

Open the **root folder** of this repository in your editor (VS Code, Cursor, or whichever IDE you use). You will navigate into each `exercise-*/` folder from here.

---

## The demo app

Every exercise contains the **same starting app** — a small e-commerce product catalog. The app has two parts:

- **Backend** (FastAPI / Python) — an API that serves 30 products from an in-memory list. Right now it has one endpoint (`GET /api/products`) that returns all products without filtering.
- **Frontend** (React / TypeScript) — a UI that shows the products in a grid. No filter controls exist yet.

Your job across all exercises is to **add filtering**: price range, category, keyword search, and sorting. The backend tests already define the exact API contract — they are just skipped until you implement the feature.

### Starting the app

Every exercise uses the same commands. You always need **two terminal windows** — one for the backend, one for the frontend:

```bash
# Terminal 1 — Backend (from exercise-*/app/backend/)
uv venv --python 3.12
uv sync
uv run python run_api.py          # → http://localhost:8000
```

```bash
# Terminal 2 — Frontend (from exercise-*/app/frontend/)
bun install
bun dev                            # → http://localhost:3000
```

> **Tip:** Stop any running servers before starting the next exercise, otherwise you will get "port already in use" errors.

---

## Exercise 1 — Baseline

**Goal:** Build catalog filtering the way you normally would with AI. No rules, no special process — just you and your assistant. This is your measurement point.

### What you will find in the folder

```
exercise-1/
├── README.md                      ← the assignment (start here)
└── app/
    ├── backend/
    │   ├── app/
    │   │   ├── api/products.py            ← the API endpoint (you will edit this)
    │   │   ├── services/product_service.py ← business logic (you will edit this)
    │   │   ├── models/product.py          ← Pydantic models
    │   │   └── data/seed_products.py      ← 30 sample products (do not edit)
    │   ├── tests/
    │   │   ├── test_products_basic.py     ← baseline tests (already passing)
    │   │   └── test_products_filtering.py ← filtering tests (all skipped — your goal is to make them pass)
    │   ├── run_api.py                     ← starts the backend server
    │   └── pyproject.toml                 ← Python dependencies
    └── frontend/
        ├── src/
        │   ├── App.tsx                    ← main app component
        │   ├── components/ProductGrid.tsx ← product list (you will add filter UI here)
        │   └── lib/api-client.ts          ← API calls to the backend
        └── package.json                   ← frontend dependencies
```

### Steps

1. Read the assignment: **[`exercise-1/README.md`](exercise-1/README.md)**
2. Start the backend and frontend (see [Starting the app](#starting-the-app) above)
3. Implement the filtering feature using AI however feels natural
4. Validate: run `uv run pytest` from `exercise-1/app/backend/` — the skipped tests should now pass, and filters should work in the browser
5. **Write down** your time, number of prompts, confidence level, and any moments where you lost control — you will compare these in Exercise 2

**Done?** Move on to Exercise 2.

---

## Exercise 2 — PIV loop

**Goal:** Build the exact same feature, but this time with a structured **Plan → Implement → Validate** loop. Notice the difference compared to your baseline.

### What you will find in the folder

```
exercise-2/
├── README.md                      ← the assignment (start here)
└── app/                           ← identical starting code as exercise-1 (fresh, unimplemented)
    ├── backend/                   ← same structure as exercise-1
    └── frontend/                  ← same structure as exercise-1
```

The `app/` folder is a **fresh copy** — the same unimplemented starting point as Exercise 1. This is intentional so you can compare results fairly.

### Steps

1. Read the assignment: **[`exercise-2/README.md`](exercise-2/README.md)** — it contains the full ticket specs and the PIV instructions
2. Start the backend and frontend (see [Starting the app](#starting-the-app) above, but from `exercise-2/`)
3. **Plan:** Write a detailed implementation plan before touching any code. Include what you will change, in what order, and how you will validate
4. **Implement:** Build the feature with your plan as context for the AI
5. **Validate:** Run `uv run pytest`, check the UI, iterate if needed
6. **Compare with Exercise 1:** Was it smoother? Did you feel more in control? Did the AI produce better output with a plan?

**Done?** Move on to Exercise 3.

---

## Exercise 3 — Commands, reviews, meta, capstone

**Goal:** Use pre-built agent commands to run a full professional workflow. This is the longest exercise — five parts that build on each other.

### What you will find in the folder

```
exercise-3/
├── README.md                      ← detailed workflow guide (read this first)
├── CHANGELOG.md                   ← you will add entries here as you complete parts
├── tasks/
│   ├── exercise-3.1.md            ← part 1: prime, plan, implement
│   ├── exercise-3.2.md            ← part 2: code review + fix
│   ├── exercise-3.3.md            ← part 3: execution report, system review, docs
│   ├── exercise-3.4.md            ← part 4: repository abstraction refactor
│   └── exercise-3.5.md            ← part 5: free-form feature
├── docs/
│   ├── DOC_INDEX.md               ← navigation hub for all exercise-3 docs
│   ├── CODEBASE_MAP.md            ← map of what lives where (you update this)
│   └── ARCHITECTURE.md            ← architecture overview (you update this)
└── app/                           ← same fresh starting code as exercises 1 and 2
```

There are also folders **outside** `exercise-3/` that you will use:

```
.agents/                           ← the agent command library
├── commands/
│   ├── prime.md                   ← /prime — loads repo context
│   ├── plan.md                    ← /plan — writes a dev-plan.md
│   ├── implement.md               ← /implement — executes the plan
│   ├── code-review.md             ← /code-review — reviews your changes
│   ├── code-review-fix.md         ← /code-review-fix — fixes review findings
│   ├── execution-report.md        ← /execution-report — plan vs reality
│   └── system-review.md           ← /system-review — process retrospective
└── rules/                         ← coding conventions (loaded automatically by commands)
    └── 01-…06-*.mdc               ← architecture, style, testing, security, debugging, docs

docs/agent-jobs/                   ← where /plan writes its output
└── <your-job-name>/
    ├── dev-plan.md                ← created by /plan
    ├── code-review.md             ← created by /code-review
    ├── execution-report.md        ← created by /execution-report
    └── system-review.md           ← created by /system-review
```

> **Note:** The `docs/agent-jobs/` folder already contains some example job artifacts from the facilitators. These are for reference — your jobs will be created alongside them.

### How to use agent commands

The commands are markdown files in `.agents/commands/`. You feed them to your AI assistant:

- **Cursor:** Type `@` in the chat input, navigate to `.agents/commands/prime.md` (or whichever command), select it, then press Enter. The AI reads the command file and follows its instructions.
- **Other assistants:** Open the command file, copy its content into your chat, and let the AI execute it.

### Parts 3.1 through 3.5

Work through these **in order**. Each part has a "done when" checklist — check all boxes before moving on.

| Part | What you do | Assignment | Chat session |
|------|------------|------------|--------------|
| **3.1** | `/prime` → `/plan` → `/implement` for filtering | [`tasks/exercise-3.1.md`](exercise-3/tasks/exercise-3.1.md) | Start a **new** chat |
| **3.2** | `/code-review` → `/code-review-fix` | [`tasks/exercise-3.2.md`](exercise-3/tasks/exercise-3.2.md) | **Same** chat as 3.1 |
| **3.3** | `/execution-report` → `/system-review`, update docs | [`tasks/exercise-3.3.md`](exercise-3/tasks/exercise-3.3.md) | **Same** chat as 3.1 |
| **3.4** | Repository abstraction refactor | [`tasks/exercise-3.4.md`](exercise-3/tasks/exercise-3.4.md) | **New** chat |
| **3.5** | Free-form feature of your choice | [`tasks/exercise-3.5.md`](exercise-3/tasks/exercise-3.5.md) | **New** chat |

**Why different chat sessions?** Parts 3.1–3.3 are one continuous flow on the same feature — the AI benefits from keeping the plan, code, and review in context. Parts 3.4 and 3.5 are separate features, so a fresh chat avoids context pollution.

---

## Exercise 4 — Your own codebase

**Goal:** Apply the workflow to your own project. No workshop app, no prescribed feature — just you, your codebase, and the patterns you have learned.

### What to do

1. Read the guide: **[`exercise-4/README.md`](exercise-4/README.md)** — it has setup instructions, practice ideas, and the core principles distilled
2. Pick something from your own work — a refactor, a legacy page, a small feature, anything
3. Use the workflow: plan before you code, validate after, review when done

There are no required tasks and no checklist. The exercise is about making the workflow yours.

---

## Quick reference — agent commands

These are used in Exercises 3 and 4. You do not need them for Exercises 1 or 2.

| Command | What it does | Output |
|---------|-------------|--------|
| `/prime` | Loads repo context into the AI's memory | (no file — context stays in chat) |
| `/plan` | Creates a detailed implementation plan | `docs/agent-jobs/<job>/dev-plan.md` |
| `/implement` | Executes the plan, follows the checklist | code changes in `exercise-3/app/` |
| `/code-review` | Reviews your changes | `docs/agent-jobs/<job>/code-review.md` |
| `/code-review-fix` | Fixes issues found in the review | code changes |
| `/execution-report` | Compares plan vs what actually happened | `docs/agent-jobs/<job>/execution-report.md` |
| `/system-review` | Process retrospective — what to improve | `docs/agent-jobs/<job>/system-review.md` |

Commands not used in this workshop: `/finish` (commit) and `/push` (publish). These exist in `.agents/commands/` for use in your own projects after the training.

---

## Folders you can ignore

| Folder | What it is | Do you need it? |
|--------|-----------|-----------------|
| `.agents/rules/` | Coding conventions that the AI follows automatically | **No action needed.** These are loaded by the commands in Exercise 3. You can read them if you are curious. |
| `AGENTS.md` (root) | A thin "constitution" that points the AI to the rules | **No action needed.** Used by the commands behind the scenes. |

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `bun: command not found` | Install Bun — see [`setup/README.md`](setup/README.md) step 4 |
| `uv: command not found` | Install uv — see [`setup/README.md`](setup/README.md) step 2 |
| Backend won't start | Make sure you ran `uv venv --python 3.12` and `uv sync` first |
| Frontend won't start | Make sure you ran `bun install` first |
| Tests fail before you changed anything | Run `uv run pytest` from the exercise's `app/backend/` folder — the filtering tests are **skipped** by default, that is expected |
| CORS errors in browser | Make sure backend runs on port 8000 and frontend on port 3000 |
| AI assistant doesn't see the right files | Scope your assistant to the current exercise's `app/` folder |
| Port already in use | You probably have another exercise's server still running — stop it first |
| `@` command file not found in Cursor | Make sure you opened the **repo root** in your IDE, not just the exercise folder |

---

## Need help?

- Check the [troubleshooting section](#troubleshooting) above
- During the workshop, ask **Dennis Claassen** or **Joppe van der Schoot**
