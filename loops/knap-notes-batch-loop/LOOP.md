---
name: knap
title: Knap skill
repo: kepano/obsidian-skills
license: MIT
url: https://gethabit.dev/skills/kepano/knap
---

# Knap skill

The knap skill uses the Knap CLI to render Markdown notes from templates and JSON or CSV data, one file or a whole batch. For note-takers who turn structured data or clipped pages into notes.

- Install the skill: `npx skills add kepano/obsidian-skills --skill knap`
- Source: https://github.com/kepano/obsidian-skills/tree/HEAD/skills/knap
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You turn CSV rows into notes; You apply a template to JSON; You format Defuddle output as a note.
Skip it when: You need browser-only Web Clipper variables; You write notes by hand.

# Make it a habit: Turn new data into notes.

When new JSON or CSV data lands, your agent validates the Knap template, does a dry run, then renders one Markdown note per row or object with knap batch. A run log keeps which files were written.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new data file arrives (event; Claude Code routine; `new CSV or JSON file in the data folder`)
- **Verification:** validate and dry run. Hard checks: knap validate template.md exits 0; knap batch --dry-run lists no duplicate names; output note count matches input rows. On fail: notify, max 1 retries.
- **Memory:** rendered files log at `loops/knap-notes-batch-loop/runs.md`. Read first: data files already rendered and their output paths.

## Steps

1. **Check the CLI.** Your agent checks knap is installed, or uses npx knap.
2. **Validate the template.** It runs knap validate on the template.
3. **Dry run.** It runs knap batch with --dry-run to list output paths.
4. **Render.** It runs knap batch with --output-dir and a safe_name --filename.
5. **Log.** It records the data file and the notes it wrote.

Stop rule: Stops after one data file per run.

## Permissions

- Writes: notes/**, loops/knap-notes-batch-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/knap-notes-batch-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new data file arrives. Verification: validate and dry run. Memory: loops/knap-notes-batch-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
