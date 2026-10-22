---
name: baidu-search
title: Baidu Search skill
repo: countbot-ai/countbot
license: MIT
url: https://gethabit.dev/skills/countbot-ai/baidu-search
---

# Baidu Search skill

Baidu search is a skill for agents that need Chinese web results through Baidu AI search, with web search, Baidu Baike, video Baike and AI-generated answer modes, plus site and time filters.

- Install the skill: `npx skills add countbot-ai/countbot --skill baidu-search`
- Source: https://github.com/countbot-ai/countbot/tree/HEAD/workspace/skills/baidu-search
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need Chinese news results; You look up a Baidu Baike entry; You filter results by recent week.
Skip it when: You need English web results; You have no Baidu Qianfan key.

# Make it a habit: Weekly Chinese news digest per topic.

Every week, your agent runs Baidu AI search on your watched topics with --recency week and --json, summarizes the new results and compares them with last week's digest. Encyclopedia lookups use the baike mode when needed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly topic digest (schedule; Claude Code routine or cron; `0 9 * * 1`)
- **Verification:** results per topic. Hard checks: search.py returns JSON without error; each topic has at least one result; each query is at most 72 characters. On fail: retry, max 1 retries.
- **Memory:** weekly digests at `loops/baidu-news-digest-loop/run-log.md`. Read first: watched topics and last week's results.

## Steps

1. **Check config.** Confirm skills/baidu-search/scripts/config.json holds an API key.
2. **Search each topic.** Run search.py with the topic, --recency week, --json and --limit.
3. **Look up terms.** Use --api-type baike for terms that need a short definition.
4. **Compare.** Drop results already in last week's digest.
5. **Write the digest.** Summarize new results per topic into the run log.

Stop rule: Stops after ten queries per run.

## Permissions

- Writes: loops/baidu-news-digest-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/baidu-news-digest-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly topic digest. Verification: results per topic. Memory: loops/baidu-news-digest-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
