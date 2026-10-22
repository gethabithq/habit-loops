---
name: ui4-convert-tests
title: UI4 Convert Tests skill
repo: payloadcms/payload
license: MIT
url: https://gethabit.dev/skills/payloadcms/ui4-convert-tests
---

# UI4 Convert Tests skill

The ui4 convert tests skill helps Payload developers find and fix e2e tests broken by UI changes, by analyzing the diff for selector, structure and text changes and updating helpers first.

- Install the skill: `npx skills add payloadcms/payload --skill ui4-convert-tests`
- Source: https://github.com/payloadcms/payload/tree/HEAD/.agents/skills/ui4-convert-tests
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: CI fails after UI changes; You finished a UI change and need tests updated; Buttons moved into a popup.
Skip it when: You do not work in the Payload repo; Your tests are unit tests only.

# Make it a habit: E2E tests follow UI changes.

When UI changes are done, your agent diffs UI files against main, sorts changes into selector, structure and text, finds affected e2e tests and helpers, confirms they fail, fixes helpers first, and re-runs the tests on an isolated port.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** UI change ready (event; GitHub Actions or Claude Code routine; `e2e CI fails after changes in packages/ui/src`)
- **Verification:** affected e2e tests pass. Hard checks: affected tests fail before fixes; PORT=3150 pnpm test:e2e <suite> --max-failures=1 passes after fixes; tests that already passed were not changed. On fail: retry, max 2 retries.
- **Memory:** selector changes log at `loops/ui4-test-fix-loop/run-log.md`. Read first: selector and helper changes from earlier runs.

## Steps

1. **Analyze the diff.** Run git diff main on packages/ui/src .tsx and .css files and build a change summary.
2. **Find tests.** Grep test/ for component names, selectors and changed text.
3. **Read the tests.** Read each test and check for shared helpers in test/<feature>/helpers/.
4. **Confirm failures.** Run the affected suite on PORT=3150 with --max-failures=1.
5. **Fix.** Fix helpers first, then tests: selectors, popup steps and text assertions.
6. **Verify.** Re-run the same tests and commit only when they pass.

Stop rule: Stops after one test suite per run, with at most 2 fix rounds.

## Permissions

- Writes: test/**, loops/ui4-test-fix-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ui4-test-fix-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: UI change ready. Verification: affected e2e tests pass. Memory: loops/ui4-test-fix-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
