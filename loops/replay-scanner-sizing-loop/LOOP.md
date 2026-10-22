---
name: creating-replay-vision-scanners
title: Creating Replay Vision Scanners skill
repo: PostHog/skills
license: MIT
url: https://gethabit.dev/skills/posthog/creating-replay-vision-scanners
---

# Creating Replay Vision Scanners skill

The creating replay vision scanners skill helps PostHog users create session recording scanners safely: choose the type, narrow the query and estimate usage before the first sweep.

- Install the skill: `npx skills add PostHog/skills --skill creating-replay-vision-scanners`
- Source: https://github.com/PostHog/skills/tree/HEAD/skills/omnibus/creating-replay-vision-scanners
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You create a Replay Vision scanner; You widen a scanner's query or model; You want a standing watch on recordings.
Skip it when: You ask about sessions you already have; You only read scanner results.

# Make it a habit: Scanners sized before they run.

Whenever a Replay Vision scanner is created or widened, your agent checks whether an inline scan fits better, picks the type and config, narrows the query, runs vision-scanners-estimate and vision-quota-get, and asks you before creating a large one.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** scanner create or widen (event; Claude Code routine; `a request to create a scanner or widen its query, sampling or model`)
- **Verification:** estimate checked, you confirm. Hard checks: vision-scanners-estimate ran before vision-scanners-create; vision-quota-get ran before vision-scanners-create; the scanner_config shape matches the scanner_type. On fail: stop, max 0 retries.
- **Memory:** scanner sizing log at `loops/replay-scanner-sizing-loop/run-log.md`. Read first: scanners created and their estimates.

## Steps

1. **Check the need.** Use vision-scanners-inline-scan instead when the sessions are already known.
2. **Design.** Run designing-replay-vision-scanners if the question is vague, then pick monitor, classifier, scorer or summarizer.
3. **Narrow the query.** Shape the RecordingsQuery and set sampling_mode and sampling_rate.
4. **Size it.** Run vision-scanners-estimate and vision-quota-get and prorate to the rest of the period.
5. **Confirm and create.** Show you the numbers when large, then call vision-scanners-create.
6. **Hand over.** Share the scanner URL and explain rating results with vision-observations-label-create.

Stop rule: Stops after one scanner per request.

## Permissions

- Writes: loops/replay-scanner-sizing-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/replay-scanner-sizing-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: scanner create or widen. Verification: estimate checked, you confirm. Memory: loops/replay-scanner-sizing-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
