---
name: gsap-performance
title: GSAP Performance skill
repo: greensock/gsap-skills
license: MIT
url: https://gethabit.dev/skills/greensock/gsap-performance
---

# GSAP Performance skill

The gsap performance skill is the official GreenSock guide for smooth GSAP animations: transforms over layout properties, careful will-change, batched reads and writes, stagger, quickTo and cleanup. For front-end developers fixing jank.

- Install the skill: `npx skills add greensock/gsap-skills --skill gsap-performance`
- Source: https://github.com/greensock/gsap-skills/tree/HEAD/skills/gsap-performance
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: GSAP animations stutter or drop frames; You animate many elements at once; You build mouse followers or scroll effects.
Skip it when: You do not use GSAP; The animation already runs smoothly on low-end devices.

# Make it a habit: Keep GSAP animations smooth.

When a pull request changes GSAP animation code, your agent reviews it against the GSAP performance rules: transforms and opacity, sparing will-change, stagger, quickTo and cleanup. A hard check flags layout tweens, and the loop keeps a list of fixed patterns.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes animation code (event; GitHub Actions or Claude Code routine; `pull_request touching files that import gsap`)
- **Verification:** layout check + review score. Hard checks: build passes; diff adds no tween that moves an element with width, height, top or left; no new tweens or timelines are created inside a per-frame or mousemove handler where gsap.quickTo() fits; ScrollTrigger.refresh() is not called on every resize without a debounce. Critic: claude-opus-5-5, pass at 17/20. On fail: notify, max 1 retries.
- **Memory:** animation findings list at `loops/gsap-performance-loop/findings.md`. Read first: patterns already fixed and files still open.

## Steps

1. **Read the diff.** Collect the GSAP tweens, timelines and ScrollTriggers the pull request adds or changes.
2. **Check properties.** Flag movement done with width, height, top or left and suggest x, y, scale or opacity instead.
3. **Check will-change.** Make sure will-change is set only on elements that really animate.
4. **Check many elements.** Suggest stagger over hand-delayed tweens, quickTo for frequent updates and reuse of timelines.
5. **Check cleanup.** Look for off-screen animations that keep running and for pins or refresh calls beyond what is needed.
6. **Report.** Post the findings, run the hard checks and add new patterns to the findings list.

Stop rule: Stops after one pull request per run and one retry of the review.

## Permissions

- Writes: loops/gsap-performance-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/gsap-performance-loop/findings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes animation code. Verification: layout check + review score. Memory: loops/gsap-performance-loop/findings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
