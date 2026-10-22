---
name: frontend-testing-best-practices
title: Frontend Testing Best Practices skill
repo: sergiodxa/agent-skills
license: MIT
url: https://gethabit.dev/skills/sergiodxa/frontend-testing-best-practices
---

# Frontend Testing Best Practices skill

The frontend testing best practices skill helps frontend developers write and review tests that favor E2E over unit tests, keep mocking minimal and test behavior instead of implementation.

- Install the skill: `npx skills add sergiodxa/agent-skills --skill frontend-testing-best-practices`
- Source: https://github.com/sergiodxa/agent-skills/tree/HEAD/skills/frontend-testing-best-practices
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You decide what kind of test to write; You review test code; You refactor a brittle test suite.
Skip it when: You test a backend library; Your team requires component unit tests.

# Make it a habit: Tests check behavior, not implementation.

On every pull request with test changes, your agent checks the six rules: E2E over unit tests, no React component unit tests, at most two mocks, E2E tests in e2e/tests/, accessible selectors and unit tests only for pure functions. A log keeps repeat findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** test files changed (event; GitHub Actions or Claude Code routine; `pull_request touches test or spec files`)
- **Verification:** tests pass, rules hold. Hard checks: tests pass; no unit test renders a React component; no test file has 3 or more vi.mock calls; E2E tests live in e2e/tests/; no CSS class selectors in E2E tests. On fail: notify, max 0 retries.
- **Memory:** test rule findings at `loops/frontend-test-review-loop/run-log.md`. Read first: rules flagged in earlier reviews.

## Steps

1. **List test changes.** Collect new and changed unit and E2E tests in the pull request.
2. **Check strategy.** Flag component unit tests and heavy mocking that should be E2E tests.
3. **Check structure.** Confirm E2E tests sit in e2e/tests/ and unit tests sit beside pure functions.
4. **Check selectors.** Prefer role, then label, then text, then test ID.
5. **Run and report.** Run the tests and list findings by rule.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/frontend-test-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/frontend-test-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: test files changed. Verification: tests pass, rules hold. Memory: loops/frontend-test-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
