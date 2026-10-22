---
name: test
title: React test skill
repo: react/react
license: MIT
url: https://gethabit.dev/skills/react/test
---

# React test skill

The react test skill runs tests for the React codebase on the source, experimental, stable, classic and www channels, with the right yarn command and flags. For contributors to React core.

- Install the skill: `npx skills add react/react --skill test`
- Source: https://github.com/react/react/tree/HEAD/.claude/skills/test
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You change React core code; You test a channel-specific behavior; You test __VARIANT__ flags.
Skip it when: You test your own React app; You need a type check, not tests.

# Make it a habit: React tests run per channel.

When a change to React core lands in a pull request, your agent runs the matching tests with yarn test on the right release channel, with --silent and --no-watchman. It reports failures and keeps a run log of failing patterns.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** React core pull request (event; GitHub Actions or Claude Code routine; `pull_request.opened or synchronize`)
- **Verification:** tests pass per channel. Hard checks: yarn test exits with code 0 for the pattern; a test pattern is given, never the full suite; both www and www variant false pass when __VARIANT__ flags are touched. On fail: notify, max 0 retries.
- **Memory:** failing patterns log at `loops/react-channel-test-loop/log.md`. Read first: patterns and channels that failed last run.

## Steps

1. **Pick the pattern.** The agent takes the test pattern from the changed files, because a run without one is very slow.
2. **Parse the channel.** It reads the channel from the arguments and uses source when none is given.
3. **Map to yarn.** It picks yarn test, yarn test -r=experimental, yarn test-stable, yarn test-classic or yarn test-www.
4. **Run quietly.** Every run uses --silent so only failures show, and --no-watchman for sandboxes.
5. **Test both variants.** For __VARIANT__ flags it runs test-www once normally and once with --variant=false.
6. **Explain skips.** If a test is skipped, it checks the @gate pragma with the feature-flags skill.
7. **Report.** It reports results and failures and writes the failing patterns to the log.

Stop rule: Stops after one pull request per run, with at most six channel runs.

## Permissions

- Writes: loops/react-channel-test-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/react-channel-test-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: React core pull request. Verification: tests pass per channel. Memory: loops/react-channel-test-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
