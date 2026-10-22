---
name: appllama-app-design-skill
title: Appllama App Design Skill skill
repo: appllama/appllama-skills
license: MIT
url: https://gethabit.dev/skills/appllama/appllama-app-design-skill
---

# Appllama App Design Skill skill

Appllama app design skill builds native-feeling Expo and React Native screens with Apple HIG fidelity, semantic colors, native controls, navigation rules, purposeful motion and a simulator-verified loop. For mobile developers shipping polished app UI.

- Install the skill: `npx skills add appllama/appllama-skills --skill appllama-app-design-skill`
- Source: https://github.com/appllama/appllama-skills/tree/HEAD/skills/appllama-app-design-skill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a new mobile screen; You polish onboarding or paywalls; Your app feels like a web wrapper.
Skip it when: You build a web-only app; You do not use Expo or React Native.

# Make it a habit: Every mobile screen meets native quality.

For each new or changed mobile screen, your agent studies reference screens, builds with Expo, runs the slop pre-flight counts, then verifies in the simulator with screenshots and a full-motion recording. It repeats until no defect is found and logs the definition-of-done checklist.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** screen added or changed (event; Claude Code routine; `pull_request paths: app/**`)
- **Verification:** slop counts + simulator. Hard checks: distinct accent hues count is 1; emoji in UI chrome count is 0; gradients without a brand reason count is 0; light and dark mode screenshots exist from the simulator; a full-flow recording exists from xcrun simctl io booted recordVideo. On fail: retry, max 2 retries.
- **Memory:** screen checklist log at `loops/native-screen-polish-loop/log.md`. Read first: the locked accent, radius scale and patterns adopted per screen.

## Steps

1. **Study references.** Pull real screens for the screen type with the Appllama MCP if connected and name the pattern.
2. **Answer navigation.** Decide push, replace, modal, sheet or overlay and what back does on iOS and Android.
3. **Build natively.** Implement with semantic colors, native controls, SF Symbols and the stated spacing and radius rules.
4. **Run slop pre-flight.** Count accent hues, radii, emoji in chrome, unexplained gradients and duplicate labels.
5. **Simulator pass.** Screenshot light, dark, safe areas and Dynamic Type XL in the simulator.
6. **Full-motion pass.** Record the whole flow and scrub it frame by frame for drops, flashes and jumps.
7. **Fix and repeat.** Fix each defect, relaunch and re-verify until none is found.

Stop rule: Stops after one screen or flow per run, with at most 2 fix rounds.

## Permissions

- Writes: app/**, components/**, assets/**, loops/native-screen-polish-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/native-screen-polish-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: screen added or changed. Verification: slop counts + simulator. Memory: loops/native-screen-polish-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
