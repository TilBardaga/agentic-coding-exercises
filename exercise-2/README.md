# Exercise 2: Systematic implementation with the PIV loop

## Overview

This is the second exercise in the Agentic Coding Workshop. After experiencing your natural workflow in the baseline exercise, you now apply the **PIV loop**—a systematic approach to AI-assisted coding that improves output quality and gives you more control.

You implement the same product filtering feature as before, but using the PIV loop methodology.

**PIV loop**: **P**lan → **I**mplement → **V**alidate → iterate

> Note: This task is simple enough that in practice you may only need one iteration of the loop.

## Quick start

If you have not set up the app yet, start it in two terminals:

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

1. **Apply the PIV loop** to a real full-stack implementation
2. **Feel the difference** in smoothness, control, and trust versus your earlier approach
3. **Build rich context** that leads the AI to better implementations
4. **Stay in the driver’s seat** while delegating coding work to your assistant

**What to focus on**: The implementation may look similar—we discussed keeping the task simple. Instead, notice:
- How much smoother does the PIV loop make the process?
- How much more control do you have over details?
- How well do you understand what was built?
- Are you steering the AI, or is the AI steering you?

## The assignment

> Open your AI coding assistant scoped to the `app/` folder for this exercise!

You implement the same product filtering feature as before, using the PIV loop.

### Part 1: Build your implementation plan

Start from the structured task specs:

- **Backend task**: `tasks/TASK1.md`
- **Frontend task**: `tasks/TASK2.md`

These read like tickets from Linear, Jira, or Asana: requirements, acceptance criteria, technical notes, and definition of done. Bringing them into your plan applies the “context engineering” part of RAG-style workflows.

Use them to produce a structured implementation plan with sections such as:

1. **Success criteria**: How do you know you’re done?
   - All tests in `app/backend/tests/test_products_filtering.py` pass
   - The frontend exposes all required filter controls
   - Manual test checklist items pass

2. **Documentation / references to use**:
   - Existing patterns in `app/backend/app/`
   - Existing frontend patterns in `app/frontend/src/`
   - Tests that show expected behavior

3. **Work breakdown**:
   - Backend: params model, service, endpoint updates
   - Frontend: filter UI, API client, state handling

4. **Desired structure**:
   - Naming conventions
   - File organization
   - Logging patterns
   - Type safety

### Part 2: Implement with your plan

With your plan ready, ask your AI assistant to implement:

- Provide the full plan as context when you start
- Point to specific sections at each step
- Keep the assistant aligned with your intended approach
- Notice how much more control you have compared to the baseline

### Part 3: Validate and iterate

Have the assistant:

- Run tests: `cd app/backend && uv run pytest tests/ -v`
- Check that code matches your planned patterns

You should:

- Manually test the UI in the browser
- Iterate on issues you find

## Project structure

This exercise uses the same layout as before:

```
exercise-2/
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
└── tasks/            # Task specs
    ├── TASK1.md      # Backend filtering task
    └── TASK2.md      # Frontend filtering task
```

## What to track

Compare with your baseline run:

### 💬 Quality of AI interaction

- **Number of prompts**: More or fewer than before?
- **Prompt effectiveness**: Did the AI understand your intent better with the plan?
- **Rework**: How much code had to be redone?

### 😊 Trust & control

Afterward, rate 1–10:

- **Control**: How much more in control did you feel vs. the baseline?
- **Understanding**: How well did you understand what was implemented?
- **Confidence**: How sure are you about code quality?
- **Alignment**: How well did the AI follow your plan?

### 🐛 Issues

- Did the AI drift from your plan? How?
- Did you need to change the plan mid-flight?
- Fewer surprises than before?

## Success criteria

You’re done when:

- ✅ You wrote a detailed implementation plan before coding
- ✅ All backend tests pass (`uv run pytest`)
- ✅ The API accepts and applies filter parameters correctly
- ✅ The frontend shows a working filter UI
- ✅ Filters apply and results update accordingly
- ✅ Code follows your planned patterns and structure
- ✅ You can explain how the PIV loop improved your workflow

## Important notes

### This is about process comparison

Finishing the feature is not the only goal—you’re **comparing** your baseline workflow with the PIV approach. Be honest about:

- Smoothness (was it really smoother?)
- Control (did you feel more in charge?)
- Understanding (do you get the code better?)
- Confidence (are you more sure about quality?)

### Don’t skip planning

It can feel like extra upfront work, but that’s where the PIV loop pays off:

- **Better alignment**: The AI has clear intent
- **Fewer surprises**: You thought it through before code appears
- **Easier debugging**: You know what “right” looks like
- **More control**: You steer with the plan instead of reacting to suggestions

### Key differences

| Aspect | Ad-hoc | Systematic (PIV) |
|--------|--------|------------------|
| **Approach** | Reactive prompting | Planned, structured |
| **Context** | Minimal | Rich, structured plan |
| **Control** | Following suggestions | Steering with a plan |
| **Understanding** | Learn while building | Understand before building |
| **Validation** | Reactive debugging | Proactive verification |

### Tips

1. **Don’t skip planning**—it saves time overall
2. **Be specific**—the more detail, the easier for the AI to follow
3. **Include examples**—point at patterns you want mirrored
4. **Reuse your plan as context**—paste relevant sections into prompts
5. **Validate often**—don’t wait until the end
6. **Update the plan**—when you learn something new, revise the plan

## Questions?

- Read `tasks/TASK1.md` and `tasks/TASK2.md`
- Review patterns in `app/backend/app/` and `app/frontend/src/`
- API docs when the backend is running: http://localhost:8000/docs

## Ready?

1. Read `tasks/TASK1.md` and `tasks/TASK2.md`
2. Produce your implementation plan (PIV planning phase)
3. Implement with the plan as context
4. Validate against your success criteria
5. Compare your experience with the baseline exercise

Good luck!
