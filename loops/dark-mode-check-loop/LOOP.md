---
name: dark-mode-design
title: Dark Mode Design skill
repo: owl-listener/designer-skills
license: MIT
url: https://gethabit.dev/skills/owl-listener/dark-mode-design
---

# Dark Mode Design skill

The dark mode design skill helps agents adapt an existing light palette to dark mode: surface elevation, desaturated colors, off-white text, contrast rebalancing and media handling. For designers and front-end teams adding a dark theme.

- Install the skill: `npx skills add owl-listener/designer-skills --skill dark-mode-design`
- Source: https://github.com/owl-listener/designer-skills/tree/HEAD/ui-design/skills/dark-mode-design
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: adding dark mode to an app; fixing low contrast in a dark theme; planning dark surface levels.
Skip it when: you have no base palette yet; you need chart colors.

# Make it a habit: Dark mode stays readable everywhere.

When light theme colors or components change, your agent checks the dark mode version: surface elevation steps, desaturated primaries, off-white text, 4.5:1 body contrast and prefers-color-scheme support. It logs components that still fail.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** light theme changed (event; GitHub Actions or Claude Code routine; `commit that edits light theme colors or components`)
- **Verification:** dark contrast and surfaces. Hard checks: body text in dark mode reaches 4.5:1; surfaces get lighter with elevation; text uses off-white, not pure white; prefers-color-scheme is respected and a manual toggle exists. On fail: notify, max 0 retries.
- **Memory:** dark mode log at `loops/dark-mode-check-loop/log.md`. Read first: components that failed in dark mode before.

## Steps

1. **Map the surfaces.** Your agent checks background and three elevated surface levels from darkest to lightest.
2. **Adapt the colors.** It checks primaries are desaturated and error and warning colors are adjusted for dark backgrounds.
3. **Check text and borders.** It confirms off-white text and subtle low-opacity borders.
4. **Check media.** It looks for dimmed images, dark illustration variants and light-on-dark logos.
5. **Check accessibility.** It measures contrast and confirms the media query and manual toggle work.
6. **Log the results.** It records failing components and uses the color-system skill when the base palette is missing.

Stop rule: Stops after one pass over the changed components.

## Permissions

- Writes: loops/dark-mode-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/dark-mode-check-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: light theme changed. Verification: dark contrast and surfaces. Memory: loops/dark-mode-check-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
