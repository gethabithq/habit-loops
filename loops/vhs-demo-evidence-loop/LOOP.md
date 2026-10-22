---
name: vhs-demo
title: VHS Demo skill
repo: cli/cli
license: MIT
url: https://gethabit.dev/skills/cli/vhs-demo
---

# VHS Demo skill

The vhs demo skill helps CLI developers record short, repeatable terminal GIFs with VHS as before/after evidence for reviewers, with isolated config and frame-by-frame inspection.

- Install the skill: `npx skills add cli/cli --skill vhs-demo`
- Source: https://github.com/cli/cli/tree/HEAD/.github/skills/vhs-demo
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need a terminal GIF for a PR; You show before and after CLI output; You author a VHS tape.
Skip it when: VHS, ffmpeg or ttyd cannot run; You need proof of general correctness.

# Make it a habit: Before and after GIFs reviewers trust.

When a pull request changes CLI output, your agent runs the VHS preflight, builds baseline and changed binaries, records an isolated tape for each, inspects every frame with the helper and returns paths, versions and hashes as evidence.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** CLI output changes (event; Claude Code routine; `pull_request labelled for demo evidence`)
- **Verification:** preflight and inspection pass. Hard checks: preflight.sh passes with VHS 0.11.0 or newer; vhs <tape> renders without parse errors; inspect.sh verifies GIF metadata outside the repository; each executable's path, version and hash is recorded. On fail: stop, max 0 retries.
- **Memory:** demo evidence log at `loops/vhs-demo-evidence-loop/run-log.md`. Read first: tape settings and geometry used for earlier demos.

## Steps

1. **Define the claim.** Write down the behavior, visible commands, initial state and the controlled variable.
2. **Run preflight.** Run .github/skills/vhs-demo/scripts/preflight.sh and stop if a tool is missing.
3. **Prove executables.** Record absolute path, version, revision and SHA-256 for each binary.
4. **Isolate the take.** Use a temp workspace, synthetic data and cleared credential variables.
5. **Render.** Author the tape with Wait+Screen for results and run vhs.
6. **Inspect.** Run inspect.sh and check every frame for secrets, clipping and transient states.
7. **Return evidence.** Report tape and GIF paths, size, duration and what the demo does not prove.

Stop rule: Stops after one before/after pair per run.

## Permissions

- Writes: loops/vhs-demo-evidence-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/vhs-demo-evidence-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: CLI output changes. Verification: preflight and inspection pass. Memory: loops/vhs-demo-evidence-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
