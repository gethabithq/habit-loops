---
name: jscpd
title: jscpd skill
repo: kucherenko/jscpd
license: MIT
url: https://gethabit.dev/skills/kucherenko/jscpd
---

# jscpd skill

The jscpd skill runs the jscpd copy-paste detector across 220+ languages, finds exact, renamed and near-miss clones, and ranks refactoring hotspots with a codebase summary. For developers and agents cleaning up duplicated code.

- Install the skill: `npx skills add kucherenko/jscpd --skill jscpd`
- Source: https://github.com/kucherenko/jscpd/tree/HEAD/skills/jscpd
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you suspect copy-pasted code; you want a duplication gate in CI; you need refactoring hotspots.
Skip it when: the codebase is tiny; you need a full linter.

# Make it a habit: Copy-pasted code stops growing.

Every week the agent runs jscpd with the ai reporter and a summary, fails the run when duplication passes your threshold, and lists the top hotspots. It keeps each run's duplication share so the next run sees the trend.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly duplication scan (schedule; GitHub Actions or cron; `0 7 * * 1`)
- **Verification:** threshold not exceeded. Hard checks: npx jscpd --threshold N exits without error; duplication share is not above the last run's share. On fail: notify, max 0 retries.
- **Memory:** duplication trend log at `loops/duplicate-code-loop/log.md`. Read first: duplication share and top hotspot files of the last run.

## Steps

1. **Read last run.** Open the log to get the last duplication share and hotspot files.
2. **Exact clone pass.** Run npx jscpd --reporters ai --summary --no-tips with --ignore for node_modules and dist.
3. **Check threshold.** Run with --threshold so the scan exits with an error when duplication is too high.
4. **Optional renamed pass.** If exact clones are handled, run one --ignore-identifiers --min-tokens 70 pass and treat hits as leads.
5. **Rank hotspots.** Pick the large files with a high dup% from the summary as refactoring targets.
6. **Hand to refactoring.** Pass the top targets to the dry-refactoring skill for a guided cleanup.
7. **Write the log.** Save the share, clone count, flags used and top files for the next run.

Stop rule: One scan per run, at most one extra noisy pass and the top 10 hotspots.

## Permissions

- Writes: loops/duplicate-code-loop/, .jscpd.json
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/duplicate-code-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly duplication scan. Verification: threshold not exceeded. Memory: loops/duplicate-code-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
