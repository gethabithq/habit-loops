---
name: playwright-skill
title: Playwright Skill skill
repo: lackeyjb/playwright-skill
license: MIT
url: https://gethabit.dev/skills/lackeyjb/playwright-skill
---

# Playwright Skill skill

The playwright skill lets an agent write and run Playwright scripts for page tests, screenshots, responsive checks, login flows and other browser automation, with dev server detection. For web developers who want browser checks from chat.

- Install the skill: `npx skills add lackeyjb/playwright-skill --skill playwright-skill`
- Source: https://github.com/lackeyjb/playwright-skill/tree/HEAD/skills/playwright-skill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want to test a local site; You need desktop and mobile screenshots; You check a login flow.
Skip it when: You already have a full Playwright test suite in CI; You cannot install Chromium.

# Make it a habit: Catch broken pages every night.

Each night your agent detects the dev server, runs saved Playwright scripts for page loads, login flow and desktop and mobile screenshots, and checks the resulting page each time. A run log keeps failures and screenshot paths.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** nightly browser check (schedule; Claude Code routine or cron; `0 2 * * *`)
- **Verification:** scripts pass, page checked. Hard checks: every script run via run.js exits 0; post-login heading is visible; screenshots exist in PW_ARTIFACT_DIR. On fail: notify, max 1 retries.
- **Memory:** nightly check log at `loops/playwright-site-check-loop/runs.md`. Read first: last failures and which scripts are saved.

## Steps

1. **Set up once.** Your agent runs npm run setup in the skill folder to install Playwright and Chromium.
2. **Find the server.** It runs detectDevServers and uses the single result, or asks you.
3. **Run saved scripts.** It runs each script with node run.js, keeping them in PW_SCRIPT_DIR.
4. **Check responsive views.** It takes desktop and mobile screenshots into PW_ARTIFACT_DIR.
5. **Check the page.** It verifies the resulting page before calling a step passed.
6. **Report.** It logs actions, failures and artifact paths.

Stop rule: Stops after 10 scripts and one retry per run.

## Permissions

- Writes: playwright-tests/**, playwright-artifacts/**, loops/playwright-site-check-loop/**
- Network: localhost
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/playwright-site-check-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: nightly browser check. Verification: scripts pass, page checked. Memory: loops/playwright-site-check-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
