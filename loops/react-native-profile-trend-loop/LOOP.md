---
name: argent-react-native-profiler
title: Argent React Native Profiler skill
repo: software-mansion/argent
license: Apache-2.0
url: https://gethabit.dev/skills/software-mansion/argent-react-native-profiler
---

# Argent React Native Profiler skill

The argent react native profiler skill helps React Native developers measure re-renders and CPU hotspots on Hermes apps, produce ranked reports and compare before and after a fix.

- Install the skill: `npx skills add software-mansion/argent --skill argent-react-native-profiler`
- Source: https://github.com/software-mansion/argent/tree/HEAD/packages/skills/skills/argent-react-native-profiler
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You measure before and after a fix; Components re-render too often; You need a ranked performance report.
Skip it when: You only have a physical iPhone; You want lint-style fixes only.

# Make it a habit: Render regressions show up early.

Each week your agent replays the same recorded e2e flow under the React and native profilers, compares the report with last week's saved session, and asks you whether to dig deeper, fix or stop.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly profiling run (schedule; Claude Code routine; `0 6 * * 3`)
- **Verification:** data captured + you decide. Hard checks: fiber_renders_captured is above zero; profiler-combined-report runs when both profilers ran; the same device_id is used for every profiler and query call; the target metric is compared with the previous session loaded by profiler-load. On fail: notify, max 1 retries.
- **Memory:** session and metric log at `loops/react-native-profile-trend-loop/run-log.md`. Read first: last session id, target metric and its value.

## Steps

1. **Set the metric.** The agent reads the log for the target metric and threshold, such as totalRenderMs.
2. **Start profilers.** It starts react-profiler-start and native-profiler-start in parallel with the same device_id.
3. **Replay the flow.** It replays the e2e test from argent-create-e2e with e2e-execute and annotates each interaction.
4. **Stop and analyze.** It stops both profilers, runs react-profiler-analyze and native-profiler-analyze, then profiler-combined-report.
5. **Compare.** It reloads last week's session with profiler-load and compares the metric honestly.
6. **Ask next step.** It shows the findings and asks you whether to investigate, fix or stop.

Stop rule: Stops after one profiling scenario per run and your answer on next steps.

## Permissions

- Writes: loops/react-native-profile-trend-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/react-native-profile-trend-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly profiling run. Verification: data captured + you decide. Memory: loops/react-native-profile-trend-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
