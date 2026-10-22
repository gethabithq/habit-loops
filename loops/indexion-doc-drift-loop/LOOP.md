---
name: indexion-documentation
title: Indexion Documentation skill
repo: trkbt10/indexion-skills
license: Apache-2.0
url: https://gethabit.dev/skills/trkbt10/indexion-documentation
---

# Indexion Documentation skill

Indexion documentation analyzes doc coverage, finds code-to-doc drift with plan reconcile and draws dependency graphs with doc graph. For maintainers who want to know what needs docs and whether existing docs are still accurate.

- Install the skill: `npx skills add trkbt10/indexion-skills --skill indexion-documentation`
- Source: https://github.com/trkbt10/indexion-skills/tree/HEAD/skills/indexion-documentation
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You check doc coverage; You suspect stale READMEs; You need a dependency diagram.
Skip it when: You build or assemble a README; Your project does not use indexion.

# Make it a habit: Docs keep up with the code.

Each week your agent measures doc coverage with indexion plan documentation, lists undocumented items with indexion grep --undocumented and runs indexion plan reconcile to find stale docs. It fixes flagged docs, re-runs reconcile and logs the coverage number.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly docs drift check (schedule; GitHub Actions or Claude Code routine; `0 7 * * 1`)
- **Verification:** coverage + reconcile rerun. Hard checks: coverage percentage is not lower than last run; plan reconcile after fixes lists fewer stale docs than before; indexion grep --undocumented count does not grow. On fail: notify, max 1 retries.
- **Memory:** coverage history log at `loops/indexion-doc-drift-loop/log.md`. Read first: last coverage percentage and open stale docs.

## Steps

1. **Measure coverage.** Run indexion plan documentation --style=coverage on the project.
2. **List gaps.** Run indexion grep --undocumented src/ for the missing doc comments.
3. **Find drift.** Run indexion plan reconcile --format=md and read the vocabulary divergence table.
4. **Fix flagged docs.** Add doc comments and enrich READMEs that show high divergence.
5. **Re-verify.** Run indexion plan reconcile --format=md again and log the new numbers.

Stop rule: Stops after at most 10 fixed docs and one re-verify per run.

## Permissions

- Writes: src/**, docs/**, **/README.md, .indexion/cache/reconcile/**, loops/indexion-doc-drift-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/indexion-doc-drift-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly docs drift check. Verification: coverage + reconcile rerun. Memory: loops/indexion-doc-drift-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
