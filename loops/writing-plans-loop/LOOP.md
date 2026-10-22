---
name: writing-plans
title: Writing Plans skill
repo: obra/superpowers
license: MIT
url: https://gethabit.dev/skills/obra/writing-plans
---

# Writing Plans skill

The writing plans skill turns a spec into a step-by-step implementation plan with exact files, signatures and tests for each task. For developers who hand work to a coding agent or a team.

- Install the skill: `npx skills add obra/superpowers --skill writing-plans`
- Source: https://github.com/obra/superpowers/tree/HEAD/skills/writing-plans
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you have a spec for a multi-step task; before any code is written; tasks go to subagents.
Skip it when: the change is one small edit; there is no spec yet.

# Make it a habit: Every spec becomes a plan.

When a new spec lands, your agent writes an implementation plan with exact files, signatures and tests per task. It runs its own five-point review against the spec, saves the plan, and waits for you to approve it and pick how it runs.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new spec committed (event; GitHub Actions or Claude Code routine; `push touches a spec or design doc`)
- **Verification:** self-review + your approval. Hard checks: plan file exists in docs/superpowers/plans/; plan starts with the required header; every spec requirement maps to a task; no step says TBD; names and signatures match across tasks. On fail: retry, max 1 retries.
- **Memory:** saved plans folder at `docs/superpowers/plans/`. Read first: earlier plans and the spec they implement.

## Steps

1. **Check the scope.** If the spec covers several separate subsystems, suggest one plan for each.
2. **Map the files.** List which files the work creates or changes and what each one owns.
3. **Write the tasks.** Each task names its files, its interfaces, a failing test, the code step and a commit.
4. **Run self-review.** Check spec coverage, empty steps, type consistency, the Review Focus list and plan length.
5. **Save the plan.** Save it as docs/superpowers/plans/YYYY-MM-DD-<feature-name>.md.
6. **Hand off.** Ask you to review and choose superpowers:subagent-driven-development or superpowers:executing-plans.

Stop rule: Stops after one spec per run and one self-review fix pass.

## Permissions

- Writes: docs/superpowers/plans/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`docs/superpowers/plans/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new spec committed. Verification: self-review + your approval. Memory: docs/superpowers/plans/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
