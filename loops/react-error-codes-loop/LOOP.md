---
name: extract-errors
title: Extract Errors skill
repo: react/react
license: MIT
url: https://gethabit.dev/skills/react/extract-errors
---

# Extract Errors skill

The extract errors skill runs the React error code extraction, reports new error messages that need codes and checks that codes are up to date. It is for contributors to the React repository.

- Install the skill: `npx skills add react/react --skill extract-errors`
- Source: https://github.com/react/react/tree/HEAD/.claude/skills/extract-errors
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add new error messages to React; You see unknown error code warnings; You review a React pull request.
Skip it when: You do not work in the React repository; Your change adds no error messages.

# Make it a habit: Every new error gets a code.

On every pull request in the React repository, your agent runs yarn extract-errors, reports any new error messages that still need a code and checks that the error codes are up to date. A run log keeps which messages were flagged.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions or Claude Code routine; `pull_request.opened or synchronize`)
- **Verification:** error codes up to date. Hard checks: yarn extract-errors finishes without failure; count of new errors without a code is zero. On fail: notify, max 0 retries.
- **Memory:** error code log at `loops/react-error-codes-loop/run-log.md`. Read first: messages flagged in earlier runs.

## Steps

1. **Read the log.** The agent reads which error messages were flagged before.
2. **Extract errors.** It runs yarn extract-errors on the branch.
3. **Report new errors.** It lists every new error message that still needs a code.
4. **Check the codes.** It confirms the error codes are up to date, or sends a note on the pull request run.
5. **Log the result.** The flagged messages and the outcome go into the run log.

Stop rule: Stops after one pull request per run, with no retries.

## Permissions

- Writes: loops/react-error-codes-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/react-error-codes-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: error codes up to date. Memory: loops/react-error-codes-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
