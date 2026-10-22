---
name: antislop-layoutmobile
title: Antislop Layout Mobile skill
repo: miqdadbadjuber/anti-slop
license: MIT
url: https://gethabit.dev/skills/miqdadbadjuber/antislop-layoutmobile
---

# Antislop Layout Mobile skill

Antislop Layout Mobile is the responsive layout part of antislop: breakpoints where content breaks, mobile scale, collapsing grids, no overflow, 44px tap targets and mobile navigation, with a checklist. For developers building responsive UI.

- Install the skill: `npx skills add miqdadbadjuber/anti-slop --skill antislop-layoutmobile`
- Source: https://github.com/miqdadbadjuber/anti-slop/tree/HEAD/skills/antislop-layoutmobile
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a responsive layout; A page scrolls sideways on phones; You check tap targets and mobile nav.
Skip it when: The UI is desktop only by design; You do not use the antislop core.

# Make it a habit: Layouts that reflow at every width.

When layout code changes, your agent loads the antislop core and this mobile skill, drags the viewport across the full width range, checks breakpoints, scale, grids, overflow, tap targets and mobile navigation, fixes failures and runs the Layoutmobile Skill Checklist.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** layout code changes (event; Claude Code routine; `pull request touches layout CSS or page components`)
- **Verification:** mobile checklist passes. Hard checks: zero horizontal scroll at the narrowest target width; interactive targets are at least 44 x 44 px; every Layoutmobile Skill Checklist item answers yes. On fail: retry, max 2 retries.
- **Memory:** numbered audit reports at `anti-slop/audit-001-YYYY-MM-DD.md`. Read first: the last audit and widths that failed before.

## Steps

1. **Load both files.** Your agent reads antislop.md and this mobile layout skill together.
2. **Check breakpoints.** It checks states sit where content breaks, with a real middle state, not just two.
3. **Check scale.** It checks type, padding, gaps and section heights have a mobile scale.
4. **Check grids and overflow.** It checks grids collapse, nothing scrolls sideways and nothing is clipped.
5. **Check touch.** It checks tap target size and spacing and gives hover-only actions a tap equivalent.
6. **Check navigation.** It checks the nav reflows and fixed bars never cover content.

Stop rule: Stops after one change and 2 fix rounds per run.

## Permissions

- Writes: src/**, anti-slop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`anti-slop/audit-001-YYYY-MM-DD.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: layout code changes. Verification: mobile checklist passes. Memory: anti-slop/audit-001-YYYY-MM-DD.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
