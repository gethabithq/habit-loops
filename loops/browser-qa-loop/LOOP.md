---
name: agent-browser
title: agent-browser skill
repo: vercel-labs/agent-browser
license: Apache-2.0
url: https://gethabit.dev/skills/vercel-labs/agent-browser
---

# agent-browser skill

The agent-browser skill by vercel-labs points agents to a fast Rust CLI that drives Chrome via CDP, with accessibility snapshots and element refs, for web tasks, QA, Electron apps and Slack.

- Install the skill: `npx skills add vercel-labs/agent-browser --skill agent-browser`
- Source: https://github.com/vercel-labs/agent-browser/tree/HEAD/skills/agent-browser
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You test a web app; You fill forms or scrape pages; You automate an Electron app.
Skip it when: You only need to fetch a static page; You cannot install a CLI.

# Make it a habit: Your web app tested every night.

Each night your agent loads the current agent-browser guide with skills get core and the dogfood skill, then explores your web app in Chrome, takes screenshots and notes bugs. A board keeps open findings so the next run checks them first.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** nightly app check (schedule; Claude Code routine; `0 2 * * *`)
- **Verification:** guide loaded, screenshots saved. Hard checks: agent-browser skills get core exits without error; at least one screenshot file exists for this run; the board has an entry for this run. On fail: notify, max 1 retries.
- **Memory:** open QA findings at `loops/browser-qa-loop/board.md`. Read first: bugs found on earlier nights that are still open.

## Steps

1. **Load the guide.** Your agent runs agent-browser skills get core to get the workflow for the installed version.
2. **Load QA skill.** It runs agent-browser skills get dogfood for exploratory testing and bug hunts.
3. **Recheck old bugs.** It opens the pages behind open findings on the board first.
4. **Explore the app.** It navigates pages, fills forms, clicks buttons and takes screenshots.
5. **Log findings.** It adds new bugs with screenshots to the board and closes fixed ones.

Stop rule: Stops after 20 pages or 10 findings per run, whichever comes first.

## Permissions

- Writes: loops/browser-qa-loop/**
- Network: your app's host
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/browser-qa-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: nightly app check. Verification: guide loaded, screenshots saved. Memory: loops/browser-qa-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
