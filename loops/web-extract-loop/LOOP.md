---
name: extract
title: Extract skill
repo: actionbook/actionbook
license: Apache-2.0
url: https://gethabit.dev/skills/actionbook/extract
---

# Extract skill

The extract skill helps developers and analysts pull structured data from websites and get a re-runnable Playwright script plus JSON or CSV output, handling hydration, infinite scroll and pagination.

- Install the skill: `npx skills add actionbook/actionbook --skill extract`
- Source: https://github.com/actionbook/actionbook/tree/HEAD/skills/extract
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You scrape a product list or table; You need a re-runnable extract script; A page uses infinite scroll or pagination.
Skip it when: The site offers an API; The site forbids scraping.

# Make it a habit: Fresh structured data from websites.

On a schedule your agent re-runs the saved Playwright extract script, validates exit code, record count and field coverage, and spot-checks against the page. If selectors broke, it re-discovers them with actionbook and regenerates the script.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily extract run (schedule; Claude Code routine or cron; `0 5 * * *`)
- **Verification:** validation table passes. Hard checks: node extract_<domain>_<slug>.cjs exits 0; output file exists and is not empty; record count is above zero; every declared field has a value in at least 90% of records. On fail: retry, max 2 retries.
- **Memory:** extract run log at `loops/web-extract-loop/run-log.md`. Read first: last record count and which selectors needed fixes.

## Steps

1. **Run the script.** Run node extract_<domain>_<slug>.cjs to write output.json.
2. **Validate.** Check exit code, output file, record count and field coverage.
3. **Spot-check.** Compare the first and last record with actionbook browser text.
4. **Repair selectors.** On failure, try actionbook search and get, then browser snapshot only for failed fields.
5. **Regenerate.** Update the script with guardrails for pages, scrolls and timeouts, then re-run.

Stop rule: Stops after one site per run, with at most 2 repair attempts; stops at a captcha and tells you.

## Permissions

- Writes: ./extract_*.cjs, ./output.json, loops/web-extract-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/web-extract-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily extract run. Verification: validation table passes. Memory: loops/web-extract-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
