---
name: bright-data-best-practices
title: Bright Data Best Practices skill
repo: brightdata/skills
license: MIT
url: https://gethabit.dev/skills/brightdata/bright-data-best-practices
---

# Bright Data Best Practices skill

Bright data best practices is a reference skill for developers who build Bright Data integrations: Web Unlocker, SERP API, Web Scraper API and Browser API, with auth, parameters and the right API for each job.

- Install the skill: `npx skills add brightdata/skills --skill bright-data-best-practices`
- Source: https://github.com/brightdata/skills/tree/HEAD/skills/bright-data-best-practices
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You scrape pages at scale; You need structured search results; You automate a browser behind bot checks.
Skip it when: You do not use Bright Data; You need raw proxy routing only.

# Make it a habit: Weekly search ranks for your keywords.

Every week, your agent sends your keywords to the Bright Data SERP API with brd_json=1, reads the organic ranks for your site and compares them with last week. It picks the most specific Bright Data API for each job.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly rank check (schedule; Claude Code routine or cron; `0 7 * * 1`)
- **Verification:** parsed results returned. Hard checks: each request returns status 200; each response has at least one organic result; every query URL includes brd_json=1. On fail: retry, max 1 retries.
- **Memory:** weekly rank log at `loops/serp-rank-watch-loop/run-log.md`. Read first: last week's rank per keyword.

## Steps

1. **Check setup.** Read references/cli-setup.md and confirm BRIGHTDATA_API_KEY and BRIGHTDATA_SERP_ZONE are set.
2. **Pick the API.** Use the SERP API for search results, not Web Unlocker or Browser API.
3. **Send queries.** POST each Google search URL with brd_json=1, gl and hl to the request endpoint.
4. **Read ranks.** Find your site's rank in the organic array for each keyword.
5. **Compare and log.** Compare with last week and write changes into the run log.

Stop rule: Stops after 50 keywords per run, with one retry each.

## Permissions

- Writes: loops/serp-rank-watch-loop/**
- Network: api.brightdata.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/serp-rank-watch-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly rank check. Verification: parsed results returned. Memory: loops/serp-rank-watch-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
