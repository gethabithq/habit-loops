---
name: planning-with-files
title: Planning with Files skill
repo: OthmanAdi/planning-with-files
license: MIT
url: https://gethabit.dev/skills/othmanadi/planning-with-files
---

# Planning with Files skill

Planning with files keeps an agent's plan, findings and progress in markdown files on disk, so long multi-step tasks survive context loss and compaction. Hooks feed the plan back in. For anyone running research or builds with many tool calls.

- Install the skill: `npx skills add OthmanAdi/planning-with-files --skill planning-with-files`
- Source: https://github.com/OthmanAdi/planning-with-files/tree/HEAD/.agents/skills/planning-with-files
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A task needs more than 5 tool calls; Work must survive compaction or a restart; Several agents share one task.
Skip it when: A simple question or quick lookup; A single-file edit.

# Make it a habit: Long tasks finish, nothing forgotten.

While a long task runs, your agent ticks every 10 minutes with planning-with-files: it re-reads task_plan.md and progress.md, runs check-complete.sh and logs progress. Errors go into the plan, and after three failed attempts it asks you.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every 10 minutes (schedule; Claude Code /loop; `/plan-loop 10m`)
- **Verification:** phases complete + escalation. Hard checks: scripts/check-complete.sh reports ALL PHASES COMPLETE; every phase in task_plan.md reports Status: complete; task_plan.md matches its attestation hash when one is set. On fail: retry, max 2 retries.
- **Memory:** plan, findings, progress files at `task_plan.md`. Read first: task_plan.md, progress.md and findings.md from the selected plan folder.

## Steps

1. **Restore plan state.** The agent resolves the plan folder with scripts/resolve-plan-dir.sh and reads the three planning files.
2. **Check code changes.** It runs git diff --stat to spot work not yet written to the plan.
3. **Work the phase.** It works on the in_progress phase and saves findings to findings.md after every two lookups.
4. **Log errors.** It writes each error to the plan and never repeats the same failed action.
5. **Update progress.** It marks finished phases complete and adds a progress.md entry.
6. **Check completion.** It runs scripts/check-complete.sh to see if all phases are done.
7. **Escalate after three.** After three failed attempts on one error, it explains what it tried and asks you for guidance.

Stop rule: Stops when check-complete.sh reports all phases complete, or after 3 failed attempts on one error.

## Permissions

- Writes: task_plan.md, findings.md, progress.md, .planning/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`task_plan.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every 10 minutes. Verification: phases complete + escalation. Memory: task_plan.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
