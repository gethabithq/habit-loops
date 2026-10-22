---
name: web-search
title: Brave Web Search skill
repo: brave/brave-search-skills
license: MIT
url: https://gethabit.dev/skills/brave/web-search
---

# Brave Web Search skill

The Brave Web Search skill calls the Brave Search API for ranked web results with snippets, URLs and thumbnails, plus freshness filters, SafeSearch, Goggles custom ranking, pagination and rich data callbacks. For developers and agents that need web search.

- Install the skill: `npx skills add brave/brave-search-skills --skill web-search`
- Source: https://github.com/brave/brave-search-skills/tree/HEAD/skills/web-search
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: An agent needs web results; You want fresh news on a topic; You want custom site ranking.
Skip it when: You need extracted page text for RAG; You have no Brave API key.

# Make it a habit: Fresh results on your topics, daily.

Each morning your agent queries the Brave Web Search API for your watched topics with freshness set to the past day, optional Goggles to boost trusted sites and a result filter for web and news. It drops links already seen and writes a short digest.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily topic search (schedule; Claude Code routine; `0 7 * * *`)
- **Verification:** API response check. Hard checks: every response has type search; the count of new results across topics is above zero or reported as zero; every query is 1-400 characters and at most 50 words. On fail: notify, max 1 retries.
- **Memory:** seen links log at `loops/brave-news-watch-loop/log.md`. Read first: watched topics, Goggles rules and URLs already reported.

## Steps

1. **Read the watchlist.** Load topics, country, language and any Goggles rules from the log.
2. **Search.** Call the web search endpoint with q, freshness=pd, count and result_filter=web,news.
3. **Re-rank.** Apply inline Goggles to boost trusted sites or discard spammy ones.
4. **Page if needed.** Use offset when more_results_available is true, up to the run's limit.
5. **Write the digest.** Keep new URLs only, summarize title and snippet, and log the URLs.

Stop rule: Stops after at most 5 topics and 2 pages per topic per run.

## Permissions

- Writes: loops/brave-news-watch-loop/**
- Network: api.search.brave.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/brave-news-watch-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily topic search. Verification: API response check. Memory: loops/brave-news-watch-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
