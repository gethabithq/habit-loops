---
name: hyperframes-cli
title: HyperFrames CLI skill
repo: heygen-com/hyperframes
license: Apache-2.0
url: https://gethabit.dev/skills/heygen-com/hyperframes-cli
---

# HyperFrames CLI skill

The hyperframes cli skill by heygen-com maps every HyperFrames command by job: scaffold, check, snapshot, edit the timeline, preview, render and publish, plus how to recover from failures. For agents that make videos in code.

- Install the skill: `npx skills add heygen-com/hyperframes --skill hyperframes-cli`
- Source: https://github.com/heygen-com/hyperframes/tree/HEAD/skills/hyperframes-cli
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You build a HyperFrames video; You need to edit a timeline; A render or check fails.
Skip it when: You edit video in a desktop editor; You have no Node.js or FFmpeg.

# Make it a habit: Checked videos, rendered on your OK.

Every hour on work days your agent checks the HyperFrames project history for your edits. If there are any, it lints the project, snapshots frames, previews it and renders after your OK. It verifies the file and its duration with ffprobe.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** hourly on work days (schedule; cron or Claude Code routine; `0 9-18 * * 1-5`)
- **Verification:** check gate + your OK. Hard checks: npx hyperframes check --json shows no errors; preview URL answers 200; rendered file is non-empty; ffprobe duration matches the root data-duration. On fail: retry, max 2 retries.
- **Memory:** HyperFrames project history at `.hyperframes/`. Read first: history --since mine, to see what the person changed since the last turn.

## Steps

1. **Open the turn.** Your agent runs history begin with a label, then history --since mine. With no edits from you, it ends the turn.
2. **Write and lint.** It builds on your edits and runs npx hyperframes lint after the first pass and big changes.
3. **Gate with check.** It runs check --json and fixes every error, including contrast and layout findings.
4. **Look at frames.** It runs snapshot and reads the PNGs, with a midpoint of every scene.
5. **Preview and wait.** It starts preview --background, confirms a 200 answer and waits for your OK.
6. **Render and verify.** It renders out.mp4, then checks the file is non-empty and the ffprobe duration matches data-duration.
7. **Close the turn.** It sends one feedback rating unless telemetry is off, and ends with history end.

Stop rule: Stops after one render per run and at most 2 fix rounds on check errors.

## Permissions

- Writes: <dir>/** (the project created with init <dir>), <dir>/.hyperframes/**, <dir>/out.mp4
- Network: npx download of the hyperframes package, local preview server
- Sends: npx hyperframes feedback --rating (unless telemetry is off)
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.hyperframes/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: hourly on work days. Verification: check gate + your OK. Memory: .hyperframes/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
