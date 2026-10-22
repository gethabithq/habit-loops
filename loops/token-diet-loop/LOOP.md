---
name: caveman
title: Caveman skill
repo: JuliusBrussee/caveman
license: Apache-2.0
url: https://gethabit.dev/skills/juliusbrussee/caveman
---

# Caveman skill

The caveman skill makes your agent answer in short, plain sentences. Fewer output tokens per task means a lower bill and faster runs.

- Install the skill: `npx skills add JuliusBrussee/caveman --skill caveman`
- Source: https://github.com/JuliusBrussee/caveman
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Your agent writes long answers you skim anyway; Token cost matters.
Skip it when: You need long explanations for others to read.

# Make it a habit: Every session short and cheap.

A hook turns caveman mode on in every new session, so you never type /caveman again. Once a week the loop compares cost per task with the baseline. If tests pass less often, it switches to a lighter mode.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every new session (event; Claude Code hook, plus a weekly routine for the cost check; `SessionStart hook sets caveman mode`)
- **Verification:** cost down, tests same. Hard checks: the hook reports caveman mode at session start; cost per task below baseline in the weekly check; test pass rate unchanged. On fail: stop, max 0 retries.
- **Memory:** cost log at `cost-log.csv`. Read first: baseline, current mode and the last four weeks.

## Steps

1. **Turn it on.** A SessionStart hook starts caveman mode in every new session.
2. **Work as usual.** Your agent answers short. Code, commands and facts stay complete.
3. **Measure weekly.** Once a week the loop reads cost per task from your agent logs.
4. **Compare.** It checks the cost against the baseline in the cost log.
5. **Check quality.** Tests must pass as often as before. If not, it switches to a lighter mode.

Stop rule: At most one mode change per week.

## Permissions

- Writes: cost-log.csv, .claude/settings.json
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`cost-log.csv`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every new session. Verification: cost down, tests same. Memory: cost-log.csv. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
