---
name: indexion-sdd
title: Indexion SDD skill
repo: trkbt10/indexion-skills
license: Apache-2.0
url: https://gethabit.dev/skills/trkbt10/indexion-sdd
---

# Indexion SDD skill

Indexion sdd drafts spec-driven development requirements from RFCs and standards, then measures how well the implementation conforms with spec align and spec verify, including CI drift gates and a codex or claude validation loop. For teams implementing specifications.

- Install the skill: `npx skills add trkbt10/indexion-skills --skill indexion-sdd`
- Source: https://github.com/trkbt10/indexion-skills/tree/HEAD/skills/indexion-sdd
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You implement an RFC as a library; You gate merges on spec conformance; You run cc-sdd with codex or claude.
Skip it when: You have no written specification; Your project does not use indexion.

# Make it a habit: Implementation stays aligned with the spec.

On every pull request your agent runs indexion spec align status with --fail-on any and --threshold 0.3 against the requirements, plus spec verify and spec align diff for the report. A failing gate blocks the merge and the report lists DRIFTED, SPEC_ONLY and SHALLOW items.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions; `pull_request paths: src/**, .kiro/specs/**`)
- **Verification:** spec align gate. Hard checks: indexion spec align status --fail-on any --threshold 0.3 exits 0; Shallow count is 0; E2E tests on real input pass. On fail: notify, max 0 retries.
- **Memory:** SDD reports folder at `.indexion/sdd-reports/`. Read first: the last align-diff and verify-gaps reports.

## Steps

1. **Check the tool.** Run indexion --version and indexion kgf edges on a source file to confirm the gate can run.
2. **Report gaps.** Run indexion spec verify and indexion spec align diff with --threshold 0.3 and save them to .indexion/sdd-reports/.
3. **Run the gate.** Run indexion spec align status with --fail-on any against src/.
4. **Run E2E tests.** Run the end-to-end tests on real input, since vocabulary alignment cannot prove the code works.
5. **Suggest fixes.** On failure, run spec align suggest and post the DRIFTED, SPEC_ONLY and SHALLOW items to the PR summary.

Stop rule: Stops after one gate run per pull request, with no retries.

## Permissions

- Writes: .indexion/sdd-reports/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.indexion/sdd-reports/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: spec align gate. Memory: .indexion/sdd-reports/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
