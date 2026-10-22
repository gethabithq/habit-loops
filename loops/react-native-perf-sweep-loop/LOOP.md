---
name: argent-react-native-optimization
title: Argent React Native Optimization skill
repo: software-mansion/argent
license: Apache-2.0
url: https://gethabit.dev/skills/software-mansion/argent-react-native-optimization
---

# Argent React Native Optimization skill

The argent react native optimization skill helps React Native developers speed up apps by measuring first, then running lint, semantic and profiling sweeps with one fix per cycle.

- Install the skill: `npx skills add software-mansion/argent --skill argent-react-native-optimization`
- Source: https://github.com/software-mansion/argent/tree/HEAD/packages/skills/skills/argent-react-native-optimization
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: The app feels slow or janky; Components re-render too often; Startup takes too long.
Skip it when: You have no simulator or emulator; You only want a code style cleanup.

# Make it a habit: The app gets measurably faster.

Each week your agent runs the four-phase sweep on a React Native app: lint, semantic review, profiling with a target metric, then a regression pass. It keeps the fix only when the metric improves and logs the numbers.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly performance sweep (schedule; Claude Code routine; `0 6 * * 2`)
- **Verification:** metric improves, no regressions. Hard checks: the target metric improves against its threshold after re-measuring, otherwise the fix is reverted; debugger-log-registry shows no new runtime errors; screenshots show no red or yellow error screens; ESLint run after the sweep reports no new issues; the recorded e2e test still passes. On fail: retry, max 2 retries.
- **Memory:** metrics and fixes log at `loops/react-native-perf-sweep-loop/run-log.md`. Read first: baseline metrics and fixes kept or reverted.

## Steps

1. **Set the target.** The agent reads the log and sets a target metric with a threshold before touching code.
2. **Lint sweep.** It runs ESLint once at the root and sends one sub-agent per file to fix results.
3. **Semantic sweep.** It sends one sub-agent per checklist item, such as memoization, lists, animations and effect cleanup.
4. **Record the flow.** It records the device interaction as an e2e test with argent-create-e2e so every cycle replays the same steps.
5. **Profile.** It loads argent-react-native-profiler, runs the key flows and analyzes with react-profiler-analyze, native-profiler-analyze and profiler-combined-report.
6. **Fix one offender.** It applies one architectural fix, checks it with debugger-evaluate, then re-measures and reverts if there is no net gain.
7. **Check regressions.** It walks the screens with argent-device-interact and checks debugger-log-registry for errors.
8. **Re-lint and log.** It runs lint again and writes the metrics to the run log.

Stop rule: Stops after three profiling cycles per run, with one architectural fix per cycle.

## Permissions

- Writes: src/**, e2e/**, loops/react-native-perf-sweep-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/react-native-perf-sweep-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly performance sweep. Verification: metric improves, no regressions. Memory: loops/react-native-perf-sweep-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
