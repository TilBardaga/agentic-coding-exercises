# Preparation — Agentic Coding Workshop

Welcome! We are looking forward to hosting you for the Agentic Coding Workshop. It is going to be a hands-on, practical session where you will experience firsthand how structured AI-assisted coding changes the way you work.

To make sure we can hit the ground running, please take **15–20 minutes** to prepare the following.

---

## 1. Clone the workshop repo

All exercises, instructions, and agent commands live here:

**https://github.com/TilBardaga/agentic-coding-exercises**

```bash
git clone https://github.com/TilBardaga/agentic-coding-exercises.git
```

Open the repo in Cursor and have a look around if you like — the [`README.md`](README.md) walks you through the full structure. No need to study it in advance, but it is there if you are curious.

---

## 2. Install Cursor and log in

We will be using **Cursor** as our AI coding assistant during the workshop. Make sure you have:

- [ ] Cursor installed — https://cursor.sh/
- [ ] Logged in with an active account
- [ ] Verified it works — open the cloned repo in Cursor and check that the AI chat is available

If you already use a different AI assistant (Claude Code, GitHub Copilot, etc.) and strongly prefer it, that works too — the exercises are assistant-agnostic. But our demos and walkthroughs will use Cursor.

---

## 3. Install the required tools

The workshop uses a small full-stack app (Python backend + React frontend). You need these tools installed:

- **Python 3.10+**
- **uv** (Python package manager)
- **Node.js LTS + npm**
- **Bun** (JavaScript runtime)
- **Git**

The repo has a detailed setup guide at [`setup/README.md`](setup/README.md) with installation instructions for Mac, Windows, and Linux.

You can also let Cursor handle the installation — paste this into the Cursor chat:

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

All five commands should print a version number. If any says "command not found", check the [setup guide](setup/README.md) or ask Cursor for help.

---

## 4. Prepare for Exercise 4 — your own project

In the final part of the workshop, you will apply the workflow to **your own codebase**. To make the most of that time:

- [ ] **Pick a project** you would like to work on — something you are actively developing or maintaining
- [ ] **Have it running** on your machine before you arrive (or ready to spin up in Docker)
- [ ] **Think about a task** — a refactor, a legacy page to modernize, a small feature, a bug to fix. Nothing big — something you can make meaningful progress on in 30–45 minutes

This does not need to be production-critical or complex. A side project, a module you have been meaning to clean up, or even "that one file everyone is afraid to touch" — all great options.

---

## What to expect

The workshop is **4 hours**, fully hands-on:

| Part | What you do |
|------|------------|
| **Exercise 1** | Build a feature with AI the way you normally would (your baseline) |
| **Exercise 2** | Build the same feature with a structured Plan-Implement-Validate loop |
| **Exercise 3** | Use pre-built agent commands for the full workflow (planning, implementation, code review, retrospectives) |
| **Exercise 4** | Apply everything to your own project |

You will build the same product filtering feature three times (Exercises 1–3) to feel the difference between approaches — then take the workflow to your own code. There will be short Q&A rounds between exercises.

---

## Quick checklist

- [ ] Repo cloned — `git clone https://github.com/TilBardaga/agentic-coding-exercises.git`
- [ ] Cursor installed and logged in
- [ ] Tools installed — Python 3.10+, uv, Node.js, Bun, Git (all print a version number)
- [ ] Own project ready for Exercise 4

If you run into any issues with the setup, do not hesitate to reach out — we are happy to help before the workshop so we can spend our time together on the actual exercises.

See you there!

**Dennis Claassen & Joppe van der Schoot**
