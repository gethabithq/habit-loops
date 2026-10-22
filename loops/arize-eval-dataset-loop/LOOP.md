---
name: arize-dataset
title: Arize Dataset skill
repo: arize-ai/arize-skills
license: MIT
url: https://gethabit.dev/skills/arize-ai/arize-dataset
---

# Arize Dataset skill

The arize dataset skill creates, manages and queries Arize datasets with the ax CLI: create from files, append examples, export versions and verify completeness. For teams building golden datasets and test sets for AI evaluation.

- Install the skill: `npx skills add arize-ai/arize-skills --skill arize-dataset`
- Source: https://github.com/arize-ai/arize-skills/tree/HEAD/skills/arize-dataset
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: creating a golden dataset; appending test examples; exporting a dataset version.
Skip it when: you do not use Arize; you only need to run experiments.

# Make it a habit: A growing, verified evaluation dataset.

When new test cases appear, your agent checks the dataset schema, appends the examples with ax datasets append, then exports with --all and confirms the row count matches the server. Arize dataset versions are the memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new test cases added (event; GitHub Actions or Claude Code routine; `new examples file committed`)
- **Verification:** export count matches server. Hard checks: new examples have the same field names as existing ones; ax datasets append exits with success; exported row count matches the server example_count. On fail: notify, max 1 retries.
- **Memory:** dataset version notes at `loops/arize-eval-dataset-loop/run-log.md`. Read first: the latest dataset version and its example count.

## Steps

1. **Find dataset.** Your agent looks up the dataset with ax datasets get by name or ID.
2. **Check schema.** It exports one example and compares its field names with the new data to catch typos.
3. **Append.** It appends the new examples with --json or --file, leaving out server fields like id.
4. **Export all.** It exports the dataset with --all.
5. **Verify count.** It compares the exported row count with the server's example_count and re-exports if they differ.
6. **Hand off.** It points to the arize-experiment skill to run evaluations on the updated dataset.

Stop rule: Stops after one append and one verified export per run, with at most one retry.

## Permissions

- Writes: dataset export folders, loops/arize-eval-dataset-loop/**
- Network: app.arize.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/arize-eval-dataset-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new test cases added. Verification: export count matches server. Memory: loops/arize-eval-dataset-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
