---
name: ralph
title: Ralph skill
repo: snarktank/ralph
license: MIT
url: https://gethabit.dev/skills/snarktank/ralph
---

# Ralph skill

Ralph is a skill that converts a PRD into the prd.json format for the Ralph autonomous agent system, with right-sized user stories, dependency order and verifiable acceptance criteria. For developers who run Ralph.

- Install the skill: `npx skills add snarktank/ralph --skill ralph`
- Source: https://github.com/snarktank/ralph/tree/HEAD/skills/ralph
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You have a PRD to run with Ralph; You need prd.json from a markdown spec; You start a new Ralph feature.
Skip it when: You have no PRD yet; You do not use Ralph.

# Make it a habit: Every PRD becomes runnable stories.

When a new PRD lands, your agent archives the old prd.json if the branch changed, splits the PRD into small ordered user stories and writes prd.json. A checklist makes sure every story is small, ordered and checkable.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new PRD file added (event; Claude Code routine; `event: new PRD markdown in the ralph directory`)
- **Verification:** prd.json checklist passes. Hard checks: every story has Typecheck passes as a criterion; UI stories include Verify in browser using dev-browser skill; story ids run in order from US-001; branchName starts with ralph/; all stories have passes false. On fail: retry, max 1 retries.
- **Memory:** Ralph progress file at `progress.txt`. Read first: the current prd.json branchName and progress.txt content.

## Steps

1. **Archive old run.** If prd.json exists with a different branchName and progress.txt has content, copy both into archive/YYYY-MM-DD-feature-name/ and reset progress.txt.
2. **Split stories.** Cut the PRD into stories small enough for one Ralph iteration.
3. **Order by dependency.** Put schema first, then backend, then UI, then summary views.
4. **Write criteria.** Give each story checkable criteria, add Typecheck passes, and add the dev-browser skill check for UI stories.
5. **Save prd.json.** Write prd.json with sequential ids, priorities and empty notes.
6. **Run the checklist.** Confirm no story depends on a later one and no criterion is vague.

Stop rule: Stops after one PRD per run, with at most one retry.

## Permissions

- Writes: prd.json, progress.txt, archive/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`progress.txt`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new PRD file added. Verification: prd.json checklist passes. Memory: progress.txt. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
