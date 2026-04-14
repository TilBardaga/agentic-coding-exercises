# Exercise 4 — Your own codebase

The workshop app is behind you. In this exercise, you take everything you have learned and apply it to **your own project** — a real codebase, with real complexity, real history, and real stakes.

This is where the training becomes practical. The patterns you practiced on the product catalog are the same ones that work on a 10-year-old monolith or a greenfield microservice. The question is: can you apply them when the codebase is not neatly structured for a workshop?

**There are no required tasks.** Pick something from your own work, use the workflow, and see what happens. The suggestions below are starting points — use them, adapt them, or ignore them entirely.

---

## Getting started

### Set up the workflow in your repo

Before you can use the agent commands, you need to bring them into your project. You have two options:

**Option A — Copy the commands into your repo:**

```
Copy the .cursor/ folder from this workshop into your own project.
The commands (prime, plan, implement, code-review, etc.) are generic —
they work on any codebase. You may want to update the rules/ files
to match your project's conventions.
```

**Option B — Start with just the mental model.** You do not need the command files to use the workflow. The PIV loop works with any AI assistant:

1. **Prime** — Give your assistant context. Share relevant files, explain the architecture, point it to conventions.
2. **Plan** — Ask it to help you plan before coding. Map the codebase, sequence the work, identify risks.
3. **Implement** — Let it execute the plan. Review the output.
4. **Validate** — Run tests, check the UI, verify the behavior.
5. **Review** — Ask it to review the changes for code smells, security issues, edge cases.

The commands are a convenience, not a requirement. The thinking behind them is what matters.

### Prime your assistant on your codebase

If this is the first time your assistant sees your project, give it a proper introduction. A good starting prompt:

```
I am going to work on [this project]. Before we start, I need you to
understand the codebase.

Read the following files to understand the structure and conventions:
- [your main README or docs]
- [key config files — package.json, pyproject.toml, etc.]
- [one or two representative source files that show the patterns]

Then tell me:
1. How is the project structured?
2. What patterns and conventions do you see?
3. What would you want to know before making changes here?
```

This is the equivalent of `/prime` — but tailored to your project instead of the workshop app.

---

## Working with your assistant

In the workshop exercises, you followed a structured sequence. In your own project, the interaction is more fluid — think of your assistant as a colleague you can brief, spar with, and delegate to. Here is how to get the most out of it.

### Brief it like a colleague

The better the briefing, the better the output. When you start a task, give your assistant the same context you would give a colleague sitting next to you:

```
We have a user settings page that was built two years ago. It still works
but it uses class components and an old state management pattern. I want to
modernize it to use hooks and our current patterns, without changing the
behavior.

Here are the files involved:
- src/pages/UserSettings.tsx (the main component)
- src/api/userSettings.ts (the API client)
- src/store/userSettingsStore.ts (the old state management)

Read these files and tell me what you think the migration path looks like
before we start changing anything.
```

Notice the pattern: what you want to do, why, which files are involved, and what you expect back. The more context you give upfront, the fewer corrections you need later.

### Spar before you decide

You do not have to have all the answers before you start. Use your assistant to think through trade-offs:

```
I need to decide how to handle file uploads in this app. We could use
presigned S3 URLs and upload directly from the client, or route everything
through our API.

What are the trade-offs? Think about: security, performance, complexity,
error handling, and what happens when uploads fail halfway.
```

This is not asking the AI to decide for you — it is using it as a sounding board. The same way you would walk over to a colleague and say "help me think through this."

### Ask it to explore what you do not know

Your assistant can read code faster than you. Use that:

- _"How does authentication work in this project? Trace the flow from login to a protected API call."_
- _"Find all the places where we handle payment errors. Do they all follow the same pattern?"_
- _"What dependencies does this module have? If I refactor it, what else will I need to update?"_
- _"Search the web for how other projects handle [this specific problem] in [this framework]."_

You are not being lazy — you are using the right tool for the job. Reading code is something AI is genuinely good at. Understanding what it means is still your job.

### When you are stuck

Getting stuck is normal. Here are prompts that help you get unstuck:

```
I am trying to [what you want to do] but [what is going wrong].
Here is the error: [paste the error].
Here is the relevant code: [paste or reference the file].
What am I missing?
```

```
This test is failing and I do not understand why. Read the test and the
implementation, and explain what the test expects vs. what the code
actually does.
```

```
I have been going back and forth on this for a while and I am not making
progress. Take a step back — read what we have done so far in this
conversation and suggest a different approach.
```

The last one is especially useful. Sometimes you and the AI get into a loop where you keep trying variations of the same broken approach. Asking it to reset and reconsider breaks the cycle.

### Set boundaries

If you want the AI to stay in its lane, say so:

- _"Only change files in the `src/auth/` folder — do not touch anything else."_
- _"Suggest the fix but do not apply it yet. I want to review first."_
- _"Do not refactor the surrounding code. Only fix the bug I described."_
- _"Explain what you would do, step by step, but do not write any code yet."_

Being explicit about scope is not micromanaging — it is preventing the AI from "helping" by changing things you did not ask it to change.

---

## Practice ideas

Not sure where to start? Here are tasks that work well for practicing the workflow on a real codebase. Pick one that is relevant to your work, or use them as inspiration.

### Refactoring tasks

These are low-risk, high-learning exercises. The behavior does not change — only the structure improves.

| Task | What you practice |
|------|------------------|
| **Extract a service layer** — Find a controller or route handler that does too much (data access, business logic, response formatting). Separate the concerns. | Planning a multi-file refactor; keeping tests green throughout |
| **Remove dead code** — Ask your assistant to find unused functions, imports, or config. Verify they are truly unused, then remove them. | Using AI for codebase analysis; validating assumptions before deleting |
| **Consolidate duplicated logic** — Find two or three places that do the same thing slightly differently. Unify them behind a shared function or module. | Impact analysis — what else depends on this code? |
| **Improve error handling** — Find a module that swallows errors silently or returns generic messages. Make it specific and useful. | Edge case thinking; understanding failure modes |

### Legacy and modernization tasks

If your codebase has older parts that need attention, these are excellent practice:

| Task | What you practice |
|------|------------------|
| **Update a legacy page or component** — Pick something old and bring it up to current standards. Same functionality, modern patterns. | Planning in a codebase with technical debt; navigating unfamiliar code |
| **Add types to an untyped module** — Take a JavaScript file and convert it to TypeScript, or add type hints to a Python module. | Incremental improvement; understanding existing behavior before changing it |
| **Replace a deprecated dependency** — Find a library that is outdated or has a security advisory. Swap it for the modern equivalent. | Risk assessment; understanding blast radius |
| **Write tests for untested code** — Pick a module with no tests. Read it, understand what it does, write tests that verify the current behavior. | Deep codebase understanding before any changes |

### Feature work

If you have a real feature to build, use the full cycle:

| Task | What you practice |
|------|------------------|
| **A small feature from your backlog** — Pick something scoped. Plan it, build it, review it. | The full workflow on real requirements |
| **A proof of concept** — Something you have been curious about but have not had time to explore. | Using AI as a research partner; rapid prototyping with structure |
| **Documentation** — Write or update docs for a part of your codebase that is poorly documented. | Using AI to understand code and explain it clearly |

---

## Principles to take with you

These are the mental models from the workshop, distilled. They are not rules — they are ways of thinking that help you work better with AI.

### You are the architect, the AI is the builder

The AI is fast at writing code. It is not good at deciding _what_ to build, _why_ to build it, or _whether_ the result is correct. Those are your jobs. The more clearly you define the what and why, the better the AI performs on the how.

### Plan at the boundaries, not in the middle

The most valuable planning happens at the edges — where your code meets external systems, user input, or other modules. What are the inputs? What are the outputs? What can go wrong? Get those right in the plan, and the implementation details mostly take care of themselves.

### Review AI output like you would review a colleague's PR

The AI does not know your context, your users, or your edge cases. It generates plausible code that often works — but "often works" is not "correct." Read what it wrote. Check the assumptions. Run the tests. Trust but verify.

### Small changes, validated often

A plan with 15 steps and no validation until the end is a plan that will fail somewhere in the middle. Break the work into chunks you can verify independently. Green tests after each step means you always know where you are.

### Invest time before implementation, not after

Debugging a bad implementation takes longer than reviewing a good plan. Edge case analysis takes less time before coding than after a production incident. Time spent understanding the codebase is never wasted — time spent guessing about the codebase always is.

---

## Resources

### The workshop commands

The agent commands from this workshop are in `.cursor/commands/`. They are not proprietary — they are markdown files that instruct any AI assistant. You can:

- **Copy them into your projects** and adapt the rules to your conventions
- **Use them as templates** for writing your own commands
- **Read them** to understand what makes a good prompt — they are examples of structured, repeatable prompting

### The PIV loop

The core of everything you practiced:

```
Plan → Implement → Validate → (iterate)
```

This is not a tool or a product. It is a habit. It works with any AI assistant, any IDE, any language. The discipline of thinking before doing and checking after is universal.

### Going deeper

If you want to explore agentic coding further:

- **Custom commands** — Write your own commands for workflows specific to your team. `/deploy-check`, `/migration-plan`, `/onboard-to-module` — anything you do repeatedly can be codified.
- **Rules files** — The `.cursor/rules/` folder contains coding conventions that the AI follows automatically. Writing rules for your own project is one of the highest-leverage things you can do — it means the AI follows your conventions without you repeating them in every prompt.
- **Multi-agent workflows** — Some tasks benefit from separate AI sessions for different concerns: one for planning, one for implementation, one for review. The same principle as code review — a fresh perspective catches what familiarity misses.

---

## One last thing

The biggest risk with AI-assisted coding is not that the AI writes bad code. It is that you stop paying attention. The moment you accept generated code without reading it is the moment you lose control of your codebase.

The workflow you learned in this workshop — plan, implement, validate, review — exists to keep you in control. Not because AI is unreliable, but because good engineering requires it. The same discipline applied before AI: understand the problem, design the solution, verify the result. AI changes the speed. It does not change the standard.

Take the workflow. Adapt it. Make it yours.
