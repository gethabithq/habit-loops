---
name: web-typography
title: Web Typography skill
repo: wondelai/skills
license: MIT
url: https://gethabit.dev/skills/wondelai/web-typography
---

# Web Typography skill

The web typography skill helps an agent choose, pair and set typefaces for the web, from line length and line height to fluid sizes and font loading. For designers and developers who want readable, fast text.

- Install the skill: `npx skills add wondelai/skills --skill web-typography`
- Source: https://github.com/wondelai/skills/tree/HEAD/plugins/ux-design/skills/web-typography
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You pick or pair typefaces; Text feels hard to read; Web fonts load slowly.
Skip it when: You need a full design system; The product has no web text.

# Make it a habit: Type stays readable on every release.

When CSS or font files change, your agent scores the typography with the web-typography Quick Diagnostic: body size, measure, line height, hierarchy, font payload, fallbacks and zoom. It logs the score and failing rows for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** CSS or fonts change (event; GitHub Actions or Claude Code routine; `pull_request with changed css or woff2 files`)
- **Verification:** diagnostic score check. Hard checks: body text is 16px or larger; prose containers cap the measure under 75 characters; total font payload under 200KB; every font-family has a fallback. On fail: notify, max 0 retries.
- **Memory:** typography score log at `loops/web-typography-check-loop/runs.md`. Read first: the last score and the diagnostic rows that failed.

## Steps

1. **Read the log.** The agent reads the last score and which rows failed.
2. **Inspect the CSS.** It reads the changed styles and font loading rules.
3. **Run the diagnostic.** It answers the ten Quick Diagnostic rows for body, headings and links.
4. **Check loading.** It checks font-display swap, preload, WOFF2 and subsetting.
5. **Score and log.** It states the score out of 10, the failing rows and the fixes in the log.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/web-typography-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/web-typography-check-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: CSS or fonts change. Verification: diagnostic score check. Memory: loops/web-typography-check-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
