---
name: grill-with-docs
title: Grill With Docs skill
repo: mattpocock/skills
license: MIT
url: https://gethabit.dev/skills/mattpocock/grill-with-docs
---

# Grill With Docs skill

The grill with docs skill by mattpocock runs a relentless interview on your plan and writes ADRs and a glossary as you go, by calling the grilling and domain modeling skills. For teams that want decisions kept.

- Install the skill: `npx skills add mattpocock/skills --skill grill-with-docs`
- Source: https://github.com/mattpocock/skills/tree/HEAD/skills/engineering/grill-with-docs
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You plan a new feature; You want decisions recorded; Your domain terms are fuzzy.
Skip it when: You need no written docs; The plan is already settled.

# Make it a habit: Plans grilled, decisions documented.

When you start a plan, your agent runs grill with docs: it calls the grilling skill to interview you and the domain modeling skill to write ADRs and a glossary as you go. A check makes sure the docs changed, and a log keeps each run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you start a plan (manual; Claude Code routine; `user invokes grill with docs`)
- **Verification:** you answer + docs check. Hard checks: at least one ADR or glossary entry was added or changed in the diff; the run log entry for this plan exists. On fail: notify, max 0 retries.
- **Memory:** grill runs log at `loops/grill-docs-loop/runs.md`. Read first: plans grilled before and the docs each run touched.

## Steps

1. **Start the plan.** You call grill with docs on a plan or design.
2. **Read the log.** Your agent reads past runs so it does not ask settled questions again.
3. **Grill.** It calls the grilling skill and interviews you hard about the plan.
4. **Model the domain.** It calls the domain modeling skill to record ADRs and glossary terms during the talk.
5. **Check the docs.** The diff must show at least one ADR or glossary change, otherwise you get a note.
6. **Log the run.** It writes the plan and the docs it touched to the run log.

Stop rule: Stops after one plan per run.

## Permissions

- Writes: loops/grill-docs-loop/**, project docs (ADRs and glossary)
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/grill-docs-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you start a plan. Verification: you answer + docs check. Memory: loops/grill-docs-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
