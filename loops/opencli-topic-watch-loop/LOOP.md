---
name: smart-search
title: Smart Search skill
repo: jackwener/OpenCLI
license: Apache-2.0
url: https://gethabit.dev/skills/jackwener/smart-search
---

# Smart Search skill

The smart search skill routes your agent's searches to the best opencli source: one AI source first, then specialist sites for social media, tech, news, shopping, travel, jobs or Chinese content, with call limits and a search summary.

- Install the skill: `npx skills add jackwener/OpenCLI --skill smart-search`
- Source: https://github.com/jackwener/OpenCLI/tree/HEAD/skills/smart-search
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You search through opencli sites; You need Chinese or platform-specific results; You want a logged search summary.
Skip it when: You do not have opencli installed; A plain web search is enough.

# Make it a habit: A fresh topic digest, sources logged.

Every morning your agent checks a saved topic with opencli: it confirms live sites, asks one AI source, adds one or two specialist sources if needed, and ends with a search summary. A call ledger keeps every site under its call limit.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** ledger within limits. Hard checks: opencli list -f yaml ran before any search; each AI site has at most 1 call in the ledger; each non-AI site has at most 2 calls in the ledger; the answer ends with a search summary. On fail: stop, max 0 retries.
- **Memory:** call ledger and digests at `loops/opencli-topic-watch-loop/run-log.md`. Read first: yesterday's digest and skipped sites.

## Steps

1. **Check live sites.** Your agent runs opencli list -f yaml and confirms the candidate sites exist.
2. **Read site help.** It runs opencli <site> -h and the command help before any search.
3. **Ask one AI source.** It picks one of grok, doubao or gemini and sends a query with topic, goal and limits.
4. **Add specialists.** If the AI answer lacks raw data, it adds one or two specialist sources.
5. **Keep the ledger.** After each real search it records site, query, count and status.
6. **Summarize.** It writes the digest and ends with the search summary, including skipped sites.

Stop rule: Stops after 1 AI source call and at most 2 specialist sources with 2 calls each.

## Permissions

- Writes: loops/opencli-topic-watch-loop/**
- Network: sites listed by opencli list
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/opencli-topic-watch-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: ledger within limits. Memory: loops/opencli-topic-watch-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
