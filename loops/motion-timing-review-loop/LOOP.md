---
name: animation-principles
title: Animation Principles skill
repo: iart-ai/motion-design-skills
license: MIT
url: https://gethabit.dev/skills/iart-ai/animation-principles
---

# Animation Principles skill

The animation principles skill decides how things should move: timing, easing curves, stagger, weight and rhythm, returning concrete durations, cubic-bezier values and spring settings, for designers and motion developers.

- Install the skill: `npx skills add iart-ai/motion-design-skills --skill animation-principles`
- Source: https://github.com/iart-ai/motion-design-skills/tree/HEAD/skills/animation-principles
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: motion feels stiff or floaty; choosing an easing curve and duration; staggering a list reveal.
Skip it when: picking an animation library; static layout work.

# Make it a habit: Motion never feels stiff again.

When an animation change lands, your agent reviews its timing, easing, stagger and weight: no linear on discrete events, durations matched to element size, stagger capped. It hands back concrete numbers. Accepted values stay in a motion notes file.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** animation change submitted (event; Claude Code routine; `pull request labelled motion`)
- **Verification:** timing rules + critic. Hard checks: linear easing only on continuous loops; every duration sits in the range for its element type; list stagger total stays under about 800ms; with 3+ elements, no more than about 1/3 move at once. Critic: claude-opus-5-5, pass at 16/20. On fail: retry, max 1 retries.
- **Memory:** motion notes at `loops/motion-timing-review-loop/notes.md`. Read first: accepted curves, durations and staggers.

## Steps

1. **Settle the pillars.** Your agent names the emotional intent, the micro-story and the craft goal first.
2. **Check the layers.** It confirms primary, secondary and ambient motion each have a role.
3. **Check easing.** Enters ease out, exits ease in, moves ease in and out.
4. **Check timing.** Durations follow the element type and grow with distance and size.
5. **Check stagger.** Groups stagger by 40-80ms for lists and 20-40ms for dense grids.
6. **Diagnose and fix.** It names the failure, such as stiff or floaty, and gives exact new values.

Stop rule: Stops after one animation change per run and one critic retry.

## Permissions

- Writes: loops/motion-timing-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/motion-timing-review-loop/notes.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: animation change submitted. Verification: timing rules + critic. Memory: loops/motion-timing-review-loop/notes.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
