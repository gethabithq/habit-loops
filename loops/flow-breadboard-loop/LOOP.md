---
name: layers-interaction-flow
title: Layers Interaction Flow skill
repo: jamiemill/layers-skills
license: MIT
url: https://gethabit.dev/skills/jamiemill/layers-interaction-flow
---

# Layers Interaction Flow skill

The layers interaction flow skill helps product designers map places, affordances, edge cases and failure paths with breadboards before any visual design.

- Install the skill: `npx skills add jamiemill/layers-skills --skill layers-interaction-flow`
- Source: https://github.com/jamiemill/layers-skills/tree/HEAD/skills/layers-interaction-flow
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You map a user flow before wireframes; You find missing edge cases; You redesign an existing flow.
Skip it when: The conceptual model is still unstable; You only need visual polish.

# Make it a habit: Flows mapped with every edge case.

For each job story your agent loads /layers-intro, confirms the conceptual model is stable, breadboards the places, affordances and destinations, walks the happy path and every failure, empty and cancel path, and logs the open decisions.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new job story to map (manual; Claude Code routine; `run when a flow for a job story needs design`)
- **Verification:** every affordance has destination. Hard checks: every affordance in the breadboard names a destination place; failure, empty, loading and cancel paths are breadboarded; one job story uses 6 places or fewer, or a reason is noted. On fail: retry, max 1 retries.
- **Memory:** breadboards and open decisions at `loops/flow-breadboard-loop/breadboards.md`. Read first: earlier breadboards and unresolved edge cases.

## Steps

1. **Load the framework.** Load /layers-intro first.
2. **Settle the job.** Agree with you on the job story, starting point and success.
3. **Check the model.** Confirm the /layers-conceptual-model objects beneath are stable.
4. **Breadboard.** Name places and map each affordance to a destination in breadboard notation.
5. **Walk the edges.** Walk the happy path, then validation, server error, timeout and concurrent edit paths.
6. **Capture.** Save the breadboard, an optional graph LR diagram and open decisions.

Stop rule: Stops after one job story per run.

## Permissions

- Writes: loops/flow-breadboard-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/flow-breadboard-loop/breadboards.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new job story to map. Verification: every affordance has destination. Memory: loops/flow-breadboard-loop/breadboards.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
