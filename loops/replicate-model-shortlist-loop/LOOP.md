---
name: find-models
title: Find Models skill
repo: replicate/skills
license: Apache-2.0
url: https://gethabit.dev/skills/replicate/find-models
---

# Find Models skill

The find models skill helps developers find current AI models on Replicate through search and curated collections, read their schemas and pick official, recent models.

- Install the skill: `npx skills add replicate/skills --skill find-models`
- Source: https://github.com/replicate/skills/tree/HEAD/skills/find-models
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You pick a model for a task; You check if a better model exists; You compare image or video models.
Skip it when: You already have a pinned model; You do not use Replicate.

# Make it a habit: Your model shortlist stays current.

Each week your agent searches the Replicate API for each task you care about, checks the official collection, reads each candidate's schema and updates a shortlist that favors official, recent models. A shortlist file keeps choices and reasons.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly model check (schedule; Claude Code routine or cron; `0 7 * * 4`)
- **Verification:** schemas read for shortlist. Hard checks: GET /v1/search returns results for each task; every shortlisted model had its schema fetched this run; community models are listed with a pinned version_id. On fail: retry, max 1 retries.
- **Memory:** model shortlist at `loops/replicate-model-shortlist-loop/shortlist.md`. Read first: current picks per task and why they were chosen.

## Steps

1. **Search by task.** Run GET /v1/search with a targeted query for each task.
2. **Check collections.** Look at the official collection with GET /v1/collections/{slug}.
3. **Read schemas.** Fetch GET /v1/models/{owner}/{name} and read the input properties.
4. **Pick.** Prefer official, latest and recently released models over raw run counts.
5. **Update shortlist.** Write changes and reasons to the shortlist.

Stop rule: Stops after 5 tasks and 3 candidates per task per run.

## Permissions

- Writes: loops/replicate-model-shortlist-loop/**
- Network: api.replicate.com, replicate.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/replicate-model-shortlist-loop/shortlist.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly model check. Verification: schemas read for shortlist. Memory: loops/replicate-model-shortlist-loop/shortlist.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
