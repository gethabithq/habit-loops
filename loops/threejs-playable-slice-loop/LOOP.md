---
name: threejs-gameplay-systems
title: Three.js Gameplay Systems skill
repo: majidmanzarpour/threejs-game-skills
license: MIT
url: https://gethabit.dev/skills/majidmanzarpour/threejs-gameplay-systems
---

# Three.js Gameplay Systems skill

The three.js gameplay systems skill builds playable browser game loops: a Vite and TypeScript starter, design briefs, core loops, levels, input, camera, physics, scoring and game feel. For developers making games with Three.js.

- Install the skill: `npx skills add majidmanzarpour/threejs-game-skills --skill threejs-gameplay-systems`
- Source: https://github.com/majidmanzarpour/threejs-game-skills/tree/HEAD/skills/threejs-gameplay-systems
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: starting a first playable Three.js game; designing levels or encounters; tuning game feel and difficulty.
Skip it when: you only need a static 3D scene; the game uses another engine.

# Make it a habit: A game loop you can play.

When you build or change a Three.js game, your agent writes or updates the design brief, core loop contract and level plan, then builds in playable increments with seeded randomness and runs the game's visual test. The design artifacts are the memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you build a mechanic (manual; Claude Code routine; `run threejs-gameplay-systems on demand`)
- **Verification:** playable and tested. Hard checks: the scaffold's visual test passes; the primary verb is mapped to real input; gameplay randomness goes through the seeded RNG; the build compiles. On fail: retry, max 2 retries.
- **Memory:** design brief and plans at `loops/threejs-playable-slice-loop/design.md`. Read first: the design brief, core loop contract and level plan.

## Steps

1. **Scaffold.** For a new game your agent runs create_threejs_game.py to copy the Vite and TypeScript starter.
2. **Design first.** It writes or updates the design brief, core loop contract and level or encounter plan.
3. **Inspect.** It reviews the existing loop, input, camera, entities, state and UI before changing anything.
4. **Build increments.** It adds input, state, entities, collision, feedback and HUD hooks so the game stays playable at each step.
5. **Tune feel.** It tunes movement, camera, impact feedback and difficulty using references/game-feel.md.
6. **Report.** It reports behavior, controls, tuned values, changed files and what it saw when playing.

Stop rule: Stops after one mechanic or encounter per run, with at most 2 fix retries.

## Permissions

- Writes: game project source files, loops/threejs-playable-slice-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/threejs-playable-slice-loop/design.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you build a mechanic. Verification: playable and tested. Memory: loops/threejs-playable-slice-loop/design.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
