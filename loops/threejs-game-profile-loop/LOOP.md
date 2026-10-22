---
name: threejs-debug-profiler
title: Three.js Debug Profiler skill
repo: majidmanzarpour/threejs-game-skills
license: MIT
url: https://gethabit.dev/skills/majidmanzarpour/threejs-debug-profiler
---

# Three.js Debug Profiler skill

Three.js Debug Profiler debugs and profiles Three.js browser games: blank canvases, runtime and loading bugs, input issues, and draw call, texture, memory and shader costs. For game developers finding root causes and bottlenecks.

- Install the skill: `npx skills add majidmanzarpour/threejs-game-skills --skill threejs-debug-profiler`
- Source: https://github.com/majidmanzarpour/threejs-game-skills/tree/HEAD/skills/threejs-debug-profiler
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: a Three.js canvas is blank; a browser game drops frames; assets or audio fail to load.
Skip it when: the project does not use Three.js; you only need new features.

# Make it a habit: Root causes fixed, bottlenecks measured.

When a Three.js game breaks or slows, your agent reproduces with your command and URL, fixes the root cause in the owning module, or baselines one scenario, changes one thing and re-measures. A run log keeps baseline and post metrics.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** bug or slowdown reported (event; Claude Code routine; `blank canvas, runtime bug or frame drop reported`)
- **Verification:** broken path retested. Hard checks: the exact broken path is retested after the fix; baseline and post metrics are recorded for the same scenario; no new console or network errors appear. On fail: retry, max 2 retries.
- **Memory:** profile metrics log at `loops/threejs-game-profile-loop/run-log.md`. Read first: earlier baselines, bottlenecks and fixes.

## Steps

1. **Reproduce.** Your agent reproduces with the same command and URL and reads console, page and network errors.
2. **Find the owner.** It finds the module that owns the failure, such as renderer, loop, assets or input.
3. **Fix the root.** It fixes the root cause there using the debug-playbook triage order.
4. **Baseline.** For speed issues it profiles one fixed scenario and classifies the bottleneck.
5. **Change one thing.** It changes one thing and re-measures the same scenario, checking visuals and playability.
6. **Report.** It leads with the root cause or bottleneck, then files, metrics, commands and residual risks.

Stop rule: Stops after one bug or one bottleneck per run, with at most 2 retest retries.

## Permissions

- Writes: game source files, loops/threejs-game-profile-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/threejs-game-profile-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: bug or slowdown reported. Verification: broken path retested. Memory: loops/threejs-game-profile-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
