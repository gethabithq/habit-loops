---
name: twitter-api
title: Twitter API skill
repo: fetcher-sh/fetcher-skills
license: MIT
url: https://gethabit.dev/skills/fetcher-sh/twitter-api
---

# Twitter API skill

Twitter api gives agents read access to Twitter/X data on fetcher.sh: tweet search with advanced operators, profiles, timelines, followers, Lists and trends, with no OAuth or developer app. For social listening and research.

- Install the skill: `npx skills add fetcher-sh/fetcher-skills --skill twitter-api`
- Source: https://github.com/fetcher-sh/fetcher-skills/tree/HEAD/skills/twitter-api
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: searching tweets by keyword or operator; pulling a profile or its followers; checking trends by country.
Skip it when: you need to post tweets; you already use the official X API.

# Make it a habit: New posts on your topics, daily.

Every day your agent runs a fixed set of tweet searches with X operators through twitter.fetcher.sh, for example from: or since:, and logs new matches. It checks each response status and keeps the last run's results to show only what is new.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily topic search (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** response status check. Hard checks: every response has status 200; no 401 or 402 in the run; count of new tweets is logged. On fail: stop, max 0 retries.
- **Memory:** seen tweets log at `loops/x-search-watch-loop/log.md`. Read first: tweet ids already seen per saved search.

## Steps

1. **Load searches.** Read the saved queries and the tweet ids seen last time.
2. **Search.** Call /api/search with each query, using operators like since: and min_faves:.
3. **Check responses.** Stop on 401 or 402 and note any 400 with the parameter it names.
4. **Filter new.** Drop tweets already in the log.
5. **Log.** Write the new tweets per query and update the seen ids.

Stop rule: Stops after the saved queries, at most 10 calls per run.

## Permissions

- Writes: loops/x-search-watch-loop/**
- Network: twitter.fetcher.sh
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/x-search-watch-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily topic search. Verification: response status check. Memory: loops/x-search-watch-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
