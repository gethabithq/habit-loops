---
name: brightdata-cli
title: Bright Data CLI skill
repo: brightdata/skills
license: MIT
url: https://gethabit.dev/skills/brightdata/brightdata-cli
---

# Bright Data CLI skill

The bright data cli skill helps developers scrape URLs, search Google, Bing or Yandex and run pre-built scrapers for structured data from the terminal with bdata.

- Install the skill: `npx skills add brightdata/skills --skill brightdata-cli`
- Source: https://github.com/brightdata/skills/tree/HEAD/skills/brightdata-cli
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You scrape a page to markdown or JSON; You need structured search results; You extract data from a platform with a scraper.
Skip it when: You have no Bright Data account; You need only a single static page fetch.

# Make it a habit: Weekly search results saved per keyword.

Each week your agent runs bdata search with --json for your tracked keywords and markets, saves the organic results, compares them to last week's snapshot and scrapes new top pages with bdata scrape to markdown for review.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly SERP snapshot (schedule; Claude Code routine or cron; `0 7 * * 1`)
- **Verification:** snapshot files written. Hard checks: bdata config shows a working login; every keyword has a JSON snapshot file; each snapshot holds more than zero organic results. On fail: notify, max 1 retries.
- **Memory:** weekly SERP snapshots at `loops/serp-snapshot-loop/snapshots/`. Read first: last week's snapshot per keyword.

## Steps

1. **Check setup.** Run bdata config and use bdata login if the key is invalid.
2. **Search.** Run bdata search per keyword with --json, --country and --language.
3. **Save snapshots.** Write each result to a dated file with -o.
4. **Compare.** Diff organic links against last week's snapshot.
5. **Scrape new pages.** Run bdata scrape on new top results to save them as markdown.

Stop rule: Stops after 20 keywords and 10 scraped pages per run.

## Permissions

- Writes: loops/serp-snapshot-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/serp-snapshot-loop/snapshots/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly SERP snapshot. Verification: snapshot files written. Memory: loops/serp-snapshot-loop/snapshots/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
