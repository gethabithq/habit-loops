---
name: parallel-web-extract
title: Parallel Web Extract skill
repo: parallel-web/parallel-agent-skills
license: MIT
url: https://gethabit.dev/skills/parallel-web/parallel-web-extract
---

# Parallel Web Extract skill

The parallel web extract skill pulls clean content from up to 20 URLs per call with parallel-cli, saves it as JSON and names any failed URL with its reason. For agents that need page text from the command line.

- Install the skill: `npx skills add parallel-web/parallel-agent-skills --skill parallel-web-extract`
- Source: https://github.com/parallel-web/parallel-agent-skills/tree/HEAD/skills/parallel-web-extract
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need verbatim text from given URLs; You want extraction saved as JSON; No web fetch tool is available.
Skip it when: You need to search for pages first; A Parallel web_fetch tool already covers it.

# Make it a habit: Know when watched pages change.

Every week your agent extracts a fixed list of URLs with parallel-cli extract, saves the JSON, compares it with last week's copy and reports what changed. Failed URLs are named with their reason, and the log keeps each snapshot path.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine or cron; `0 6 * * 1`)
- **Verification:** JSON saved, errors named. Hard checks: parallel-cli exits zero; saved JSON file exists and is newer than the run start; results count above zero; every URL in errors is named with its reason. On fail: retry, max 1 retries.
- **Memory:** snapshots and changes at `loops/page-watch-extract-loop/run-log.md`. Read first: the URL list and last week's snapshot path.

## Steps

1. **Read the list.** Your agent reads the URL list and last week's snapshot path from the log.
2. **Check auth.** It runs parallel-cli auth --json and checks the authenticated value.
3. **Extract pages.** It passes each URL as its own quoted argument, up to 20, with --json and -o to a new file.
4. **Handle failures.** It keeps good results and names each failed URL with the returned reason, never inventing content.
5. **Compare snapshots.** It compares the new JSON with last week's file and lists changed pages.
6. **Log the run.** It writes the new snapshot path and the change list to the log.

Stop rule: Stops after one call of up to 20 URLs and 1 retry.

## Permissions

- Writes: loops/page-watch-extract-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/page-watch-extract-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: JSON saved, errors named. Memory: loops/page-watch-extract-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
