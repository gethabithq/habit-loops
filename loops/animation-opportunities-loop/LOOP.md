---
name: find-animation-opportunities
title: Find Animation Opportunities skill
repo: emilkowalski/skills
license: MIT
url: https://gethabit.dev/skills/emilkowalski/find-animation-opportunities
---

# Find Animation Opportunities skill

Find animation opportunities is a read-only skill that searches a UI for moments that should animate, rejects the rest through a strict gate, and proposes exact motion values. For design engineers who want restraint.

- Install the skill: `npx skills add emilkowalski/skills --skill find-animation-opportunities`
- Source: https://github.com/emilkowalski/skills/tree/HEAD/skills/find-animation-opportunities
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You ask what could be animated here; You want the UI to feel more alive; You want exact motion values per spot.
Skip it when: You want to fix animations that already exist; You want the code written for you.

# Make it a habit: Only motion that earns its place.

Each week your agent sweeps the interface for places that should animate, runs every candidate through the four-question gate and reports a short table with exact values plus rejected candidates. It never changes code. The report file keeps what was suggested and rejected.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly UI sweep (schedule; Claude Code routine; `0 9 * * 1`)
- **Verification:** report format holds. Hard checks: no source file changed (git diff is empty); at most 7 suggestions in the table; rejected candidates section lists 2 to 5 items; every suggestion has file:line evidence. On fail: retry, max 1 retries.
- **Memory:** past suggestions and rejections at `loops/animation-opportunities-loop/report.md`. Read first: suggestions and rejected candidates from the last sweep.

## Steps

1. **Recon.** Find the stack, motion libraries, easing and duration tokens, and a rough frequency map of the surfaces.
2. **Sweep.** Check every seam class in the hunt list and record file:line evidence or clear it.
3. **Gate.** Run each candidate through frequency, purpose, speed and function, and reject what fails.
4. **Report.** Write the opportunities table with exact values, the rejected candidates and a short verdict.
5. **Hand off.** Point each row at improve-animations plan for the implementation plan.

Stop rule: Stops after one sweep and at most 7 suggestions per run.

## Permissions

- Writes: loops/animation-opportunities-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/animation-opportunities-loop/report.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly UI sweep. Verification: report format holds. Memory: loops/animation-opportunities-loop/report.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
