# Agentic Coding Workshop — Preparation Guide

Welcome! We are looking forward to hosting you for the Agentic Coding Workshop. This is a hands-on, practical session where you will experience firsthand how structured AI-assisted coding changes the way you work. No slides, no theory dumps — you will be coding from the start.

Please take **20–30 minutes before the workshop** to go through this guide. Everything you set up now is time we do not lose during the session. If you get stuck on any step, reach out — we are happy to help before the workshop so we can spend our time together on the actual exercises.

---

## What to expect

The workshop is **4 hours**, fully hands-on. Here is what we will do:

| Part | What you do | Duration |
|------|------------|----------|
| **Exercise 1** | Build a feature with AI the way you normally would — your baseline | ~45 min |
| **Exercise 2** | Build the same feature with a structured Plan-Implement-Validate loop | ~45 min |
| **Exercise 3** | Use pre-built agent commands for the full workflow (planning, implementation, code review, retrospectives) | ~90 min |
| **Exercise 4** | Apply everything to your own project | ~30 min |

You will build the same product filtering feature three times (Exercises 1–3) to feel the difference between approaches — then take the workflow to your own code. There will be short Q&A rounds between exercises where we share experiences and insights.

**Why the same feature three times?** So you can compare apples to apples. The only thing that changes is _how_ you work. By the end, you will have concrete data on which approach gives you more control, better output, and higher confidence.

---

## Step 1 — Install Cursor

We will be using **Cursor** as our AI coding assistant during the workshop.

1. Download and install Cursor from https://cursor.sh/
2. Open Cursor, sign in, and make sure the AI chat works (Ctrl+L / Cmd+L to open the chat panel)
3. If prompted, choose a model — any will work for the workshop

> **Already using a different assistant?** The exercises are designed for Cursor, but the concepts work with any AI coding assistant (Claude Code, GitHub Copilot, Aider, etc.). Our demos and walkthroughs will use Cursor, so following along will be easiest if you use it too.

---

## Step 2 — Clone the workshop repo

All exercises, instructions, and agent commands live in one repo. Clone the **cursor** branch — this is the version optimized for Cursor:

```bash
git clone -b cursor https://github.com/TilBardaga/agentic-coding-exercises.git
```

Open the cloned folder in Cursor. You should see exercise folders (`exercise-1/` through `exercise-4/`), a `.cursor/` folder with agent commands, and this preparation guide.

---

## Step 3 — Install the required tools

The workshop uses a small full-stack app (Python backend + React frontend). You need the following tools installed and working:

- **Python 3.10+**
- **uv** (Python package manager)
- **Node.js LTS + npm**
- **Bun** (JavaScript runtime)
- **Git**

### Option A — Let Cursor handle it

Open the cloned repo in Cursor and paste this into the AI chat:

```
I need to set up my development environment for this workshop.
Check which of these tools are installed and install anything that is missing:

- Python 3.10+
- uv (Python package manager — https://docs.astral.sh/uv/)
- Node.js LTS + npm
- Bun (JavaScript runtime — https://bun.sh/)
- Git

After installing, run these verification commands and show me the output:

python3 --version
uv --version
node --version
bun --version
git --version
```

Cursor will check what is already installed, install what is missing, and verify everything works. If it hits a permissions issue, it will tell you what to run manually.

> This is your first taste of agentic workflow — instead of following manual steps for each tool, you give the AI a clear goal and let it figure out the details. You will do the same with code throughout the workshop.

### Option B — Install manually

<details>
<summary><strong>Python 3.10+</strong></summary>

**macOS / Windows:** Download and run the installer from https://www.python.org/downloads/

> On Windows: enable **"Add Python to PATH"** during installation!

**Linux:** Python is often pre-installed. Check with `python3 --version`.

Verify: `python3 --version` should show 3.10 or higher.

More info: [Official Python downloads](https://www.python.org/downloads/)

</details>

<details>
<summary><strong>uv (Python package manager)</strong></summary>

**macOS / Linux:**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows (PowerShell):**
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Alternative (Homebrew):**
```bash
brew install uv
```

Verify: `uv --version`

More info: [Official uv installation guide](https://docs.astral.sh/uv/getting-started/installation/)

</details>

<details>
<summary><strong>Node.js LTS + npm</strong></summary>

Download the LTS version from https://nodejs.org/ — npm is included automatically.

**Alternative (macOS — Homebrew):**
```bash
brew install node
```

**Alternative (Windows — Chocolatey):**
```bash
choco install nodejs
```

Verify: `node --version` and `npm --version`

More info: [Official Node.js downloads](https://nodejs.org/en/download/)

</details>

<details>
<summary><strong>Bun (JavaScript runtime)</strong></summary>

**macOS / Linux:**
```bash
curl -fsSL https://bun.sh/install | bash
```

**macOS (Homebrew):**
```bash
brew install oven-sh/bun/bun
```

**Windows (PowerShell):**
```powershell
powershell -c "irm bun.sh/install.ps1 | iex"
```

Verify: `bun --version`

More info: [Official Bun installation guide](https://bun.sh/docs/installation)

</details>

<details>
<summary><strong>Git</strong></summary>

**macOS:** Usually pre-installed. Run `git --version` — if not installed, you will be prompted to install Xcode Command Line Tools. Or: `brew install git`

**Windows:** Download from https://git-scm.com/download/win

**Linux (Ubuntu/Debian):** `sudo apt install git-all`

**Linux (Fedora/RHEL):** `sudo dnf install git-all`

Verify: `git --version`

More info: [Official Git installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

</details>

### Verify everything works

Run all five commands — each should print a version number:

```bash
python3 --version    # 3.10 or higher
uv --version         # any version
node --version       # any version
bun --version        # any version
git --version        # any version
```

**Seeing "command not found"?** Restart your terminal and try again. If it still fails, ask Cursor — it is usually faster at diagnosing PATH issues than scrolling through docs.

---

## Step 4 — Download dependencies ahead of time

During the workshop, everyone will be on the same network. Downloading dependencies with 15+ people at once can be painfully slow. Save yourself (and everyone else) time by installing them now, while you are on your own internet:

**Option A — Let Cursor handle it:**

```
Install all dependencies for exercises 1, 2, and 3 in this workshop repo.
For each exercise:
- Backend: cd exercise-N/app/backend, run uv venv --python 3.12, then uv sync
- Frontend: cd exercise-N/app/frontend, run bun install
Do this for exercise-1, exercise-2, and exercise-3.
```

**Option B — Run it yourself:**

```bash
# From the root of the cloned repo:

# Backend dependencies
cd exercise-1/app/backend && uv venv --python 3.12 && uv sync && cd ../../..
cd exercise-2/app/backend && uv venv --python 3.12 && uv sync && cd ../../..
cd exercise-3/app/backend && uv venv --python 3.12 && uv sync && cd ../../..

# Frontend dependencies
cd exercise-1/app/frontend && bun install && cd ../../..
cd exercise-2/app/frontend && bun install && cd ../../..
cd exercise-3/app/frontend && bun install && cd ../../..
```

---

## Step 5 — Prepare for Exercise 4 (your own project)

In the final part of the workshop, you will apply the workflow to **your own codebase**. This is where you take the techniques from the workshop and use them on real work. To make the most of that time, prepare before the workshop starts:

- [ ] **Pick a project** you would like to work on — something you are actively developing or maintaining
- [ ] **Have it ready to run** on your machine before the workshop. If it needs Docker, make sure the containers build and start. If it needs a database, have it seeded. Do not wait until exercise 4 to discover that your dev environment is broken.
- [ ] **Think about a task** — a refactor, a legacy page to modernize, a small feature, a bug to fix. Nothing big — something you can make meaningful progress on in 30–45 minutes

This does not need to be production-critical or complex. A side project, a module you have been meaning to clean up, or even "that one file everyone is afraid to touch" — all great options. The point is to have something real to work with, not something perfect.

> **Using Docker?** Make sure `docker compose up` (or however you start your project) works before the workshop. Pull all images beforehand — you do not want to be downloading 2 GB of container images over shared wifi.

---

## Step 6 — Read ahead (optional)

If you want to hit the ground running, you can browse the workshop materials before we start. None of this is required — we will walk through everything together — but it can help you feel oriented.

- **[`README.md`](README.md)** — The main workshop guide. Explains the structure, how exercises connect, and what you will build.
- **[`exercise-1/README.md`](exercise-1/README.md)** — The first exercise. Reading it gives you a feel for what the assignments look like.
- **[`.cursor/commands/`](.cursor/commands/)** — The agent command files used in Exercise 3. These are markdown files that instruct Cursor how to plan, implement, and review code. Browsing them gives you a sense of what "operationalized AI workflow" looks like in practice.

Do not worry about understanding everything — the exercises are designed to guide you step by step.

---

## Practical tips

**Internet bandwidth** — The workshop involves AI assistants, package downloads, and (for remote participants) video streaming. If you are on-site, be aware that shared wifi with 15+ developers running AI assistants can get slow. Having dependencies pre-installed (Step 4) and your own project ready (Step 5) avoids the worst bottlenecks.

**Screen setup** — You will be switching between your IDE, a browser (to test the app), and the workshop materials. Two monitors make this much smoother. If you only have one screen, consider using split-screen or virtual desktops.

**Terminals** — Each exercise needs two terminal windows (one for the backend server, one for the frontend). Having a terminal app that supports tabs or splits will save you time.

---

## If you are joining remotely

The workshop is interactive — we will be sharing screens, discussing approaches, and doing Q&A rounds between exercises. To get the most out of it:

- **Camera on** — it makes a real difference for group discussions. We want to see your reactions, not a grid of black squares.
- **Stable internet** — you will be streaming video and running an AI assistant simultaneously. If your connection is unreliable, do all the preparation steps over a wired connection beforehand so you are not downloading anything during the session.
- **Two screens strongly recommended** — one for the video call, one for your IDE. Working on a single screen with a video call and an IDE is possible but frustrating.
- **Headset with mic** — for clear audio during Q&A. Laptop speakers and microphones tend to cause echo and feedback.

---

## Quick checklist

Before the workshop starts, make sure you can check all of these:

- [ ] Cursor installed and logged in (AI chat works)
- [ ] Repo cloned — `git clone -b cursor https://github.com/TilBardaga/agentic-coding-exercises.git`
- [ ] Tools installed — `python3`, `uv`, `node`, `bun`, `git` all print a version number
- [ ] Dependencies pre-installed — `uv sync` and `bun install` done for exercises 1–3
- [ ] Own project ready for Exercise 4 (builds, starts, and runs)
- [ ] Task in mind for Exercise 4 (refactor, feature, cleanup, etc.)

**Everything green? You are ready.** See you at the workshop!

**Dennis Claassen & Joppe van der Schoot**
