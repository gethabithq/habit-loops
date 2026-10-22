---
name: search
title: Bright Data Search skill
repo: brightdata/skills
license: MIT
url: https://gethabit.dev/skills/brightdata/search
---

# Bright Data Search skill

The bright data search skill runs web searches through the Bright Data CLI, with keyword SERP results from bdata search and intent-ranked pages from bdata discover. For people who need search results or URLs to scrape.

- Install the skill: `npx skills add brightdata/skills --skill search`
- Source: https://github.com/brightdata/skills/tree/HEAD/skills/search
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need Google, Bing or Yandex results; You want URLs to feed a scraper; You want pages that match an intent.
Skip it when: You need structured data from a known platform; You already have the URLs.

# Make it a habit: Fresh search results, checked.

On a schedule, your agent runs your saved queries through the Bright Data CLI, with bdata search for keyword results or bdata discover for intent. It checks the JSON, required fields and block pages, and logs the result URLs.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly query run (schedule; Claude Code routine or cron; `0 7 * * 1`)
- **Verification:** verification gate passes. Hard checks: jq . on the output returns 0; result array is not empty; each result has title and link; no block-page signatures in content. On fail: retry, max 1 retries.
- **Memory:** queries and result URLs at `loops/bright-data-search-loop/log.md`. Read first: past queries and URLs already seen, for dedup.

## Steps

1. **Run the setup gate.** Your agent checks that bdata is installed and that bdata zones works, else it stops.
2. **Pick the command.** It uses bdata search for keyword rankings and bdata discover for intent-ranked pages.
3. **Set the geo.** It sets --country, --language and --device so results can be compared run to run.
4. **Run the queries.** It runs each query with --json and pages with --page when more results are needed.
5. **Check the output.** It runs the verification gate: valid JSON, results present, title and link fields, no block pages.
6. **Dedup and log.** It removes URLs seen before and writes the new ones to the log.
7. **Hand off.** It passes chosen URLs to scrape or platform data needs to data-feeds.

Stop rule: Stops after twenty queries per run, with one retry per query.

## Permissions

- Writes: loops/bright-data-search-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/bright-data-search-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly query run. Verification: verification gate passes. Memory: loops/bright-data-search-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
