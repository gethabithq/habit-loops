---
name: spec
title: Spec skill
repo: klerith/fernando-skills
license: MIT
url: https://gethabit.dev/skills/klerith/spec
---

# Spec skill

Spec designs a feature spec with the spec-driven method: it asks clarifying questions before proposing structure, builds the spec section by section from a template, and saves a numbered draft to specs/. For teams planning a large feature before code.

- Install the skill: `npx skills add klerith/fernando-skills --skill spec`
- Source: https://github.com/klerith/fernando-skills/tree/HEAD/skills/engineering/spec
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You start a large feature; You want a spec before code; You need clarifying questions drawn out.
Skip it when: You want code written now; The change is a small tweak.

# Make it a habit: Each feature gets an approved spec.

Before a large feature is coded, your agent runs the spec-driven method: it reads the project memory and recent specs, asks clarifying questions in blocks until scope, data and verification are clear, writes the spec section by section from the template and saves it to specs/ as a numbered draft.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you start a feature (manual; Claude Code slash command; `run /spec with a description`)
- **Verification:** spec saved as draft. Hard checks: the three closing questions are answerable without assuming: which files change, first and last step, how to verify; the spec file exists at specs/NN-slug.md; the state is Draft, not Approved; listed dependencies exist in specs/. On fail: retry, max 1 retries.
- **Memory:** specs folder at `specs/`. Read first: the two most recent specs for numbering, language and conventions.

## Steps

1. **Understand the context.** Read the project-memory file and the two most recent specs for conventions and numbering.
2. **Clarify by questions.** Ask 3 to 5 concrete questions per block on scope, data, integration, persistence, states and risks until nothing is assumed.
3. **Write the spec.** Follow template.md: header, scope, data model, implementation plan, acceptance criteria, decisions and risks.
4. **Save as draft.** Write specs/NN-slug.md with the next number and the session date, state Draft, and seed .spec-config.yml if missing.
5. **Confirm and stop.** Report the path and that /spec-impl runs once the user approves; propose no further action.

Stop rule: Stops after one spec is written and saved per run.

## Permissions

- Writes: specs/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`specs/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you start a feature. Verification: spec saved as draft. Memory: specs/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
