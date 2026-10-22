---
name: design
title: Design skill
repo: nextlevelbuilder/ui-ux-pro-max-skill
license: MIT
url: https://gethabit.dev/skills/nextlevelbuilder/design
---

# Design skill

The design skill is an all-in-one design kit for brand identity, design tokens, UI styling, logos, corporate identity mockups, HTML slides, banners, icons and social photos. For founders and marketers who need visual assets fast.

- Install the skill: `npx skills add nextlevelbuilder/ui-ux-pro-max-skill --skill design`
- Source: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill/tree/HEAD/.claude/skills/design
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need a logo or brand identity; You need social images in many sizes; You want a pitch deck or banner.
Skip it when: You need video editing; You need a full production website.

# Make it a habit: On-brand social images for each campaign.

When you start a campaign, your agent runs the design skill's social photos flow: it proposes concepts for you to pick, builds HTML per idea and size with the brand and design-system skills, exports PNGs, checks them and writes a report to plans/reports/.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new campaign brief (manual; Claude Code; `user asks for social media images`)
- **Verification:** your pick + size check. Hard checks: each exported PNG matches the platform pixel size; one PNG exists per chosen idea and size; a report file exists in plans/reports/. On fail: retry, max 2 retries.
- **Memory:** design reports folder at `plans/reports/`. Read first: past campaign reports and their design decisions.

## Steps

1. **Analyze the brief.** The agent reads subject, platforms, style, brand context and content from your prompt.
2. **Propose concepts.** It offers 3 to 5 concepts with AskUserQuestion and waits for your choice.
3. **Design per size.** It builds HTML for each idea and size using the brand, design-system and ui-ux-pro-max skills.
4. **Export PNGs.** It takes screenshots with Chrome headless, Playwright or Puppeteer at the exact pixel size.
5. **Verify and fix.** It opens each PNG, fixes layout or styling issues and exports again.
6. **Report and sort.** It writes a summary to plans/reports/ and sorts files into the asset folders.

Stop rule: Stops after one campaign, at most 5 concepts, and 2 export retries per image.

## Permissions

- Writes: plans/reports/**, assets/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`plans/reports/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new campaign brief. Verification: your pick + size check. Memory: plans/reports/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
