---
name: argent-react-native-app-workflow
title: Argent React Native App Workflow skill
repo: software-mansion/argent
license: Apache-2.0
url: https://gethabit.dev/skills/software-mansion/argent-react-native-app-workflow
---

# Argent React Native App Workflow skill

The argent react native app workflow skill guides agents to start, debug, rebuild and test React Native apps on iOS simulators and Android emulators with argent tools.

- Install the skill: `npx skills add software-mansion/argent --skill argent-react-native-app-workflow`
- Source: https://github.com/software-mansion/argent/tree/HEAD/packages/skills/skills/argent-react-native-app-workflow
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You start a React Native app; Metro or the build fails; You need to run app tests.
Skip it when: You test on a physical iPhone; The project is not React Native.

# Make it a habit: The app builds and runs clean.

When code changes in a React Native project, your agent reads the saved build workflow, makes sure one Metro is ready, reloads or rebuilds the app, checks the log registry for errors and runs the tests you chose.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** app code changed (event; Claude Code routine; `push to the app branch`)
- **Verification:** Metro up, tests pass. Hard checks: debugger-status reports Metro is up; only one process listens on the Metro port; debugger-log-registry shows no JavaScript errors; the chosen unit or E2E tests pass. On fail: retry, max 2 retries.
- **Memory:** saved build workflow at `loops/react-native-run-check-loop/workflow.md`. Read first: Metro, build and run commands found before.

## Steps

1. **Read the workflow.** The agent reads the saved commands, or reads the argent-environment-inspector result and package.json scripts on the first run.
2. **Check Metro.** It checks the port with lsof and debugger-status and starts Metro only if none is running.
3. **Get a device.** It picks a device with list-devices and boots it with the argent-ios-simulator-setup or argent-android-emulator-setup steps.
4. **Reload or rebuild.** It uses debugger-reload-metro for JS changes and a rebuild for native changes.
5. **Check runtime.** It reads debugger-log-registry and uses describe or screenshot to check the screen.
6. **Confirm tests.** It asks you which test suite to run, then runs it.
7. **Ask after failures.** After two or three failed builds it stops and asks you for guidance.

Stop rule: Stops after one build and test pass per run, or after three failed build attempts.

## Permissions

- Writes: loops/react-native-run-check-loop/**
- Network: registry.npmjs.org
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/react-native-run-check-loop/workflow.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: app code changed. Verification: Metro up, tests pass. Memory: loops/react-native-run-check-loop/workflow.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
