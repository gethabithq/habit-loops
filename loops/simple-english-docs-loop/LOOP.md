---
name: simple-english
title: Simple English skill
repo: aminblg/simpleenglish
license: MIT
url: https://gethabit.dev/skills/aminblg/simple-english
---

# Simple English skill

The simple english skill rewrites or checks documentation in plain English based on ASD-STE100: short sentences, active voice, one word per meaning. For developers and writers whose readers are outside the field or not native speakers.

- Install the skill: `npx skills add aminblg/simpleenglish --skill simple-english`
- Source: https://github.com/aminblg/simpleenglish/tree/HEAD/skills/simple-english
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write READMEs or runbooks; Readers are non-native speakers; You want AI slop removed.
Skip it when: You write marketing or brand copy; You need certified STE compliance.

# Make it a habit: Every doc reads plain English.

When a pull request changes documentation, your agent checks the changed prose with simple english, rewrites what breaks the rules and runs the self-check. It logs each fixed file so the next run starts with the open hits.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** docs change in PR (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*.md`)
- **Verification:** self-check finds zero hits. Hard checks: no em-dash or semicolon left in the prose; no should, may or has been left; three longest sentences stay at 25 words or less; code, flags and file paths are unchanged in the diff. On fail: retry, max 2 retries.
- **Memory:** log of fixed files at `loops/simple-english-docs-loop/run-log.md`. Read first: files with open rule hits from the last run.

## Steps

1. **Find changed docs.** The run collects the documentation files that the pull request changed.
2. **Check the text.** In CHECK mode the agent opens references/rule-catalog.md and lists each violation with its rule number and a rewrite.
3. **Pick the mode.** For runbooks, release notes or error messages the agent reads references/use-cases.md first, and Strict mode only applies when you name STE.
4. **Rewrite the prose.** The agent rewrites the prose with short active sentences and leaves code, commands and facts as they are.
5. **Run the self-check.** The agent searches for the banned marks and words and counts the longest sentences, then fixes each hit.
6. **Log the run.** The run writes each file and its remaining hits into the run log.

Stop rule: Stops after 10 changed files or 2 retries per file.

## Permissions

- Writes: **/*.md, loops/simple-english-docs-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/simple-english-docs-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: docs change in PR. Verification: self-check finds zero hits. Memory: loops/simple-english-docs-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
