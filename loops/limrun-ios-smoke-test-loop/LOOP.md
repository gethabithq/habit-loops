---
name: limrun-ios-simulator
title: Limrun iOS Simulator skill
repo: limrun-inc/skills
license: MIT
url: https://gethabit.dev/skills/limrun-inc/limrun-ios-simulator
---

# Limrun iOS Simulator skill

The limrun ios simulator skill drives an app on a Limrun cloud iOS simulator: tap, type, element tree, logs, screenshots, video, tunnels, proxy, camera and Face ID. For iOS developers who test without a local Mac.

- Install the skill: `npx skills add limrun-inc/skills --skill limrun-ios-simulator`
- Source: https://github.com/limrun-inc/skills/tree/HEAD/skills/limrun-ios-simulator
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want to see or test a built app; You need screenshots or a demo video; The app must reach a local server.
Skip it when: You still need to build the app; You test on a local simulator.

# Make it a habit: Each build gets a smoke test.

After each successful iOS build, your agent attaches a Limrun simulator, reads the element tree, taps through what changed plus core flows, and records a demo video for UI changes. Results and the instance ID go to a run log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** iOS build succeeds (event; Claude Code routine or GitHub Actions; `lim xcode build succeeded`)
- **Verification:** element tree confirms flow. Hard checks: lim ios element-tree shows the expected screen after each tap; launch-app reports no crash exit; recording file exists for UI changes. On fail: notify, max 1 retries.
- **Memory:** smoke test log at `loops/limrun-ios-smoke-test-loop/runs.md`. Read first: core flows to test and last instance ID.

## Steps

1. **Find the instance.** Run lim xcode get or lim ios list, or lim ios create --attach.
2. **Share the stream.** Give the signed stream URL as a link.
3. **Read the screen.** Run lim ios element-tree with --id before acting.
4. **Drive the change.** Tap by accessibility id, then label, then coordinates, and type into focused fields.
5. **Confirm each step.** Re-run element-tree after every interaction.
6. **Capture evidence.** Take screenshots for visuals and use lim ios record for motion.
7. **Clean up.** Run lim ios delete when the work is done.

Stop rule: Stops after the changed flow and one core-flow pass per build.

## Permissions

- Writes: loops/limrun-ios-smoke-test-loop/**
- Network: console.limrun.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/limrun-ios-smoke-test-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: iOS build succeeds. Verification: element tree confirms flow. Memory: loops/limrun-ios-smoke-test-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
