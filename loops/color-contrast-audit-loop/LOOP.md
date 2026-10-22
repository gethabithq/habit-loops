---
name: color-system
title: Color System skill
repo: owl-listener/designer-skills
license: MIT
url: https://gethabit.dev/skills/owl-listener/color-system
---

# Color System skill

The color system skill helps agents build a product color system from scratch: tonal scales, neutral and semantic palettes, usage guidance and contrast rules for AA and AAA. For designers and front-end teams defining color.

- Install the skill: `npx skills add owl-listener/designer-skills --skill color-system`
- Source: https://github.com/owl-listener/designer-skills/tree/HEAD/ui-design/skills/color-system
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: defining a product palette from scratch; adding semantic success, warning and error colors; checking color contrast.
Skip it when: you adapt an existing palette to dark mode; you need chart palettes.

# Make it a habit: Every color pair passes contrast.

When your color tokens change, your agent checks the color system: full tonal scales, semantic roles with all variants, and contrast for every foreground and background pair. It logs failing pairs so the next run checks them first.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** color tokens changed (event; GitHub Actions or Claude Code routine; `commit that edits the color token file`)
- **Verification:** contrast ratios pass. Hard checks: body text pairs reach at least 4.5:1; large text pairs reach at least 3:1; UI components reach 3:1 against neighbors; each semantic color has background, foreground, border and icon variants. On fail: notify, max 0 retries.
- **Memory:** failing pairs log at `loops/color-contrast-audit-loop/log.md`. Read first: pairs that failed before and their last ratio.

## Steps

1. **Read the palette.** Your agent loads brand, neutral, semantic and extended colors.
2. **Check tonal scales.** It confirms each hue has a full scale such as 50 to 950, not single swatches.
3. **Check semantic roles.** It confirms success, warning, error and info each have all four variants.
4. **Test every pair.** It measures contrast for each foreground and background pair against AA or AAA.
5. **Check meaning.** It flags places where color alone carries meaning and notes color-blindness checks.
6. **Log and hand off.** It logs failures and points dark mode work to the dark-mode-design skill.

Stop rule: Stops after one pass over all color pairs.

## Permissions

- Writes: loops/color-contrast-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/color-contrast-audit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: color tokens changed. Verification: contrast ratios pass. Memory: loops/color-contrast-audit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
