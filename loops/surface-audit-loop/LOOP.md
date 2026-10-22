---
name: layers-surface
title: Layers Surface skill
repo: jamiemill/layers-skills
license: MIT
url: https://gethabit.dev/skills/jamiemill/layers-surface
---

# Layers Surface skill

Layers surface is a skill for product designers that audits the surface layer against the layers below: vocabulary, object consistency, completeness, feedback and errors, hierarchy, emotional register and accessibility.

- Install the skill: `npx skills add jamiemill/layers-skills --skill layers-surface`
- Source: https://github.com/jamiemill/layers-skills/tree/HEAD/skills/layers-surface
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Labels feel inconsistent; Users do not know what happened; Accessibility was left to defaults.
Skip it when: No conceptual model exists yet; You need a visual design system built.

# Make it a habit: Surface matches the model below.

After a significant change to the conceptual model or interaction structure, your agent audits the surface: vocabulary, object consistency, completeness, feedback and errors, hierarchy and accessibility. Each finding is tagged surface fix or deeper-layer issue.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** model or flow changes (event; Claude Code routine; `event: conceptual model or breadboard updated`)
- **Verification:** findings tagged, designer reviews. Hard checks: every label is checked against the ubiquitous language list; every breadboard affordance is present on the surface; every error state diagnoses, explains and offers recovery. On fail: notify, max 0 retries.
- **Memory:** surface audit findings at `loops/surface-audit-loop/findings.md`. Read first: open findings, cross-layer issues and what already works.

## Steps

1. **Establish context.** Ask the designer for the medium and what exists below: model, breadboard and job stories.
2. **Pick techniques.** Choose the checks that fit the live concern instead of running all ten.
3. **Run the checks.** Run the chosen checks, such as vocabulary, object consistency, completeness or accessibility.
4. **Tag findings.** Mark each finding as a surface fix or a deeper-layer issue.
5. **Route deeper issues.** Send flow gaps to /layers-interaction-flow instead of patching the symptom.
6. **Capture residue.** Write findings, open decisions and what works well into the findings file.

Stop rule: Stops after three techniques per run.

## Permissions

- Writes: loops/surface-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/surface-audit-loop/findings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: model or flow changes. Verification: findings tagged, designer reviews. Memory: loops/surface-audit-loop/findings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
