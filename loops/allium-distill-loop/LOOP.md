---
name: distill
title: Distill skill
repo: juxt/allium
license: MIT
url: https://gethabit.dev/skills/juxt/distill
---

# Distill skill

The distill skill extracts an Allium specification from an existing codebase, filtering out implementation detail so the spec captures what the system does, for teams documenting or reverse engineering behaviour.

- Install the skill: `npx skills add juxt/allium --skill distill`
- Source: https://github.com/juxt/allium/tree/HEAD/skills/distill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: code exists but no spec; reverse engineering behaviour from implementation; documenting a service in Allium terms.
Skip it when: building a spec for a new system; checking an existing spec against code.

# Make it a habit: Existing code gets a spec.

When a module has no spec yet, your agent maps it into bounded contexts, fans out one subagent per context and assembles an Allium spec. allium check must pass and the abstraction checklist must be clean. Open questions stay in the spec.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** module needs a spec (manual; Claude Code routine; `run on a chosen code path`)
- **Verification:** allium check + you confirm. Hard checks: allium check passes; first line is the -- allium: N version marker; scope comment lists includes and excludes; no database column types, ORM syntax or API paths in the spec; each concept has exactly one name. On fail: retry, max 2 retries.
- **Memory:** distilled spec questions at `loops/allium-distill-loop/notes.md`. Read first: parked open questions and excluded code paths.

## Steps

1. **Scope it.** Your agent asks which part of the codebase to cover and what to leave out.
2. **Map the territory.** It scans entry points, models, services and integrations and groups them into bounded contexts.
3. **Fan out.** One subagent per context extracts states, transitions, temporal triggers, boundaries and actors with file:line evidence.
4. **Assemble.** The agent merges the fragments, removes duplicates and picks one name per concept.
5. **Abstract.** It strips implementation details until the abstraction checklist is clean.
6. **Validate.** It runs allium check and allium analyse if available, then asks you whether the spec is right.

Stop rule: Stops after one bounded codebase area per run and at most two check retries.

## Permissions

- Writes: **/*.allium, loops/allium-distill-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/allium-distill-loop/notes.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: module needs a spec. Verification: allium check + you confirm. Memory: loops/allium-distill-loop/notes.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
