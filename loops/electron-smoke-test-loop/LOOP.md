---
name: electron
title: Electron skill
repo: vercel-labs/agent-browser
license: Apache-2.0
url: https://gethabit.dev/skills/vercel-labs/electron
---

# Electron skill

The electron skill automates Electron desktop apps such as VS Code, Slack, Discord and Figma with agent-browser over the Chrome DevTools Protocol: launch with a debugging port, connect, snapshot and interact. For developers testing desktop apps.

- Install the skill: `npx skills add vercel-labs/agent-browser --skill electron`
- Source: https://github.com/vercel-labs/agent-browser/tree/HEAD/skill-data/electron
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You automate or test an Electron app; You drive a desktop app's UI from the command line; You snapshot a native app's screen.
Skip it when: The app is not built on Electron; You only test a plain web page.

# Make it a habit: Desktop app checked after each build.

When a new Electron build is ready, your agent launches it with remote debugging, connects agent-browser over the DevTools port, snapshots the UI, walks a short flow, and saves a screenshot. A log keeps the ports and flows for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new Electron build (event; Claude Code routine; `build artifact ready`)
- **Verification:** connect and snapshot work. Hard checks: agent-browser connect to the debugging port succeeds; the snapshot lists interactive elements; the screenshot file is written. On fail: retry, max 1 retries.
- **Memory:** ports and flows log at `loops/electron-smoke-test-loop/run-log.md`. Read first: the debugging port and the flow steps from the last run.

## Steps

1. **Read the log.** The agent reads the debugging port and the flow steps from the last run.
2. **Launch with CDP.** It quits any running copy and relaunches the app with --remote-debugging-port.
3. **Connect.** It waits a few seconds, then runs agent-browser connect to the port.
4. **Snapshot.** It runs agent-browser snapshot -i and lists targets with agent-browser tab if there are webviews.
5. **Walk the flow.** It clicks, fills and presses through the short flow by element refs, re-snapshotting after each change.
6. **Capture and log.** It saves a screenshot and records the port and flow in the run log.

Stop rule: Stops after one app flow per run and at most 1 retry of a failed connect.

## Permissions

- Writes: *.png, loops/electron-smoke-test-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/electron-smoke-test-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new Electron build. Verification: connect and snapshot work. Memory: loops/electron-smoke-test-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
