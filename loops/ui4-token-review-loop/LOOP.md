---
name: ui4-review
title: UI4 Review skill
repo: payloadcms/payload
license: MIT
url: https://gethabit.dev/skills/payloadcms/ui4-review
---

# UI4 Review skill

The ui4 review skill helps Payload UI developers review and auto-fix UI4 CSS migrations so components use spacing, radius, elevation and semantic color tokens instead of hardcoded values.

- Install the skill: `npx skills add payloadcms/payload --skill ui4-review`
- Source: https://github.com/payloadcms/payload/tree/HEAD/.agents/skills/ui4-review
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You migrate CSS to UI4 tokens; You review CSS changes in Payload UI; Hardcoded colors slip into components.
Skip it when: You do not work on Payload UI; You use a different token system.

# Make it a habit: CSS uses tokens, not hardcoded values.

When CSS files change, your agent runs six greps for SCSS nesting, hardcoded spacing and colors, legacy variables, old token names and raw palette use, auto-fixes in priority order, flags unclear cases and reports a per-file summary.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** CSS files changed (event; Claude Code routine or GitHub Actions; `git status shows changed .css files, or pull_request touches .css`)
- **Verification:** violation greps come back clean. Hard checks: no &__ or &-- nesting left; no var(--theme-, var(--style- or var(--base) left; no var(--ramp- outside colors.css; every remaining hardcoded value is listed as flagged. On fail: notify, max 1 retries.
- **Memory:** flagged values log at `loops/ui4-token-review-loop/run-log.md`. Read first: values flagged for manual review earlier.

## Steps

1. **Get changed files.** Run git status --porcelain filtered to .css files.
2. **Detect violations.** Run the six grep checks in one parallel batch.
3. **Auto-fix by priority.** Fix nesting, legacy variables, old names, raw palette, then hardcoded values.
4. **Flag the rest.** Flag values with no matching token instead of guessing.
5. **Report.** List auto-fixed and flagged lines and a per-file summary table.

Stop rule: Stops after the changed CSS files of one change set.

## Permissions

- Writes: **/*.css, loops/ui4-token-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ui4-token-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: CSS files changed. Verification: violation greps come back clean. Memory: loops/ui4-token-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
