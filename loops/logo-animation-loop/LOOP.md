---
name: logo-animation
title: Logo Animation skill
repo: iart-ai/motion-design-skills
license: MIT
url: https://gethabit.dev/skills/iart-ai/logo-animation
---

# Logo Animation skill

The logo animation skill helps designers and developers animate a brand mark for web, video or app splash with one clear technique, a reduced-motion path and a static fallback frame.

- Install the skill: `npx skills add iart-ai/motion-design-skills --skill logo-animation`
- Source: https://github.com/iart-ai/motion-design-skills/tree/HEAD/skills/logo-animation
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need a logo intro or splash; You want an SVG draw-on reveal; You sync a mark to a sound-logo.
Skip it when: You need a full brand identity; The logo itself is not designed yet.

# Make it a habit: Every logo reveal ships clean.

When a logo brief comes in, your agent builds one standalone HTML reveal with a single technique, freezes it at start, mid and end with ?t=N, screenshots each frame and fixes it until all frames are clean. A run log keeps what was tried.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new logo brief (manual; Claude Code routine; `run when a logo animation is requested`)
- **Verification:** frozen frame screenshots. Hard checks: file opens with no console errors; screenshots exist for start, mid and end; reveal is 2.5s or shorter; prefers-reduced-motion shows the static mark; static end-frame fallback file exists. On fail: retry, max 2 retries.
- **Memory:** reveal run log at `loops/logo-animation-loop/run-log.md`. Read first: technique, timing and fixes from past reveals.

## Steps

1. **Pick one technique.** Choose draw, build or morph for the mark, never all three.
2. **Build the file.** Write one .html file with the inline SVG or Lottie canvas, one driver and the freeze harness.
3. **Freeze and shoot.** Open the file at ?t=0, mid and end and screenshot each frame with npx playwright screenshot.
4. **Check the frames.** Confirm geometry is intact, clearspace is clear and the end frame is the true logo.
5. **Fix and repeat.** Adjust stroke-dashoffset, duration or easing and reshoot the same ?t=N until clean.
6. **Ship fallbacks.** Add the prefers-reduced-motion path and a static end-frame SVG or PNG.

Stop rule: Stops after one logo per run, with at most 2 fix rounds.

## Permissions

- Writes: logo.html, frame-*.png, loops/logo-animation-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/logo-animation-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new logo brief. Verification: frozen frame screenshots. Memory: loops/logo-animation-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
