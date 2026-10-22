---
name: app-store-screenshots
title: App Store Screenshots skill
repo: ParthJadhav/app-store-screenshots
license: MIT
url: https://gethabit.dev/skills/parthjadhav/app-store-screenshots
---

# App Store Screenshots skill

The app store screenshots skill scaffolds a Next.js editor to design and bulk-export marketing screenshots for the App Store, Mac App Store and Google Play. For app makers who want screenshots that work as ads.

- Install the skill: `npx skills add ParthJadhav/app-store-screenshots --skill app-store-screenshots`
- Source: https://github.com/ParthJadhav/app-store-screenshots/tree/HEAD/skills/app-store-screenshots
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need App Store or Play screenshots; You want localized screenshot sets; You refresh screenshots for a release.
Skip it when: You have no app captures yet; You only need one plain screenshot.

# Make it a habit: Store screenshots that sell features.

When new app captures land in public/screenshots, your agent runs app store screenshots: it updates the Next.js editor deck, coaches the copy, you design and export, and a QA gate checks build, layouts and file names. The deck lives in app-store-screenshots.json.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new app captures added (event; GitHub Actions or Claude Code routine; `push that changes public/screenshots/**`)
- **Verification:** you export + QA gate. Hard checks: the build passes; app-store-screenshots.json has a schemaVersion and a boolean connectedCanvas; every referenced screenshot file exists for each configured locale; no two adjacent slides share the same layout; exported file names sort with zero-padded prefixes. On fail: notify, max 1 retries.
- **Memory:** deck project file at `app-store-screenshots.json`. Read first: existing decks, locales, theme and screenshot paths.

## Steps

1. **Probe the project.** The agent checks package.json and app-store-screenshots.json for an older or current editor setup.
2. **Ask about migration.** If an older project is found, you choose whether to move it to the connected-canvas editor.
3. **Gather input.** You confirm captures, app icon, name, feature order, style and locales before any scaffolding.
4. **Scaffold or update.** The template is copied, dependencies installed and your captures placed under public/screenshots.
5. **Coach the copy.** The agent reads copy-ideas.md and offers three headline options per slide, one idea each.
6. **Design and export.** You open the editor from the dev server, adjust slides and hit Export bundle per device.
7. **Run the QA gate.** The final checklist covers message, layout rhythm, export sizes, clipping and file names.

Stop rule: Stops after one device deck per run, with at most one retry of the build.

## Permissions

- Writes: app-store-screenshots.json, public/**, src/**, package.json, /tmp/app-store-screenshots-migration-*
- Network: localhost:3000
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`app-store-screenshots.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new app captures added. Verification: you export + QA gate. Memory: app-store-screenshots.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
