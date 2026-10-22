---
name: gemini-api-dev
title: Gemini API Dev skill
repo: google-gemini/gemini-skills
license: Apache-2.0
url: https://gethabit.dev/skills/google-gemini/gemini-api-dev
---

# Gemini API Dev skill

The gemini api dev skill helps developers write Python and TypeScript code for the Gemini API, with current models, the interactions API, streaming, agents and migration notes.

- Install the skill: `npx skills add google-gemini/gemini-skills --skill gemini-api-dev`
- Source: https://github.com/google-gemini/gemini-skills/tree/HEAD/skills/gemini-api-dev
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You write code that calls Gemini; You migrate from generateContent; You build with Deep Research or managed agents.
Skip it when: You need the real-time Live API; You use a different model provider.

# Make it a habit: No deprecated Gemini models ship.

Each week your agent scans the codebase for legacy Gemini model strings and deprecated SDKs, confirms the migration scope with you, migrates using the skill's migration guide and docs, and logs what changed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly model scan (schedule; Claude Code routine or GitHub Actions; `0 8 * * 1`)
- **Verification:** no legacy models, tests pass. Hard checks: no gemini-2.5-*, gemini-2.0-* or gemini-1.5-* model strings remain; google-generativeai and @google/generative-ai are not in the dependencies; google-genai or @google/genai meets the minimum version; tests pass. On fail: notify, max 1 retries.
- **Memory:** migration log at `loops/gemini-model-freshness-loop/run-log.md`. Read first: files migrated and scope you approved before.

## Steps

1. **Scan.** The agent searches the code for deprecated model strings and legacy SDK imports.
2. **Confirm scope.** It lists the hits and asks you to confirm the migration scope, as the skill requires.
3. **Read the docs.** It reads references/migration.md and fetches the matching hosted docs page before editing.
4. **Migrate.** It swaps model strings to current models and moves old generateContent calls to the interactions API.
5. **Re-specify per turn.** It checks tools, system_instruction and generation_config are passed on every turn.
6. **Test and log.** It runs the tests and writes the changes to the run log.

Stop rule: Stops after migrating at most 10 files per run.

## Permissions

- Writes: src/**, loops/gemini-model-freshness-loop/**
- Network: ai.google.dev
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/gemini-model-freshness-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly model scan. Verification: no legacy models, tests pass. Memory: loops/gemini-model-freshness-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
