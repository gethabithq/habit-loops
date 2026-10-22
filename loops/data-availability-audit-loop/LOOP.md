---
name: nature-data
title: Nature Data skill
repo: yuan1z0825/nature-skills
license: Apache-2.0
url: https://gethabit.dev/skills/yuan1z0825/nature-data
---

# Nature Data skill

The nature data skill drafts and audits Data and Code Availability statements, dataset access routes, repository plans and FAIR metadata, for researchers preparing a manuscript for journal submission.

- Install the skill: `npx skills add yuan1z0825/nature-skills --skill nature-data`
- Source: https://github.com/yuan1z0825/nature-skills/tree/HEAD/skills/nature-data
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Drafting a Data Availability statement; Choosing a repository and identifiers; Auditing a statement before submission.
Skip it when: General data cleaning; Statistical analysis.

# Make it a habit: Every dataset has an access route.

Before a manuscript goes to a journal, the agent lists every supporting dataset, gives each one access route, drafts the Data Availability statement and runs the FAIR metadata audit. Unresolved fields stay on a board for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** before manuscript submission (manual; Claude Code routine; `manual run per manuscript revision`)
- **Verification:** route and metadata audit. Hard checks: every supporting dataset maps to exactly one access route; no DOI, accession number, repository name or licence appears that the author did not supply; available upon request is flagged as weak unless a specific restriction is named; the FAIR/metadata audit lists each open item as an unresolved field. On fail: notify, max 0 retries.
- **Memory:** unresolved dataset fields at `loops/data-availability-audit-loop/board.md`. Read first: unresolved fields and missing identifiers from the last audit.

## Steps

1. **Load the core.** The agent reads manifest.yaml, then static/core/stance.md and static/core/workflow.md.
2. **Identify the journal.** It names the journal and article type, and journal rules win where they differ.
3. **List datasets.** It makes an inventory of every dataset that supports the paper.
4. **Classify routes.** Each dataset gets one route, such as public repository, controlled access or within paper.
5. **Plan repositories.** It picks the repository and identifier strategy before any drafting.
6. **Draft and cite.** It writes the statement with a dataset-to-location map and formal dataset citations.
7. **Run the FAIR audit.** It checks metadata with references/fair-metadata-checklist.md and returns paste-ready text plus open fields.

Stop rule: Stops after one manuscript per run, with no more than 2 redraft rounds.

## Permissions

- Writes: loops/data-availability-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/data-availability-audit-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: before manuscript submission. Verification: route and metadata audit. Memory: loops/data-availability-audit-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
