---
name: nature-polishing
title: Nature Polishing skill
repo: yuan1z0825/nature-skills
license: Apache-2.0
url: https://gethabit.dev/skills/yuan1z0825/nature-polishing
---

# Nature Polishing skill

The nature polishing skill polishes, translates or tightens existing academic prose in Nature style while keeping facts, terms and evidence limits, and fixes LaTeX layout. For researchers preparing manuscripts.

- Install the skill: `npx skills add yuan1z0825/nature-skills --skill nature-polishing`
- Source: https://github.com/yuan1z0825/nature-skills/tree/HEAD/skills/nature-polishing
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You polish a draft for a Nature journal; You translate a Chinese manuscript to English; You fix loose LaTeX pages or floats.
Skip it when: You need to draft a new section; You want to rebuild the paper's argument.

# Make it a habit: Tighter prose, same facts.

When a manuscript section changes, your agent detects paper type, section, language and journal, loads only the matching guidance, polishes the prose without new claims, and checks that terms and numbers stay the same. A log keeps the chosen axes.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** manuscript section changes (event; Claude Code routine; `push paths: **/*.tex`)
- **Verification:** facts kept + your check. Hard checks: every number in the original text still appears after the polish; key terms are unchanged across affected passages; the LaTeX file compiles after layout fixes. On fail: notify, max 1 retries.
- **Memory:** axes and terms log at `loops/manuscript-polish-loop/run-log.md`. Read first: axis values chosen before and terms fixed in earlier rounds.

## Steps

1. **Load the core.** The agent reads manifest.yaml and every file under always_load.
2. **Detect the axes.** It picks paper_type, section, language and journal, states them in one line, and asks you if the section is unclear.
3. **Load fragments.** It reads only the fragments the manifest maps to those values, plus the shared Nature guidance for the section.
4. **Polish.** It applies paper type, section, journal and language rules in order and flags gaps instead of inventing content.
5. **Sweep consistency.** It rechecks affected terms, numbers and claims, using consistency-sweep.md for a whole manuscript.
6. **Fix layout.** For placement problems it loads references/latex-layout.md, compiles and inspects the rendered pages.

Stop rule: Stops after one changed section per run and at most 1 retry.

## Permissions

- Writes: **/*.tex, loops/manuscript-polish-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/manuscript-polish-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: manuscript section changes. Verification: facts kept + your check. Memory: loops/manuscript-polish-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
