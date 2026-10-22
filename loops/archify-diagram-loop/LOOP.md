---
name: archify
title: Archify skill
repo: tt-a1i/archify
license: MIT
url: https://gethabit.dev/skills/tt-a1i/archify
---

# Archify skill

Archify turns a codebase or an idea into an interactive architecture diagram. Your agent reads the structure and draws boxes and arrows you can click through.

- Install the skill: `npx skills add tt-a1i/archify --skill archify`
- Source: https://github.com/tt-a1i/archify
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: New people need to understand the codebase fast; You want a diagram that matches the real files; You review a design before you build it.
Skip it when: The project is a single small script; You need a hand-drawn whiteboard sketch.

# Make it a habit: Diagrams that match the code.

After changes land on main, your agent redraws the architecture diagram from repository evidence and runs archify finalize. The run passes only when every finalize gate passes. A run log keeps the candidate folder and receipt per run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** push to main (event; GitHub Actions or Claude Code routine; `push to main`)
- **Verification:** finalize gates pass. Hard checks: node bin/archify.mjs finalize exits 0; receipt shows validate, deliver, check and browser-check passed; output HTML file exists. On fail: retry, max 2 retries.
- **Memory:** candidates and receipts at `loops/archify-diagram-loop/run-log.md`. Read first: the last candidate.json folder and its finalize receipt.

## Steps

1. **Pick the type.** Choose the diagram type from the Type router, such as architecture or dataflow.
2. **Read references.** Read the authoring defaults, the schema and the example, plus repository authoring for code-backed diagrams.
3. **Write the candidate.** Write candidate.json in a new .archify folder with source evidence from the repo.
4. **Finalize.** Run finalize with --repo-root and --quality showcase and keep the candidate unchanged meanwhile.
5. **Repair.** On a non-zero exit, repair the failed gate and rerun finalize with its own --out-dir.
6. **Report.** Link the HTML and note any update notice from the receipt.

Stop rule: Stops after one diagram per run, with at most 2 repair rounds.

## Permissions

- Writes: .archify/**, loops/archify-diagram-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/archify-diagram-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: push to main. Verification: finalize gates pass. Memory: loops/archify-diagram-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
