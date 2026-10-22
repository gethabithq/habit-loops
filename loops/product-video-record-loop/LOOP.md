---
name: screenci
title: ScreenCI skill
repo: screenci/screenci
license: MIT
url: https://gethabit.dev/skills/screenci/screenci
---

# ScreenCI skill

ScreenCI is a skill for product teams that creates narrated product videos and stills in a ScreenCI project by editing .screenci.ts recordings, testing them and recording a live preview.

- Install the skill: `npx skills add screenci/screenci --skill screenci`
- Source: https://github.com/screenci/screenci/tree/HEAD/skills/screenci
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need a product demo video; Your UI changed and videos are stale; You want narrated how-to videos.
Skip it when: You only change app source; You have no ScreenCI project.

# Make it a habit: Narrated product videos kept current.

Your agent explores the target page, writes a narrated .screenci.ts recording with mock data and kit overlays, debugs it with npx screenci test, then records a live preview and reports the link in plain language. Real-world forms on production stay unsent.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** product UI changes (event; Claude Code; `event: app change needs an updated recording`)
- **Verification:** test run passes, preview recorded. Hard checks: npx screenci test passes for the recording; npx screenci preview prints a link; no submit on production order, payment, send or delete forms; every video has narration. On fail: retry, max 2 retries.
- **Memory:** recording files at `recordings/*.screenci.ts`. Read first: existing recordings and npx screenci context.

## Steps

1. **Read context.** Run npx screenci context for site, sign-in and team notes.
2. **Explore the page.** Use npx screenci explore with --click or the playwright-cli skill.
3. **Write the recording.** Edit recordings/*.screenci.ts with narration, hide() blocks and kit overlays.
4. **Debug.** Run npx screenci test with --grep, and set channel chrome on browser failures.
5. **Record preview.** Run npx screenci preview with the title and keep the link.
6. **Report.** Tell the person what the video shows and end with the link.

Stop rule: Stops after one video and 2 failed test runs.

## Permissions

- Writes: recordings/**, screenci.config.ts
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`recordings/*.screenci.ts`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: product UI changes. Verification: test run passes, preview recorded. Memory: recordings/*.screenci.ts. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
