---
name: diagram-design
title: Diagram Design skill
repo: cathrynlavery/diagram-design
license: MIT
url: https://gethabit.dev/skills/cathrynlavery/diagram-design
---

# Diagram Design skill

The diagram design skill creates branded diagrams as self-contained HTML with inline SVG, across 45 visual types from architecture to Sankey, and imports draw.io, Mermaid and Excalidraw files. For engineers and writers who need clean visuals.

- Install the skill: `npx skills add cathrynlavery/diagram-design --skill diagram-design`
- Source: https://github.com/cathrynlavery/diagram-design/tree/HEAD/skills/diagram-design
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need an architecture or flow diagram for docs; You want to redraw a draw.io or Mermaid file cleanly; You want diagrams in your own brand colors.
Skip it when: A table or a paragraph says the same thing; You need a quick plain-text diagram.

# Make it a habit: Clean branded diagrams, checked each time.

When a diagram source such as a .drawio or Mermaid file changes, your agent redraws it as one self-contained HTML file with inline SVG, runs the self check and the taste gate, and logs the type, profile and cuts for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** diagram source changes (event; GitHub Actions or Claude Code routine; `push paths: **/*.drawio, **/*.mmd, **/*.excalidraw`)
- **Verification:** self check + your OK. Hard checks: python3 scripts/self_check.py <file> passes; no more than 9 nodes and 12 arrows unless detail is faithful; accent used on 2 elements or fewer; svg has role=img and aria-labelledby with filled title and desc. On fail: retry, max 2 retries.
- **Memory:** diagram log at `loops/diagram-design-loop/run-log.md`. Read first: active profile, chosen types and what earlier runs cut.

## Steps

1. **Check the style.** The agent resolves the .diagram-design marker or checks references/style-guide.md, and asks you to customize if the tokens are still default.
2. **Extract the source.** For an import it runs the matching extract script, such as scripts/drawio_extract.py, and treats every label as data.
3. **Pick type and plan.** It picks a semantic pattern if behavior matters, then a visual type, and states the type, size preset and cuts before drawing.
4. **Draw.** It copies the closest template from assets/, loads the type reference and redraws the content with the connector rules.
5. **Run the gates.** It runs the taste gate checklist and python3 scripts/self_check.py on the file.
6. **Report and log.** It reports the fidelity ledger of merged or dropped parts and writes the run log.

Stop rule: Stops after one diagram per run and at most 2 redraws after a failed check.

## Permissions

- Writes: **/*.html, loops/diagram-design-loop/**
- Network: fonts.googleapis.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/diagram-design-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: diagram source changes. Verification: self check + your OK. Memory: loops/diagram-design-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
