---
name: nature-figure
title: Nature Figure skill
repo: Yuan1z0825/nature-skills
license: Apache-2.0
url: https://gethabit.dev/skills/yuan1z0825/nature-figure
---

# Nature Figure skill

The nature figure skill helps researchers create, revise, audit and export submission-ready scientific figures in Python or R, with a figure contract, multi-panel planning and automated alignment, text and collision checks.

- Install the skill: `npx skills add Yuan1z0825/nature-skills --skill nature-figure`
- Source: https://github.com/Yuan1z0825/nature-skills/tree/HEAD/skills/nature-figure
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You make a multi-panel manuscript figure; You prepare figures for a Nature journal; You audit a figure PDF before submission.
Skip it when: You need an interactive dashboard; You only need statistics or data cleaning.

# Make it a habit: Every figure passes QA before delivery.

Whenever a manuscript figure script changes, your agent re-renders it in the chosen backend, then runs the panel alignment, source validation, PDF text and collision audits. A failed gate blocks delivery, and a log keeps the audit results.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Figure script changes (event; GitHub Actions or Claude Code routine; `push touching figure plotting scripts`)
- **Verification:** audits pass, you review. Hard checks: scripts/validate_figure.py passes on the plotting source; scripts/audit_pdf_text.py passes on the exported PDF; scripts/audit_figure_collisions.py exits 0 on the final PDF; panel alignment audit has no FIX BEFORE DELIVERY result. On fail: retry, max 2 retries.
- **Memory:** figure audit log at `loops/nature-figure-qa-loop/run-log.md`. Read first: backend, last audit results and recorded exemptions.

## Steps

1. **Load the core.** The agent reads manifest.yaml and the always_load contract and stance files.
2. **Resolve the backend.** It uses the saved choice from scripts/nature_figure_backend.py get, or asks you once: Python or R.
3. **Load the fragment.** It reads only the matching Python or R backend fragment.
4. **Build to contract.** It writes the core conclusion and evidence chain, then renders the figure.
5. **Check alignment.** It runs the panel alignment audit on multi-panel figures at final size.
6. **Run audits.** It runs validate_figure.py, audit_pdf_text.py and audit_figure_collisions.py on the export.
7. **Repair or deliver.** On a blocking result it repairs, re-exports and reruns every check.

Stop rule: Stops after one figure per run, with at most 2 repair rounds.

## Permissions

- Writes: figure output folder, loops/nature-figure-qa-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/nature-figure-qa-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Figure script changes. Verification: audits pass, you review. Memory: loops/nature-figure-qa-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
