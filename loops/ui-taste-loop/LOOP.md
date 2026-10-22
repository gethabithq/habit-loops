---
name: ui-taste-loop
title: UI taste loop
outcome: Keep every UI change on taste.
source: https://github.com/gethabithq/habit-loops
license: MIT
url: https://gethabit.dev/loops/ui-taste-loop
---

# UI taste loop: Keep every UI change on taste.

Every pull request that touches UI files gets built with frontend design and taste, screenshotted at three widths, and graded by a separate impeccable audit. Rejected patterns go on a board so the next run avoids them.

## Skills in this habit

Install each skill from its original repo first. Habit does not host or change them.

- Frontend Design (worker): `npx skills add anthropics/skills --skill frontend-design` · https://github.com/anthropics/skills/tree/main/skills/frontend-design · Apache-2.0
- Taste (worker): `npx skills add Leonxlnx/taste-skill --skill taste-skill` · https://github.com/Leonxlnx/taste-skill · MIT
- Impeccable (critic): `npx skills add pbakaus/impeccable --skill impeccable` · https://github.com/pbakaus/impeccable · Apache-2.0

## The three decisions

- **Trigger:** PR changes UI files (event; GitHub Actions; `paths: src/**/*.{tsx,astro,css}`)
- **Verification:** screenshots + design critic. Hard checks: screenshots at 1440, 768, 375; no console errors; build passes. Critic: claude-opus-5-5, pass at 17/20. On fail: retry, max 1 retries.
- **Memory:** design board at `design-board.md`. Read first: rejected patterns and last screenshots.

## Steps

1. **Pick up the PR.** A pull request that changes UI files starts the run.
2. **Build with taste.** frontend design and taste guide the change.
3. **Screenshot.** Three widths, console read, build checked.
4. **Critic.** impeccable audits the result in its own run. Below 17 of 20, fix once.
5. **Remember.** What got rejected goes on the design board.

Stop rule: Stops after one fix round per PR.

## Permissions

- Writes: src/**, design-board.md
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`design-board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes UI files. Verification: screenshots + design critic. Memory: design-board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`

Setup prompt: Read https://gethabit.dev/loops/ui-taste-loop.md and install this loop in my project. Show me the files first.
