---
name: color-motion
title: Color in Motion skill
repo: iart-ai/motion-design-skills
license: MIT
url: https://gethabit.dev/skills/iart-ai/color-motion
---

# Color in Motion skill

The color in motion skill helps motion designers build restrained palettes, premium gradients and smooth OKLCH color transitions, and fix washed-out or gamma-shifted video renders.

- Install the skill: `npx skills add iart-ai/motion-design-skills --skill color-motion`
- Source: https://github.com/iart-ai/motion-design-skills/tree/HEAD/skills/color-motion
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a gradient background; Your gradient midpoint looks gray; Your render looks washed out.
Skip it when: You need a full brand system; Your work is print only.

# Make it a habit: Gradients without muddy midpoints.

When a palette or gradient task comes in, your agent builds one standalone HTML file that interpolates in OKLCH, freezes it at start, mid and end, screenshots each frame and fixes banding or gray midpoints. A run log keeps the palettes that passed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new color brief (manual; Claude Code routine; `run when a palette, gradient or color transition is requested`)
- **Verification:** frozen frames stay vivid. Hard checks: file opens with no console errors; screenshots exist for start, mid and end; interpolation uses OKLCH or Lab, not raw sRGB; prefers-reduced-motion pauses the drift. On fail: retry, max 2 retries.
- **Memory:** palette run log at `loops/color-motion-loop/run-log.md`. Read first: palettes and fixes from earlier runs.

## Steps

1. **Build the palette.** Pick one primary, one accent and two or three neutrals with exact OKLCH values.
2. **Write the file.** Put the gradient or @property transition and the freeze harness in one .html file.
3. **Freeze and shoot.** Open it at ?t=0, mid and end and screenshot each frame with npx playwright screenshot.
4. **Check the frames.** Look for banding and gray or muddy midpoints at every frozen frame.
5. **Fix and repeat.** Adjust chroma and lightness or add grain, then reshoot the same ?t=N.

Stop rule: Stops after one palette or gradient per run, with at most 2 fix rounds.

## Permissions

- Writes: color.html, frame-*.png, loops/color-motion-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/color-motion-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new color brief. Verification: frozen frames stay vivid. Memory: loops/color-motion-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
