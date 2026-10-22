---
name: drawio-diagrams
title: Draw.io Diagrams skill
repo: stark-ai-de/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/stark-ai-de/drawio-diagrams
---

# Draw.io Diagrams skill

The draw.io diagrams skill creates, edits, reviews and exports editable .drawio files such as architecture, flow, sequence and network diagrams, with design profiles, official icons, validators and light and dark support.

- Install the skill: `npx skills add stark-ai-de/agent-skills --skill drawio-diagrams`
- Source: https://github.com/stark-ai-de/agent-skills/tree/HEAD/plugins/stark-ai-developer/skills/drawio-diagrams
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: you need an editable architecture diagram; a .drawio file needs repair; you want a diagram review.
Skip it when: you need data charts; you want artistic images.

# Make it a habit: Diagrams stay valid and readable.

When a pull request changes .drawio files, your agent runs the read-only review workflow: XML preflight, lint and diagram rule checks, then a semantic and light/dark review. It logs findings so recurring layout problems are easy to spot.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes drawio files (event; GitHub Actions or Claude Code routine; `pull_request.opened or synchronize, *.drawio`)
- **Verification:** validators report no errors. Hard checks: scripts/preflight-drawio-xml.mjs passes; scripts/validate_drawio.py reports no ERROR; scripts/validate-drawio-diagram-rules.mjs reports no ERROR; every WARN is listed with a reason. On fail: notify, max 0 retries.
- **Memory:** diagram review log at `loops/drawio-diagram-review-loop/log.md`. Read first: warnings seen in earlier reviews per diagram.

## Steps

1. **Select review.** The agent announces the review workflow, which is strictly read-only.
2. **Build semantic model.** It reads each changed .drawio file and maps nodes, edges and labels.
3. **Run validators.** It runs preflight-drawio-xml.mjs, validate_drawio.py and validate-drawio-diagram-rules.mjs.
4. **Review readability.** It checks routing, floating edges, icon coverage and light and dark contrast.
5. **Report findings.** Findings and the suggested follow-up workflow go into a review comment and the log, with no fixes made.

Stop rule: Stops after 10 diagrams per run.

## Permissions

- Writes: loops/drawio-diagram-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/drawio-diagram-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes drawio files. Verification: validators report no errors. Memory: loops/drawio-diagram-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
