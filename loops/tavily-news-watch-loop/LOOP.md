---
name: tavily-search
title: Tavily Search skill
repo: tavily-ai/skills
license: MIT
url: https://gethabit.dev/skills/tavily-ai/tavily-search
---

# Tavily Search skill

The tavily search skill lets agents search the web through the Tavily CLI with LLM-ready snippets, scores, domain filters, time ranges and search depths. For anyone whose agent needs current web information.

- Install the skill: `npx skills add tavily-ai/skills --skill tavily-search`
- Source: https://github.com/tavily-ai/skills/tree/HEAD/skills/tavily-search
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need recent news on a topic; You do not have a URL yet; You want results from trusted domains.
Skip it when: You already have the URL to read; You need deep multi-source research.

# Make it a habit: Daily news on your topics.

Each morning your agent runs tavily search for your saved topics with --topic news and --time-range day, filtered to trusted domains. It keeps only results not seen before and logs them by topic.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily news search (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** results saved. Hard checks: tvly search returns valid JSON for each topic; result count is above zero for at least one topic; output file from -o exists. On fail: notify, max 1 retries.
- **Memory:** seen results log at `loops/tavily-news-watch-loop/seen.md`. Read first: topic list and URLs already seen.

## Steps

1. **Load topics.** Read the saved topics and trusted domains from the log.
2. **Search.** Run tvly search with --topic news, --time-range day and --json per topic.
3. **Focus sources.** Use --include-domains for trusted sources.
4. **Drop repeats.** Remove URLs that are already in the log.
5. **Log new items.** Save new results by topic with their relevance score.

Stop rule: Stops after ten topics per run.

## Permissions

- Writes: loops/tavily-news-watch-loop/**
- Network: Tavily API via tvly
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/tavily-news-watch-loop/seen.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily news search. Verification: results saved. Memory: loops/tavily-news-watch-loop/seen.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
