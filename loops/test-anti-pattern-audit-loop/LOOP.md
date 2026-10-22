---
name: test-anti-patterns
title: Test Anti-Patterns skill
repo: dotnet/skills
license: MIT
url: https://gethabit.dev/skills/dotnet/test-anti-patterns
---

# Test Anti-Patterns skill

Test anti-patterns audits a test file or suite in any language and produces a severity-ranked report of tests that verify nothing, swallowed exceptions, flaky or order-dependent tests, duplication and magic values. For developers reviewing test quality.

- Install the skill: `npx skills add dotnet/skills --skill test-anti-patterns`
- Source: https://github.com/dotnet/skills/tree/HEAD/plugins/dotnet-test/skills/test-anti-patterns
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You ask if your tests are good; Your tests are flaky; You review a test pull request.
Skip it when: You want new tests written; You want to run the tests.

# Make it a habit: Tests that prove nothing get caught.

On every pull request that touches tests, your agent audits the changed test files for anti-patterns, from missing assertions and swallowed exceptions to flaky sleeps and order coupling. It accounts for every test, gives exact fixes for critical findings and logs the report.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** test files change (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*Tests*/**, **/test_*.py, **/*.test.*`)
- **Verification:** complete, consistent report. Hard checks: the reviewed test count equals the discovered test count; summary counts equal the listed findings; every Critical and High finding has a fix with an exact expected value. On fail: notify, max 0 retries.
- **Memory:** test audit log at `loops/test-anti-pattern-audit-loop/log.md`. Read first: open Critical and High findings from earlier audits.

## Steps

1. **Detect language.** Find the test files in the workspace and identify language and framework.
2. **Inventory tests.** List every test method and class-level fixture before reading bodies.
3. **Scan the catalog.** Check each test against the Critical, High, Medium and Low anti-patterns.
4. **Check production code.** Open the production symbol behind each suspicious test to judge the oracle.
5. **Calibrate severity.** Apply the severity rules and the not-an-issue list, never inflating findings.
6. **Report.** Write summary, findings with locations and fixes, adjacent gaps and positive observations.

Stop rule: Stops after the changed test files of one pull request.

## Permissions

- Writes: loops/test-anti-pattern-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/test-anti-pattern-audit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: test files change. Verification: complete, consistent report. Memory: loops/test-anti-pattern-audit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
