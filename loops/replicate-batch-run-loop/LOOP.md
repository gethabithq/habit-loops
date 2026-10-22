---
name: run-models
title: Run Models skill
repo: replicate/skills
license: Apache-2.0
url: https://gethabit.dev/skills/replicate/run-models
---

# Run Models skill

The run models skill helps developers run AI models on Replicate with predictions, polling, webhooks and streaming, with schema-valid inputs and safe handling of expiring output URLs.

- Install the skill: `npx skills add replicate/skills --skill run-models`
- Source: https://github.com/replicate/skills/tree/HEAD/skills/run-models
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You run a model on Replicate; You chain models in a pipeline; You receive results by webhook.
Skip it when: You need to pick a model first; You do not use Replicate.

# Make it a habit: Queued generations done and saved.

On a schedule your agent takes queued jobs from the board, fetches each model's schema, validates inputs, starts predictions in parallel with a lifetime, polls until they finish and downloads outputs before the URLs expire. The board tracks every job.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** hourly job queue (schedule; Claude Code routine or cron; `0 * * * *`)
- **Verification:** predictions succeeded, outputs saved. Hard checks: every input matches the schema minimum, maximum and enum; each prediction reaches succeeded or is marked failed; output files are saved locally within the hour. On fail: retry, max 1 retries.
- **Memory:** generation job board at `loops/replicate-batch-run-loop/board.md`. Read first: queued, running and failed jobs.

## Steps

1. **Pick jobs.** Take queued jobs from the board.
2. **Get schemas.** Fetch each model's input and output schema.
3. **Create predictions.** POST to /v1/predictions for each job in parallel with a lifetime set.
4. **Poll.** Poll each prediction until it succeeds, fails or is canceled.
5. **Save outputs.** Download output files right away, since URLs expire after one hour.

Stop rule: Stops after 10 jobs per run, with one retry per failed job.

## Permissions

- Writes: loops/replicate-batch-run-loop/**
- Network: api.replicate.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/replicate-batch-run-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: hourly job queue. Verification: predictions succeeded, outputs saved. Memory: loops/replicate-batch-run-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
