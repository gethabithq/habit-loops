---
name: prd-creator
title: PRD Creator skill
repo: pageai-pro/ralph-loop
license: MIT
url: https://gethabit.dev/skills/pageai-pro/prd-creator
---

# PRD Creator skill

Prd creator turns a rough software idea into a full product requirements document through structured questions, then generates a JSON task list with verifiable pass criteria. For beginner developers planning features or apps for coding agents.

- Install the skill: `npx skills add pageai-pro/ralph-loop --skill prd-creator`
- Source: https://github.com/pageai-pro/ralph-loop/tree/HEAD/.agent/skills/prd-creator
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You document a new software idea; You plan a feature for an agent; You need tasks with pass criteria.
Skip it when: You want code written now; Your spec already exists and is final.

# Make it a habit: Ideas become PRDs and tasks.

When you start a new feature or app idea, your agent asks clarifying questions, gets your approval on an executive summary, writes PRD.md and SUMMARY.md, and generates tasks.json with TASK-1 as prerequisite check. A file check confirms all three files exist.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you describe an idea (manual; Claude Code routine; `on request`)
- **Verification:** you approve + file check. Hard checks: .agent/prd/PRD.md exists; .agent/prd/SUMMARY.md exists; .agent/tasks.json exists and starts with TASK-1; every task has "passes": false; no real secret values in .env.local. On fail: notify, max 0 retries.
- **Memory:** PRD summary at `.agent/prd/SUMMARY.md`. Read first: the project summary, main features and key requirements.

## Steps

1. **Understand the idea.** Read your short description and think about the larger architecture behind it.
2. **Ask questions.** Use AskUserQuestion to fill the gaps in requirements.
3. **Check prerequisites.** Verify access, MCPs, docs, env variables and test users, and write placeholders only to .env.local.
4. **Get summary approval.** Write an executive summary and wait for your approval.
5. **Research and write.** Research the competition with WebSearch and write the full PRD.md.
6. **Generate tasks.** Turn the PRD into small tasks in tasks.json, starting with TASK-1 and all set to not passing.
7. **Confirm the files.** Check that PRD.md, SUMMARY.md and tasks.json exist and warn you if any is missing.

Stop rule: Stops after one PRD and one task list per run.

## Permissions

- Writes: .agent/**, .env.local
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.agent/prd/SUMMARY.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you describe an idea. Verification: you approve + file check. Memory: .agent/prd/SUMMARY.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
