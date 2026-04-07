# Exercise 1: Baseline implementation

## Overview

This is the first exercise in the Agentic Coding Workshop. Exercise 1 establishes your **personal baseline** for AI-assisted coding **before** you learn systematic techniques.

You implement product filtering in both the backend API and the frontend of a simple e-commerce product catalog (under `app/`), the way you would in a real project.

**Important**: This is a baseline, not a test. Use AI coding assistants however feels most natural. There are no rules, limits, or required ways to use AI tools—work the way you normally would.

## Quick start

Start the app in two terminals so you can explore it before you begin:

**Terminal 1 – Backend**:
```bash
cd app/backend
uv venv --python 3.12
uv sync
uv run python run_api.py
# → http://localhost:8000
```

**Terminal 2 – Frontend**:
```bash
cd app/frontend
npm install -g bun
bun install
bun dev
# → http://localhost:3000
```

## Goals

1. **Ship a full-stack feature** from backend to frontend
2. **Record your baseline** for time, effort, and confidence when using AI assistants
3. **Experience your current workflow** before optimization techniques in later exercises

**Note**: Your implementation will likely work—even with simple prompts—because AI assistants are strong enough for this scope. The project is intentionally simple because **the goal is not to fight working code**. Pay attention instead to:
- How smooth does the process feel?
- How much do you understand of what gets implemented?
- How much control do you have over the details?
- Are you driving, or just going along?

## The assignment

> Open your AI coding assistant scoped to the `app/` folder for this exercise!

The assignment has two parts; you can implement them together or in sequence:

### Part 1: Backend API filtering

Add filtering to the FastAPI backend:

- **Price filtering**: Min and max price query parameters
- **Category filtering**: Filter by product category
- **Keyword search**: Search in product names and descriptions
- **Sorting**: Sort by price or name (ascending and descending)

All filters must be optional and work when combined.

### Part 2: Frontend filter UI

Build a React UI that talks to your filtered API:

- **Price range controls**: Min/max price
- **Category selector**: Filter by category
- **Search field**: Keyword search
- **Sort controls**: Sort results
- **Filter actions**: Apply and clear filters

The UI should handle loading states, empty results, and validation errors cleanly.

### Use AI however you want

There are **no rules** on AI usage:

- **Work the way you would on a real task today**
- Use whatever prompting style comes naturally
- Ask for help, generation, debugging—whatever you need

## Project structure

```
exercise-1/
├── app/
│   ├── backend/      # FastAPI backend
│   │   ├── app/
│   │   │   ├── api/
│   │   │   ├── models/
│   │   │   ├── services/
│   │   │   └── ...
│   │   └── tests/    # Backend tests (keep them green!)
│   └── frontend/     # React frontend
│       └── src/
│           ├── components/
│           ├── lib/
│           └── types/
```

## What to track

While you work, track:

### ⏱️ Time

- **Backend time**: How long to implement the API changes?
- **Frontend time**: How long to build the UI?
- **Total time**: End-to-end duration

### 💬 AI interaction

- **Number of prompts**: How often did you invoke the assistant?
- **Types of requests**: Generation? Debugging? Explanation?
- **Iterations**: How many back-and-forth rounds?

### 😊 Confidence

After finishing, rate your confidence (1–10):

- How sure are you the code is **correct**?
- How sure are you it follows **best practices**?
- How well do you **understand** the generated code?
- How **maintainable** is the result?

### 🐛 Issues

- Did the AI make mistakes? What kind?
- Did you debug generated code?
- Type errors or failing tests?
- How much manual fixing was needed?

## Success criteria

You’re done when:

- ✅ All backend tests pass (`uv run pytest`)
- ✅ The API accepts and applies filter parameters correctly
- ✅ The frontend shows a working filter UI
- ✅ Filters apply and results update accordingly
- ✅ You can manually exercise the full flow in the browser

## Important notes

### This is not a competition

The goal is **your personal baseline**, not beating others. Be honest about:

- Time spent (no rushing!)
- Prompts used (keep a log)
- Confidence levels (be realistic)
- Problems hit (document them)

### Reflection matters

Afterward, reflect on:

- What worked well in your AI workflow?
- What felt slow or frustrating?
- Where did you get stuck?
- What would you improve?

That reflection clarifies your learning goals.

## After you finish

You’ll have:

1. A working full-stack filter feature
2. Baseline stats for your AI-assisted workflow
3. Insight into strengths and pain points
4. Context for the techniques in the next exercise.

## Questions?

- Browse existing files for architecture and setup
- Follow patterns in `app/backend/app/` and `app/frontend/src/`
- Hit `/health` to confirm the backend: http://localhost:8000/health
- Open API docs when the server is up: http://localhost:8000/docs

## Ready?

Implement using AI the way you normally would. Track time, prompts, and confidence as you go.

Good luck!
