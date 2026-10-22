---
name: writing-prds
title: Writing PRDs skill
repo: refoundai/lenny-skills
license: MIT
url: https://gethabit.dev/skills/refoundai/writing-prds
---

# Writing PRDs skill

The writing prds skill helps turn ideas into short product requirement documents: a clear problem, measurable success metrics, bounded scope and a clarity review. For product managers aligning design and engineering.

- Install the skill: `npx skills add refoundai/lenny-skills --skill writing-prds`
- Source: https://github.com/refoundai/lenny-skills/tree/HEAD/skills/writing-prds
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: writing a new PRD or one-pager; reviewing a spec draft; defining success metrics for a project.
Skip it when: you need a technical design doc; the work is already fully specified.

# Make it a habit: Short PRDs with clear problems.

When a new spec draft appears, your agent helps write or reviews it: a solution-free problem statement, measurable success metrics, explicit non-goals and a one-page length, flagging common mistakes. A notes file keeps reviewed PRDs and open questions.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new PRD draft (event; Claude Code routine; `a PRD or one-pager file is added or changed`)
- **Verification:** core sections present. Hard checks: the draft has a problem statement near the top; at least one success metric is listed; a non-goals or out-of-scope section exists; the draft fits on about one page. On fail: notify, max 0 retries.
- **Memory:** PRD review notes at `loops/prd-review-loop/notes.md`. Read first: earlier reviews and unanswered questions per PRD.

## Steps

1. **Draft the problem.** Your agent helps state the core problem in a few sentences without naming a solution.
2. **Set metrics.** It helps define specific, measurable outcomes that later filter feature requests.
3. **Bound the scope.** It narrows fuzzy requests with shaping techniques and lists what is out of scope.
4. **Ask questions.** It asks you the key questions about the problem, metrics, non-goals, engineering input and time budget.
5. **Review clarity.** It audits the draft for brevity and readability and flags over-specification.
6. **Flag mistakes.** It flags the common mistakes, like the word just, early high-fidelity mocks, missing non-goals and waterfall handoffs.

Stop rule: Stops after one PRD per run, with no automatic rewrites.

## Permissions

- Writes: loops/prd-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/prd-review-loop/notes.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new PRD draft. Verification: core sections present. Memory: loops/prd-review-loop/notes.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
