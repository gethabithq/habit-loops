---
name: baseline-ui
title: Baseline UI skill
repo: ibelick/ui-skills
license: MIT
url: https://gethabit.dev/skills/ibelick/baseline-ui
---

# Baseline UI skill

The baseline ui skill helps frontend developers clean up AI-generated interfaces with fixed rules for spacing, typography, components, animation, layout and design.

- Install the skill: `npx skills add ibelick/ui-skills --skill baseline-ui`
- Source: https://github.com/ibelick/ui-skills/tree/HEAD/skills/baseline-ui
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A UI needs a fast polish pass; You review AI-generated components; You want one shared UI baseline.
Skip it when: Your project does not use Tailwind CSS; You are building a custom design system from scratch.

# Make it a habit: UI slop gets caught on merge.

When a pull request changes UI files, your agent reviews each one with baseline-ui, reports violations with the exact line and a fix, and keeps a log of the rules broken most often.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches UI files (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*.tsx, **/*.jsx, **/*.css`)
- **Verification:** no baseline rule violations. Hard checks: no h-screen class in changed files; every icon-only button has an aria-label; no arbitrary z-* values; no paste blocking on input or textarea; each reported violation quotes the exact line. On fail: notify, max 1 retries.
- **Memory:** violation log at `loops/baseline-ui-review-loop/run-log.md`. Read first: rules broken most often before.

## Steps

1. **Read the log.** The agent reads which baseline rules were broken most often.
2. **Pick changed files.** It lists changed component and style files.
3. **Review each file.** It runs /baseline-ui <file> on each one.
4. **Check every area.** It checks stack, components, interaction, animation, typography, layout, performance and design rules.
5. **Report.** For each violation it gives the quoted line, a short reason and a code-level fix.
6. **Log.** It adds the broken rules to the run log.

Stop rule: Stops after reviewing at most 10 changed files per pull request.

## Permissions

- Writes: loops/baseline-ui-review-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/baseline-ui-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches UI files. Verification: no baseline rule violations. Memory: loops/baseline-ui-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
