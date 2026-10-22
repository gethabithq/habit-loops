---
name: qmd
title: QMD skill
repo: tobi/qmd
license: MIT
url: https://gethabit.dev/skills/tobi/qmd
---

# QMD skill

The qmd skill searches local markdown notes, docs and wikis with QMD: BM25 and structured semantic queries, retrieving full sources by docid, metadata filters and index setup. For people with large local knowledge bases.

- Install the skill: `npx skills add tobi/qmd --skill qmd`
- Source: https://github.com/tobi/qmd/tree/HEAD/skills/qmd
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You search your markdown notes; You answer from indexed docs; You set up QMD collections.
Skip it when: Notes are not in markdown; You need web search.

# Make it a habit: Keep your markdown notes searchable.

Each night your agent runs qmd update and qmd embed on your collections, checks qmd status and qmd doctor, and runs a few saved searches to confirm they still return the right docs. A log keeps index health and search results.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** nightly index refresh (schedule; Claude Code routine or cron; `0 3 * * *`)
- **Verification:** index health and searches. Hard checks: qmd update and qmd embed exit without error; qmd doctor reports no problems; each saved search returns at least one result. On fail: notify, max 1 retries.
- **Memory:** index health log at `loops/qmd-notes-index-loop/runs.md`. Read first: last run's status and saved search hits.

## Steps

1. **Check what is indexed.** Your agent runs qmd collection list and qmd status.
2. **Refresh.** It runs qmd update and qmd embed, which you set up to run on a schedule.
3. **Check health.** It runs qmd doctor if anything fails.
4. **Test searches.** It runs saved qmd search and structured qmd query checks with intent and lex fields.
5. **Log.** It records status and which docids each search returned.

Stop rule: Stops after one refresh and 5 test searches per run.

## Permissions

- Writes: loops/qmd-notes-index-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/qmd-notes-index-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: nightly index refresh. Verification: index health and searches. Memory: loops/qmd-notes-index-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
