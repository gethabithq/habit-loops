---
name: uniwind
title: Uniwind skill
repo: uni-stack/uniwind
license: MIT
url: https://gethabit.dev/skills/uni-stack/uniwind
---

# Uniwind skill

Uniwind skill covers Tailwind CSS v4 styling for React Native with Uniwind: setup, Metro config, global.css themes, className and accent- props, variants, withUniwind, safe areas and troubleshooting. For React Native and Expo developers.

- Install the skill: `npx skills add uni-stack/uniwind --skill uniwind`
- Source: https://github.com/uni-stack/uniwind/tree/HEAD/skills/uniwind
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You style React Native with Tailwind; You set up Uniwind themes; Styles do not apply as expected.
Skip it when: You migrate from NativeWind; You build a web-only app.

# Make it a habit: React Native styles follow Uniwind rules.

On every pull request that touches React Native components, your agent checks the Uniwind critical rules: no dynamic classNames, no cssInterop or remapProps, no tailwind.config.js, no withUniwind on core components and accent- classes for non-style color props. A log keeps open issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** component files change (event; GitHub Actions or Claude Code routine; `pull_request paths: src/**, app/**, global.css`)
- **Verification:** rule scan count zero. Hard checks: no className is built with a template string; no cssInterop or remapProps call exists; no tailwind.config.js file exists; no react-native core component is wrapped with withUniwind; the app build passes. On fail: notify, max 0 retries.
- **Memory:** Uniwind issue log at `loops/uniwind-style-rules-loop/log.md`. Read first: open rule violations and the Uniwind version in use.

## Steps

1. **Identify the task.** Decide whether the change is setup, styling, theming, variants or integrations.
2. **Read the reference.** Read the matching file in references/, such as styling-patterns.md or theming.md.
3. **Scan the rules.** Check each changed file against the critical rules, including accent- props and single font families.
4. **Check themes.** Make sure every theme in global.css defines the same CSS variables.
5. **Verify unsure APIs.** Check unclear APIs against the official Uniwind docs instead of guessing.
6. **Log findings.** Record each violation with its file and the rule it breaks.

Stop rule: Stops after the changed files of one pull request, at most 30 files.

## Permissions

- Writes: loops/uniwind-style-rules-loop/**
- Network: docs.uniwind.dev
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/uniwind-style-rules-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: component files change. Verification: rule scan count zero. Memory: loops/uniwind-style-rules-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
