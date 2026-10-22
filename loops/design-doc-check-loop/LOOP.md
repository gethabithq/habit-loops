---
name: writing-design-docs
title: Writing Design Docs skill
repo: riekelt/technical-writer
license: MIT
url: https://gethabit.dev/skills/riekelt/writing-design-docs
---

# Writing Design Docs skill

The writing design docs skill gives a proposal skeleton, a Why & What decision box and completeness checks, for engineers writing RFCs, specs, design documents or migration plans that argue for a change.

- Install the skill: `npx skills add riekelt/technical-writer --skill writing-design-docs`
- Source: https://github.com/riekelt/technical-writer/tree/HEAD/plugins/technical-writer/skills/writing-design-docs
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Writing a proposal or RFC; Scoping a migration plan; Handing a spec to a reviewer.
Skip it when: Recording a decision already taken; Writing a runbook or status report.

# Make it a habit: Specs reach reviewers without vague gaps.

When a proposal, RFC or spec is opened for review, the agent checks the skeleton, the Why & What boxes, the benefits and costs chapter and the five vagueness defects. A board keeps open questions and their owners.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** design doc pull request (event; GitHub Actions; `pull_request adds or changes a design doc`)
- **Verification:** completeness check. Hard checks: no unmarked TBD, TODO or fill in later remains; every requirement has an independently testable acceptance criterion; every open question has an owner; the benefits chapter also names the costs. On fail: notify, max 1 retries.
- **Memory:** open questions board at `loops/design-doc-check-loop/board.md`. Read first: open questions, owners and DRAFT - input wanted blocks.

## Steps

1. **Load background.** The agent reads the technical-writing skill first.
2. **Check the skeleton.** The summary must give the conclusion and the chapters must be numbered.
3. **Check choices.** Each contested choice needs a Why & What box with a real alternative and its strongest argument.
4. **Check costs.** The benefits chapter must end with what the change costs.
5. **Run completeness.** It scans for the five vagueness defects before the spec goes to a reviewer.
6. **Mark sources.** Facts without a source get a source wanted marker, never an invented citation.
7. **Update the board.** Open questions and their owners go on the board.

Stop rule: Stops after one document per run, with at most 1 recheck.

## Permissions

- Writes: loops/design-doc-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/design-doc-check-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: design doc pull request. Verification: completeness check. Memory: loops/design-doc-check-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
