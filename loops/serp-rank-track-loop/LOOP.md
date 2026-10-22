---
name: google-search
title: Google Search API skill
repo: fetcher-sh/fetcher-skills
license: MIT
url: https://gethabit.dev/skills/fetcher-sh/google-search
---

# Google Search API skill

The Google Search API skill returns Google web search results as clean JSON through fetcher.sh, with Google's own operators, pagination and language and country scoping, and no Custom Search setup. For agents doing rank tracking and research.

- Install the skill: `npx skills add fetcher-sh/fetcher-skills --skill google-search`
- Source: https://github.com/fetcher-sh/fetcher-skills/tree/HEAD/skills/google-search
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: getting Google results as JSON; tracking search ranks; running site: or filetype: searches programmatically.
Skip it when: you only need occasional manual searches; you must use Google's own Custom Search API.

# Make it a habit: A daily record of search ranks.

On a schedule, your agent runs your tracked queries through the google-search API, reads the clean JSON results and records where your pages rank. A run log keeps yesterday's positions per query.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily rank check (schedule; cron; `0 6 * * *`)
- **Verification:** results returned per query. Hard checks: each /api/search call returns status 200; results come back with entries, count above zero; the rank record file is written. On fail: notify, max 1 retries.
- **Memory:** rank history log at `loops/serp-rank-track-loop/run-log.md`. Read first: yesterday's position for each tracked query.

## Steps

1. **Load queries.** Your agent reads the tracked queries, with any site:, filetype: or intitle: operators and country and language settings.
2. **Search.** It calls /api/search for each query with the Bearer key, using page for more results.
3. **Read JSON.** It reads the clean JSON response and finds where your pages appear.
4. **Record ranks.** It writes each query's position to the rank record and the run log.
5. **Flag moves.** It compares with yesterday and flags queries that rose or fell.

Stop rule: Stops after one pass over the tracked queries per run, with at most one retry.

## Permissions

- Writes: loops/serp-rank-track-loop/**
- Network: google.fetcher.sh
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/serp-rank-track-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily rank check. Verification: results returned per query. Memory: loops/serp-rank-track-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
