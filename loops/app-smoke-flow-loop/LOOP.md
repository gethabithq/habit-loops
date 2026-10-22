---
name: agent-device
title: agent-device skill
repo: callstack/agent-device
license: MIT
url: https://gethabit.dev/skills/callstack/agent-device
---

# agent-device skill

The agent-device skill lets your agent drive apps on iOS, tvOS, macOS, Android and Vega OS TV: tap, type, scroll, read the UI and check what is on screen. For mobile and TV app developers who want agents to test real flows.

- Install the skill: `npx skills add callstack/agent-device --skill agent-device`
- Source: https://github.com/callstack/agent-device/tree/HEAD/skills/agent-device
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You test an app flow on a device; You need screenshots or UI info; You drive a TV app remote.
Skip it when: Web pages in a browser; Pure unit tests without a device.

# Make it a habit: Every build passes a real tap-through.

After each new app build, your agent opens the app on a device with agent-device, taps through one key flow and checks the expected text appears. It closes the session and logs which flows passed for the next build.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new app build ready (event; GitHub Actions or Claude Code routine; `build finished on main`)
- **Verification:** expected text on screen. Hard checks: agent-device open returns a snapshot with refs; wait text finds the expected text; is or get confirms the named expectation; agent-device close ends the session. On fail: retry, max 1 retries.
- **Memory:** flow results per build at `loops/app-smoke-flow-loop/run-log.md`. Read first: flows that failed on the last build.

## Steps

1. **Open the app.** Your agent runs agent-device open with --foreground and gets the first snapshot with refs.
2. **Drive the flow.** It uses press, fill or scroll with --settle and follows the printed diff.
3. **Reach far targets.** For items off screen it uses scroll down --until with a selector.
4. **Check the result.** It confirms the expected screen with wait text, is, get or find.
5. **Close and log.** It runs agent-device close and writes pass or fail for the flow.

Stop rule: Stops after 3 flows per build or 1 retry per failed flow.

## Permissions

- Writes: loops/app-smoke-flow-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/app-smoke-flow-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new app build ready. Verification: expected text on screen. Memory: loops/app-smoke-flow-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
