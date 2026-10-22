---
name: cavecrew
title: Cavecrew skill
repo: JuliusBrussee/caveman
license: Apache-2.0
url: https://gethabit.dev/skills/juliusbrussee/cavecrew
---

# Cavecrew skill

Cavecrew is a skill that tells an agent when to hand work to three compressed subagents: an investigator to find code, a builder for one or two file edits and a reviewer for diffs. For Claude Code users who want longer sessions.

- Install the skill: `npx skills add JuliusBrussee/caveman --skill cavecrew`
- Source: https://github.com/JuliusBrussee/caveman/tree/HEAD/skills/cavecrew
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You need to find where code lives; You make a one or two file fix; Your main context fills up fast.
Skip it when: You build a big feature; You want prose explanations.

# Make it a habit: Small fixes with lean context.

When a small fix task comes in, your agent chains the cavecrew subagents: the investigator finds the sites, the builder edits one or two files, the reviewer checks the diff. Each answers in compressed form. The run log keeps results.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** small fix task (manual; Claude Code; `manual run with a task of one or two files`)
- **Verification:** re-read + reviewer totals. Hard checks: builder reports verified: re-read OK; reviewer totals show zero 🔴 findings; investigator lines match path:line. On fail: stop, max 1 retries.
- **Memory:** fix results log at `loops/cavecrew-fix-loop/run-log.md`. Read first: recent tasks and builder or reviewer results.

## Steps

1. **Locate.** cavecrew-investigator returns a path:line list, or two or three run in parallel for a broad search.
2. **Pick sites.** The main thread picks one or two sites and skips the investigator if the site is already known.
3. **Edit.** cavecrew-builder makes the edit and re-reads it, or answers too-big, needs-confirm, ambiguous or regressed.
4. **Review.** cavecrew-reviewer checks the diff and returns findings with totals.
5. **Log.** The result line goes into the run log, paraphrased if a person reads it.

Stop rule: Stops after one task per run; a too-big answer ends the run and goes back to the main thread.

## Permissions

- Writes: up to two source files, loops/cavecrew-fix-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/cavecrew-fix-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: small fix task. Verification: re-read + reviewer totals. Memory: loops/cavecrew-fix-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
