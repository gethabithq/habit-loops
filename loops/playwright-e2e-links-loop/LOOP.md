---
name: playwright-testing
title: Playwright E2E Testing skill
repo: alinaqi/maggy
license: MIT
url: https://gethabit.dev/skills/alinaqi/playwright-testing
---

# Playwright E2E Testing skill

The playwright e2e testing skill sets up end-to-end tests with Playwright: page objects, role-based locators, shared auth, network mocks, visual checks, dead link detection and CI. For web teams who want reliable browser tests.

- Install the skill: `npx skills add alinaqi/maggy --skill playwright-testing`
- Source: https://github.com/alinaqi/maggy/tree/HEAD/skills/playwright-testing
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: writing E2E tests for a web app; checking a site for dead links; running browser tests in CI.
Skip it when: you only need unit tests; the app has no web interface.

# Make it a habit: No broken flows or dead links.

On every push to main and weekly, your agent runs the Playwright end-to-end suite and the dead link tests across browsers, then reports failures with traces. The HTML report and a run log keep what failed last time.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** push to main (event; GitHub Actions; `push to main, plus weekly cron 0 6 * * 1`)
- **Verification:** E2E and link tests. Hard checks: npx playwright test passes; links.spec.ts finds zero dead links; no broken images on the homepage. On fail: notify, max 2 retries.
- **Memory:** E2E failure log at `loops/playwright-e2e-links-loop/run-log.md`. Read first: tests and links that failed last run.

## Steps

1. **Install browsers.** Your agent installs dependencies and Playwright browsers with npx playwright install.
2. **Auth setup.** The setup project logs in once and stores the auth state for the other tests.
3. **Run E2E suite.** It runs npx playwright test with page objects and role-based locators across the configured projects.
4. **Check links.** It runs links.spec.ts and the image check so dead links and broken images fail the run.
5. **Report.** On failure it uploads the playwright-report and keeps traces from the first retry.

Stop rule: Stops after one full suite run per trigger, with at most 2 retries per failing test.

## Permissions

- Writes: e2e/**, playwright-report/**, .auth/**, loops/playwright-e2e-links-loop/**
- Network: localhost
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/playwright-e2e-links-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: push to main. Verification: E2E and link tests. Memory: loops/playwright-e2e-links-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
