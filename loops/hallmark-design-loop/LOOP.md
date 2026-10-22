---
name: hallmark
title: Hallmark skill
repo: Nutlope/hallmark
license: MIT
url: https://gethabit.dev/skills/nutlope/hallmark
---

# Hallmark skill

The hallmark skill is an anti-AI-slop design skill for building, auditing, redesigning and studying web pages. It picks varied page structures and themes and checks the result against a slop test. For developers who want generated UIs that look made.

- Install the skill: `npx skills add Nutlope/hallmark --skill hallmark`
- Source: https://github.com/Nutlope/hallmark/tree/HEAD/skills/hallmark
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a new landing page or app; You want to audit or redesign a page; You want to study a design you admire.
Skip it when: The project has a fixed design you must copy exactly; You only need a quick unstyled prototype.

# Make it a habit: Pages that never look templated.

When you ask for a new page, your agent scans the project, asks audience, use case and tone, picks a macrostructure and theme unlike the last builds, builds, then runs the slop test. It records each build in .hallmark/log.json for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you request a page (manual; Claude Code session; `user asks to design, build or redesign a page`)
- **Verification:** slop test + self-critique. Hard checks: all slop-test gates in references/slop-test.md answer no; first line of the page CSS carries the Hallmark macrostructure stamp; tokens.css exists and the page CSS uses no raw colour values; no horizontal scroll at 320, 375, 414 and 768 px; macrostructure differs from the last three entries in .hallmark/log.json. Critic: claude-opus-5-5, pass at every axis 3/5 or higher. On fail: retry, max 2 retries.
- **Memory:** Hallmark build log at `.hallmark/log.json`. Read first: the last builds' macrostructure, theme and enrichment.

## Steps

1. **Pre-flight scan.** Read design.md, fonts, palette, motion libraries, spacing and framework, and cache them in .hallmark/preflight.json.
2. **Ask three things.** Ask you once for audience, use case and tone, or infer them and say so if you wave it through.
3. **Pick structure.** Read .hallmark/log.json and choose a macrostructure, nav, footer and theme that differ from recent builds.
4. **Preview.** Show the short preview block of picks before writing any code.
5. **Build.** Write the page with locked tokens, all eight states, tokens.css and the stamp, without clobbering the global stylesheet.
6. **Slop test.** Run the slop test and the six-axis self-critique, fix any failure, and update the preview.
7. **Log.** Add the build to the front of .hallmark/log.json, keeping the last 20 entries.

Stop rule: Stops after one page or component per run and at most two fix passes after the slop test.

## Permissions

- Writes: src/**, tokens.css, .hallmark/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.hallmark/log.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you request a page. Verification: slop test + self-critique. Memory: .hallmark/log.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
