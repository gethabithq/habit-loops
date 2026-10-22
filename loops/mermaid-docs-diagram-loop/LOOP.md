---
name: mermaid-diagrams
title: Mermaid Diagrams skill
repo: softaworks/agent-toolkit
license: MIT
url: https://gethabit.dev/skills/softaworks/mermaid-diagrams
---

# Mermaid Diagrams skill

The mermaid diagrams skill creates software diagrams in Mermaid syntax: class, sequence, flowchart, ERD, C4, state, git graph, gantt and charts, with type selection, theming and export through the Mermaid CLI. For developers documenting systems.

- Install the skill: `npx skills add softaworks/agent-toolkit --skill mermaid-diagrams`
- Source: https://github.com/softaworks/agent-toolkit/tree/HEAD/dist/plugins/mermaid-diagrams/skills/mermaid-diagrams
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You document system architecture; You design a database schema; You map an API or user flow.
Skip it when: You need pixel-perfect design graphics; Your docs tool cannot render Mermaid.

# Make it a habit: Keep diagrams matched to the code.

When architecture, schema or flows change, your agent picks the right Mermaid diagram type, updates the .mmd file next to the code, renders it with mmdc to catch syntax errors, and keeps one focused diagram per concept.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** structure or flow changes (event; Claude Code routine; `pull request changes models, schemas, APIs or architecture docs`)
- **Verification:** diagrams render cleanly. Hard checks: mmdc -i input.mmd -o output.png succeeds for each changed diagram; the first line declares a diagram type; output file exists. On fail: retry, max 2 retries.
- **Memory:** diagram files in git at `loops/mermaid-docs-diagram-loop/diagrams.md`. Read first: which .mmd files cover which parts of the code.

## Steps

1. **Find the change.** Your agent sees which models, flows or services changed.
2. **Pick a type.** It chooses class, sequence, flowchart, ERD, C4, state or other diagrams per the selection guide.
3. **Update the source.** It edits the .mmd file, adding %% comments for complex links.
4. **Split if large.** It splits crowded diagrams into focused views.
5. **Render.** It renders with mmdc to catch syntax errors, using references/advanced-features.md for themes.

Stop rule: Stops after the changed diagrams and 2 render retries each.

## Permissions

- Writes: **/*.mmd, docs/**, loops/mermaid-docs-diagram-loop/**
- Network: mermaid.live
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/mermaid-docs-diagram-loop/diagrams.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: structure or flow changes. Verification: diagrams render cleanly. Memory: loops/mermaid-docs-diagram-loop/diagrams.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
