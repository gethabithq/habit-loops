---
name: drawio
title: Draw.io skill
repo: bahayonghang/drawio-skills
license: MIT
url: https://gethabit.dev/skills/bahayonghang/drawio
---

# Draw.io skill

The draw io skill creates, edits, imports and exports draw.io diagrams from a YAML spec, offline, for developers who need architecture maps, flowcharts, UML or network topologies.

- Install the skill: `npx skills add bahayonghang/drawio-skills --skill drawio`
- Source: https://github.com/bahayonghang/drawio-skills/tree/HEAD/skills/drawio
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: drawing an architecture diagram; converting Mermaid or CSV to draw.io; redrawing a screenshot of a diagram.
Skip it when: figures for a paper or thesis; a quick sketch with no file needed.

# Make it a habit: Diagrams stay valid and current.

Runs when a diagram spec changes. Your agent renders the YAML spec to .drawio and a 300dpi PNG, runs the built-in validator, inspects the exported image, and keeps a review record of open blockers for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** diagram spec changed (event; Claude Code routine or GitHub Actions; `push touches *.spec.yaml`)
- **Verification:** validator and export check. Hard checks: cli.js --validate reports no errors; the .drawio file exists; a PNG or fallback SVG was exported; no unresolved blockers from the previous review. On fail: retry, max 2 retries.
- **Memory:** visual review record at `loops/drawio-diagram-loop/review.md`. Read first: blockers left open in the last visual review.

## Steps

1. **Pick the route.** Identify the diagram type and load only the references for that route.
2. **Normalize to YAML.** Turn text, Mermaid, CSV or an imported .drawio into the canonical YAML spec.
3. **Validate and render.** Run node scripts/cli.js with --validate to write the .drawio and the image.
4. **Inspect the export.** Look at the exported PNG, or the SVG fallback, for overlaps and label problems.
5. **Fix and rerun.** Patch the YAML when validation or the visual check fails, then render again.
6. **Report.** List deliverables, commands run, the image checked and any missing exporters.

Stop rule: Stops after 3 diagrams or 2 rework rounds per diagram.

## Permissions

- Writes: .drawio-tmp/**, loops/drawio-diagram-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/drawio-diagram-loop/review.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: diagram spec changed. Verification: validator and export check. Memory: loops/drawio-diagram-loop/review.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
