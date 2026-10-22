---
name: plan-grill-loop
title: Plan grill loop
outcome: Turn every idea into tickets.
source: https://github.com/gethabithq/habit-loops
license: MIT
url: https://gethabit.dev/loops/plan-grill-loop
---

# Plan grill loop: Turn every idea into tickets.

When an issue gets the label idea, your agent grills you about it with grill me, writes the spec with to spec and splits it into tickets with to tickets. A hard check makes sure the spec has acceptance criteria and every ticket links it.

## Skills in this habit

Install each skill from its original repo first. Habit does not host or change them.

- Grill Me (worker): `npx skills add mattpocock/skills --skill grill-me` · https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me · MIT
- To Spec (worker): `npx skills add mattpocock/skills --skill to-spec` · https://github.com/mattpocock/skills/tree/main/skills/engineering/to-spec · MIT
- To Tickets (worker): `npx skills add mattpocock/skills --skill to-tickets` · https://github.com/mattpocock/skills/tree/main/skills/engineering/to-tickets · MIT

## The three decisions

- **Trigger:** issue labelled idea (event; GitHub Actions or Claude Code routine; `issues.labeled == idea`)
- **Verification:** you answer + spec check. Hard checks: spec has acceptance criteria; every ticket links the spec; no open questions left. On fail: notify, max 0 retries.
- **Memory:** workflow notes at `workflows/NOTES.md`. Read first: ideas already grilled and their specs.

## Steps

1. **Pick up the idea.** A new issue with the label idea starts the run.
2. **Grill.** Your agent asks the hard questions with grill me. You answer.
3. **Write the spec.** to spec writes the plan down with acceptance criteria.
4. **Split.** to tickets turns the spec into small issues.
5. **Check.** Spec has criteria, every ticket links it. Otherwise you get a note.

Stop rule: Stops after one idea per run.

## Permissions

- Writes: workflows/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`workflows/NOTES.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: issue labelled idea. Verification: you answer + spec check. Memory: workflows/NOTES.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`

Setup prompt: Read https://gethabit.dev/loops/plan-grill-loop.md and install this loop in my project. Show me the files first.
