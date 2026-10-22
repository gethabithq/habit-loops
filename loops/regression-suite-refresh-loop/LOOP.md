---
name: qa-test-planner
title: QA Test Planner skill
repo: softaworks/agent-toolkit
license: MIT
url: https://gethabit.dev/skills/softaworks/qa-test-planner
---

# QA Test Planner skill

Qa test planner generates test plans, manual test cases, regression suites and bug reports, with optional Figma design validation. For QA engineers who need structured, reproducible test artifacts.

- Install the skill: `npx skills add softaworks/agent-toolkit --skill qa-test-planner`
- Source: https://github.com/softaworks/agent-toolkit/tree/HEAD/dist/plugins/qa-test-planner/skills/qa-test-planner
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You plan testing for a feature; You build a regression suite; You write a bug report.
Skip it when: You want automated test code; You need load testing only.

# Make it a habit: Regression suite tracks new features.

When a feature ships, your agent uses the QA test planner to add manual test cases for it, update the regression suite with execution order and priorities, and keep each case's steps and expected results complete. A suite file keeps the cases and coverage matrix.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** feature shipped (event; Claude Code routine; `pull_request.closed && merged`)
- **Verification:** case checklist + review. Hard checks: every test step has an expected result; every case has preconditions and a priority; every case lists its test data. On fail: notify, max 0 retries.
- **Memory:** regression suite file at `loops/regression-suite-refresh-loop/suite.md`. Read first: existing test cases, the coverage matrix and critical paths.

## Steps

1. **Analyze the feature.** Parse the shipped feature and decide which test types it needs.
2. **Write test cases.** Write step-by-step cases with expected results, preconditions, test data and priority.
3. **Cover edge cases.** Add boundary values, nulls and negative cases, not just the happy path.
4. **Place in the suite.** Add the cases to the smoke, targeted or full regression suite with an execution order.
5. **Update coverage.** Update the coverage matrix and note any gaps.
6. **Review.** Check the cases against the verification checklist with a QA engineer.

Stop rule: Stops after one feature's test cases per run.

## Permissions

- Writes: loops/regression-suite-refresh-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/regression-suite-refresh-loop/suite.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: feature shipped. Verification: case checklist + review. Memory: loops/regression-suite-refresh-loop/suite.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
