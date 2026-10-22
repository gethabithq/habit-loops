---
name: plan-crafting
title: Plan Crafting skill
repo: sentimony/skills
license: MIT
url: https://gethabit.dev/skills/sentimony/plan-crafting
---

# Plan Crafting skill

The plan crafting skill helps coding agents turn an approved design into a detailed implementation plan with bite-sized, test-first tasks, exact files and a self-review before execution.

- Install the skill: `npx skills add sentimony/skills --skill plan-crafting`
- Source: https://github.com/sentimony/skills/tree/HEAD/plugins/devflow/skills/plan-crafting
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A design was approved; You need a multi-step implementation plan; You hand work to subagents.
Skip it when: The change is a one-line fix; Requirements are not settled yet.

# Make it a habit: Approved specs become executable plans.

When a spec is approved, your agent maps the files, writes bite-sized tasks with tests and commits, self-reviews for gaps and placeholders, runs cross-review if installed, saves the plan in docs/plans/ and asks you how to execute it.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** spec approved (event; Claude Code routine; `a spec in docs/specs/ is approved`)
- **Verification:** plan checks, you choose. Hard checks: plan starts with the required header; no TBD, TODO or 'similar to Task N' text; every requirement maps to a task; every helper used in a code block is defined. On fail: retry, max 1 retries.
- **Memory:** plans folder at `docs/plans/`. Read first: the approved spec and earlier plans for the same area.

## Steps

1. **Announce.** Say that plan-crafting is creating the implementation plan.
2. **Map files.** List files to create or change and what each is responsible for.
3. **Write tasks.** Write right-sized tasks with Files, Interfaces, test-first steps and commits.
4. **Self-review.** Check coverage, placeholders, type consistency and symbol closure.
5. **Cross-review.** If cross-review is installed and a spec exists, run it and apply fixes through review-resolution.
6. **Ask execution choice.** Save the plan and ask you to pick inline-plan-dev or subagent-plan-dev.

Stop rule: Stops after one plan per run; at most 3 automatic review rounds.

## Permissions

- Writes: docs/plans/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`docs/plans/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: spec approved. Verification: plan checks, you choose. Memory: docs/plans/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
