---
name: tend
title: Tend skill
repo: juxt/allium
license: MIT
url: https://gethabit.dev/skills/juxt/tend
---

# Tend skill

The tend skill writes, edits and refactors Allium specs: adding entities, rules, triggers and surfaces, fixing validation errors and migrating versions, while pushing back on vague requirements.

- Install the skill: `npx skills add juxt/allium --skill tend`
- Source: https://github.com/juxt/allium/tree/HEAD/skills/tend
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: adding a rule or entity to a spec; fixing allium check errors; renaming across spec files.
Skip it when: building a spec from scratch; extracting a spec from code.

# Make it a habit: Spec changes stay valid.

When a change request for an Allium spec arrives, your agent reads the existing specs, pushes back on vague parts and makes a minimal edit. allium check must pass after every edit. Changes and parked questions are logged for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** spec change requested (event; Claude Code routine; `issue labelled spec-change`)
- **Verification:** allium check passes. Hard checks: allium check passes on every modified .allium file; -- allium: N version marker unchanged; temporal triggers have requires guards; only .allium files changed. On fail: retry, max 2 retries.
- **Memory:** spec change log at `loops/allium-tend-loop/log.md`. Read first: open questions parked by earlier edits.

## Steps

1. **Start up.** Your agent reads the language reference and the relevant .allium files, and runs allium check first.
2. **Challenge vagueness.** It asks what happens at boundaries, under failure and with concurrency before writing.
3. **Check the flow.** It looks at data flow, transition graph impact and surface coverage for the new rule.
4. **Edit minimally.** It adds only what was asked and follows the spec writing guidelines.
5. **Verify.** It runs allium check after every edit and allium analyse if the spec qualifies.
6. **Explain.** It states the behavioural intent, shows the changes and logs open questions.

Stop rule: Stops after one change request per run and at most two check retries.

## Permissions

- Writes: **/*.allium, loops/allium-tend-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/allium-tend-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: spec change requested. Verification: allium check passes. Memory: loops/allium-tend-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
