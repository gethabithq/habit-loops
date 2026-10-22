---
name: compare-models
title: Compare Models skill
repo: replicate/skills
license: Apache-2.0
url: https://gethabit.dev/skills/replicate/compare-models
---

# Compare Models skill

The compare models skill helps developers compare Replicate models on speed, quality and capabilities by shortlisting, reading schemas and running the same small test batch through each.

- Install the skill: `npx skills add replicate/skills --skill compare-models`
- Source: https://github.com/replicate/skills/tree/HEAD/skills/compare-models
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You choose between several models; You want to check if a newer model is better; You compare official and community models.
Skip it when: You already have a fixed model; You do not use Replicate.

# Make it a habit: Your model choice re-tested each month.

Each month your agent builds a shortlist for your task, fetches each model's schema, runs the same small prompt set through each one, reads predict_time from the metrics and compares outputs against your criteria. A results file keeps each round's pick and why.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly model bake-off (schedule; Claude Code routine; `0 9 1 * *`)
- **Verification:** same prompts, metrics recorded. Hard checks: every candidate ran the same prompt set; metrics.predict_time is recorded for each completed prediction; every candidate's schema was fetched this round. On fail: retry, max 1 retries.
- **Memory:** bake-off results at `loops/replicate-model-bakeoff-loop/results.md`. Read first: last round's winner, prompts and timings.

## Steps

1. **Shortlist.** Search or browse collections for candidate models.
2. **Compare schemas.** Fetch each schema and compare inputs, outputs and features.
3. **Prepare prompts.** Use the prompt-images or prompt-videos skill to write the shared prompt set.
4. **Run a small batch.** Run the same prompts through each model and collect outputs.
5. **Compare.** Compare speed from metrics, output quality and capabilities, noting official versus community.
6. **Record the pick.** Write the winner and reasons to the results file.

Stop rule: Stops after 4 candidates and 5 prompts per candidate per run.

## Permissions

- Writes: loops/replicate-model-bakeoff-loop/**
- Network: api.replicate.com, replicate.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/replicate-model-bakeoff-loop/results.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly model bake-off. Verification: same prompts, metrics recorded. Memory: loops/replicate-model-bakeoff-loop/results.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
