---
name: agy-delegate
title: Antigravity Delegate (agy) skill
repo: amelnagdy/delegate-skills
license: MIT
url: https://gethabit.dev/skills/amelnagdy/agy-delegate
---

# Antigravity Delegate (agy) skill

Antigravity Delegate (agy) lets an orchestrator hand a bounded coding task to the Google Antigravity CLI, then review the diff, rerun the gates and commit it itself, with a relay that records result.json. For developers using Antigravity as an implementer.

- Install the skill: `npx skills add amelnagdy/delegate-skills --skill agy-delegate`
- Source: https://github.com/amelnagdy/delegate-skills/tree/HEAD/skills/agy-delegate
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want Antigravity to implement a task; You run a queue of coding tasks; You want to review before commit.
Skip it when: The task is small enough inline; agy is not installed.

# Make it a habit: Delegate to agy, review, then land.

For each task in your queue, your agent writes a full brief, runs relay.mjs to hand it to the Antigravity agy CLI, reads result.json, reruns the gates and the diff itself and commits only verified work. A queue file keeps progress.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you queue tasks for agy (manual; Claude Code routine; `user asks to delegate tasks to Antigravity`)
- **Verification:** gates rerun, diff reviewed. Hard checks: result.json exists and status is not failed; project gates pass when rerun; readOnlyViolation is false on read-only runs; diff touches only files the brief allows. On fail: retry, max 2 retries.
- **Memory:** delegation queue at `loops/antigravity-task-queue-loop/queue.md`. Read first: open tasks and constraints carried from earlier ones.

## Steps

1. **Check prerequisites.** Your agent runs agy help and agy models.
2. **Write the brief.** It writes goal, state, limits, real gate commands and a report contract, and says agy will not commit.
3. **Dispatch.** It runs node relay.mjs with --brief and --cd, adding --read-only for reviews.
4. **Wait.** It waits until result.json exists and the process exits.
5. **Review.** It reads touchedFiles, reruns the gates and checks the diff against the brief.
6. **Land or rework.** It commits verified work, or sends a delta brief with --resume-last.

Stop rule: Stops after 5 tasks or 2 rework rounds per task per run.

## Permissions

- Writes: src/**, loops/antigravity-task-queue-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/antigravity-task-queue-loop/queue.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you queue tasks for agy. Verification: gates rerun, diff reviewed. Memory: loops/antigravity-task-queue-loop/queue.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
