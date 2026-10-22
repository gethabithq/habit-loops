---
name: playwright-stealth-verify
title: Playwright Stealth Verify skill
repo: liarjsdev/liarjs-skills
license: MIT
url: https://gethabit.dev/skills/liarjsdev/playwright-stealth-verify
---

# Playwright Stealth Verify skill

The playwright stealth verify skill checks whether a Playwright, Puppeteer, Selenium or CDP browser shows a coherent fingerprint, using liarjs checkPage on a Page you already have. For QA engineers who want fingerprint assertions in tests.

- Install the skill: `npx skills add liarjsdev/liarjs-skills --skill playwright-stealth-verify`
- Source: https://github.com/liarjsdev/liarjs-skills/tree/HEAD/skills/playwright-stealth-verify
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You measure a stealth plugin's effect; A headless setup needs checking; You want fingerprint asserts in tests.
Skip it when: You need evasions, not measurements; You do not drive a browser from code.

# Make it a habit: Automation harness stays coherent per PR.

On every pull request that changes your Playwright or Puppeteer harness, your test suite calls checkPage from liarjs on a real Page and asserts the score and zero critical checks. A run log keeps the failing ids per pull request.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes test harness (event; GitHub Actions; `pull_request paths: playwright.config.*, harness launch code`)
- **Verification:** checkPage assertions pass. Hard checks: result.score is 85 or above; no check has status bad; liarjs is pinned as a dev dependency in the lockfile. On fail: notify, max 0 retries.
- **Memory:** failing ids per PR at `loops/harness-coherence-test-loop/run-log.md`. Read first: check ids that failed on recent pull requests.

## Steps

1. **Pin liarjs.** Install it with npm install --save-dev liarjs so the version sits in the lockfile.
2. **Measure the page.** Call checkPage(page) on the harness's own Page with its real flags, plugins and proxy.
3. **Assert.** Expect the score at 85 or above and zero checks with status bad.
4. **Read the ids.** Map failures like webdriver, native-integrity, headless-ua and worker-consistency to their cause.
5. **Log and hand off.** Log the failing ids and send full reports to fingerprint-failure-triage.

Stop rule: One test run per pull request, no retries.

## Permissions

- Writes: loops/harness-coherence-test-loop/**, test files
- Network: liarjs.dev
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/harness-coherence-test-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes test harness. Verification: checkPage assertions pass. Memory: loops/harness-coherence-test-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
