---
name: daily-ai-news
title: Daily AI News skill
repo: yyh211/claude-meta-skill
license: MIT
url: https://gethabit.dev/skills/yyh211/daily-ai-news
---

# Daily AI News skill

The daily ai news skill gathers the latest AI news from news sites and web search, filters and sorts it into five categories, and writes a short briefing with direct links, for anyone who wants a daily AI update.

- Install the skill: `npx skills add yyh211/claude-meta-skill --skill daily-ai-news`
- Source: https://github.com/yyh211/claude-meta-skill/tree/HEAD/daily-ai-news
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you want today's AI news; a daily AI briefing for a team; tracking AI product and research releases.
Skip it when: deep research on one topic; no web access is available.

# Make it a habit: A fresh AI briefing daily.

Every morning, your agent fetches 3-5 AI news sites, runs date-filtered web searches, drops duplicates and old items, sorts stories into five categories and writes a linked briefing. A check rejects briefings with missing links or repeats.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; Claude Code routine; `0 7 * * *`)
- **Verification:** links and dedupe check. Hard checks: every story has a link and a date; no duplicate story across categories; stories come from more than one source; at least five stories in the briefing. On fail: retry, max 1 retries.
- **Memory:** past briefings at `loops/daily-ai-news-loop/briefings.md`. Read first: headlines already covered in recent briefings.

## Steps

1. **Fetch news sites.** Your agent reads 3-5 AI news sites with mcp__web_reader__webReader.
2. **Search the web.** It runs 2-3 WebSearch queries filtered to today or yesterday.
3. **Read full articles.** It fetches the top 10-15 stories in full instead of using snippets.
4. **Filter.** It keeps the last 24-48 hours and removes duplicates, minor updates and off-topic items.
5. **Categorise.** It sorts stories into major announcements, research, industry, tools and policy.
6. **Write the briefing.** It fills the briefing template with summaries, key points, sources, links and three takeaways.

Stop rule: Stops after one briefing per run, with at most 15 full articles fetched.

## Permissions

- Writes: loops/daily-ai-news-loop/**
- Network: venturebeat.com, techcrunch.com, www.theverge.com, www.technologyreview.com, artificialintelligence-news.com, ai.hubtoday.app
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/daily-ai-news-loop/briefings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: links and dedupe check. Memory: loops/daily-ai-news-loop/briefings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
