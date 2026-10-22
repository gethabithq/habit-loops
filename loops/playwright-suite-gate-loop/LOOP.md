---
name: playwright-automation
title: Playwright Automation skill
repo: petrkindlmann/qa-skills
license: MIT
url: https://gethabit.dev/skills/petrkindlmann/playwright-automation
---

# Playwright Automation skill

Playwright automation is a skill for QA and frontend engineers who write production-grade Playwright tests in TypeScript with page objects, fixtures, user-facing locators, parallel runs, CI sharding and version checks.

- Install the skill: `npx skills add petrkindlmann/qa-skills --skill playwright-automation`
- Source: https://github.com/petrkindlmann/qa-skills/tree/HEAD/skills/playwright-automation
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You start a Playwright suite; You write page objects; You set up sharding in CI.
Skip it when: You fix one flaky test; You need deep WCAG audits.

# Make it a habit: E2E tests that stay stable.

When a pull request adds or changes Playwright tests, your agent checks them with the skill's own gates: tests list and parse, no waitForTimeout or page.pause, types compile and locators stay user-facing. It logs repeat offenders.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes e2e tests (event; GitHub Actions or Claude Code routine; `pull_request.opened touching e2e/`)
- **Verification:** list, grep and tsc. Hard checks: npx playwright test --list discovers the tests; grep -rn 'waitForTimeout\|page.pause' e2e/ prints nothing; npx tsc --noEmit passes; playwright.config.ts sets forbidOnly for CI. On fail: retry, max 2 retries.
- **Memory:** QA project context at `.agents/qa-project-context.md`. Read first: language, browsers, team maturity and known gaps.

## Steps

1. **Read context.** Read .agents/qa-project-context.md and ask the user only what it does not answer.
2. **Check versions.** Run npm ls @playwright/test playwright and npx playwright --version before version-sensitive APIs.
3. **Check locators.** Prefer getByRole, getByLabel and getByTestId over CSS or xpath.
4. **Check structure.** Confirm fixtures for setup, page objects without expect and isolated test data.
5. **Run the gates.** Run --list, the waitForTimeout grep and tsc --noEmit.
6. **Route special cases.** Send flaky fixes to test-reliability and visual baselines to visual-testing.

Stop rule: Stops after one pull request per run, with two retries.

## Permissions

- Writes: e2e/**, playwright.config.ts, .agents/qa-project-context.md
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.agents/qa-project-context.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes e2e tests. Verification: list, grep and tsc. Memory: .agents/qa-project-context.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
