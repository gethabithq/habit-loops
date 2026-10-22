---
name: flow
title: Flow skill
repo: react/react
license: MIT
url: https://gethabit.dev/skills/react/flow
---

# Flow skill

The flow skill runs Flow type checking in the React repository for a chosen renderer and reports type errors with file locations, for contributors who change React code or see Flow errors.

- Install the skill: `npx skills add react/react --skill flow`
- Source: https://github.com/react/react/tree/HEAD/.claude/skills/flow
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You changed code in the React repo; You see Flow type errors; You need to check a specific renderer.
Skip it when: Your project uses TypeScript, not Flow; You work outside the React repository.

# Make it a habit: No Flow errors reach main.

On each pull request in the React repository, your agent runs yarn flow for the right renderer, reports type errors with file locations, checks new $FlowFixMe suppressions and logs the error count so the next run sees the trend.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request updated (event; GitHub Actions or Claude Code routine; `pull_request.opened or pull_request.synchronize`)
- **Verification:** yarn flow passes. Hard checks: yarn flow exits without type errors for the chosen renderer; no new $FlowFixMe comment masks a real error; yarn flow-ci passes before merge. On fail: notify, max 0 retries.
- **Memory:** Flow error count log at `loops/react-flow-check-loop/runs.md`. Read first: error counts and suppressions from the last runs.

## Steps

1. **Pick the renderer.** Choose dom-node by default, or dom-browser, native or fabric when the change touches that code.
2. **Run Flow.** Run yarn flow with the chosen renderer and never without one.
3. **Report errors.** List each type error with its file location.
4. **Check suppressions.** Look at $FlowFixMe comments in the change and flag any that hide a real problem.
5. **Check type imports.** Confirm types come from the correct package.
6. **Full check.** Run the slow yarn flow-ci before merge and log the error count.

Stop rule: Stops after one pull request per run: one yarn flow pass and one yarn flow-ci pass, no retries.

## Permissions

- Writes: loops/react-flow-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/react-flow-check-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request updated. Verification: yarn flow passes. Memory: loops/react-flow-check-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
