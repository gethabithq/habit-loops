---
name: ai-seo
title: AI SEO skill
repo: coreyhaines31/marketingskills
license: MIT
url: https://gethabit.dev/skills/coreyhaines31/ai-seo
---

# AI SEO skill

AI SEO is a skill that helps content get cited in AI answers from Google AI Overviews, ChatGPT, Perplexity and others, with audits, extractable structure, bot access rules and monitoring. For marketers and SEO teams.

- Install the skill: `npx skills add coreyhaines31/marketingskills --skill ai-seo`
- Source: https://github.com/coreyhaines31/marketingskills/tree/HEAD/skills/ai-seo
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want to be cited in AI answers; You want to check AI bot rules in robots.txt; You want to track AI visibility over time.
Skip it when: You need a classic technical SEO audit; You only need schema markup added.

# Make it a habit: Know where AI answers cite you.

Each month your agent gives you the top 20 queries. You run them in your own ChatGPT, Perplexity and Google, or export answers from a monitoring tool. The agent records who gets cited, checks the AI bot rules in robots.txt and turns gaps into fixes.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly visibility check (schedule; Claude Code routine; `0 7 1 * *`)
- **Verification:** full sample logged. Hard checks: 20 queries are logged; each query has at least 3 runs per platform; every rate shows its sample size; each AI user agent group is checked in robots.txt. On fail: retry, max 1 retries.
- **Memory:** monthly cite rates at `loops/ai-visibility-loop/run-log.md`. Read first: last month's cite rates and open fixes per query.

## Steps

1. **Read context.** Read .agents/product-marketing.md if it exists and the query list from last month.
2. **Hand over queries.** Give you the top 20 queries to run 3 to 5 times per platform in your own accounts, or to export from your monitoring tool.
3. **Record citations.** From the answers you paste, log if you are cited, who is, which page, and the rate with its sample size.
4. **Check bot access.** Read robots.txt on your domain for search, user, training and Google-Extended agents separately.
5. **Check extractability.** Run the extractability checklist on pages that lost or never had citations.
6. **Turn gaps into work.** Fix pages that state facts vaguely and list cited third-party sources as targets.

Stop rule: Stops after one monthly log with at most 20 queries and 5 runs per query per platform.

## Permissions

- Writes: loops/ai-visibility-loop/**
- Network: your own domain (robots.txt and priority pages)
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ai-visibility-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly visibility check. Verification: full sample logged. Memory: loops/ai-visibility-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
