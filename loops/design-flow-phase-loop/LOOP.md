---
name: design-flow
title: Design Flow skill
repo: julianoczkowski/designer-skills
license: Apache-2.0
url: https://gethabit.dev/skills/julianoczkowski/design-flow
---

# Design Flow skill

The design flow skill runs the full design-to-build workflow as a guided sequence: grilling, design brief, information architecture, design tokens, task planning and frontend build, with review on request. For designers building features end to end.

- Install the skill: `npx skills add julianoczkowski/designer-skills --skill design-flow`
- Source: https://github.com/julianoczkowski/designer-skills/tree/HEAD/design-flow
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You start a project from scratch; You want the full design process; You resume a paused design flow.
Skip it when: You only need one small component tweak; You already have a finished brief and tasks.

# Make it a habit: Takes features from idea to UI.

For each new feature, your agent walks you through grill-me, design-brief, information-architecture, design-tokens, brief-to-tasks and frontend-design in order, confirms each phase before the next, and saves every output under .design/<feature-slug>/.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you start a feature (manual; Claude Code routine; `user asks to run the full design flow for a new project or feature`)
- **Verification:** phase files and approval. Hard checks: DESIGN_BRIEF.md exists after phase 2; INFORMATION_ARCHITECTURE.md exists unless skipped; TASKS.md exists after phase 5; you confirmed each phase before the next. On fail: stop, max 0 retries.
- **Memory:** design folder per feature at `.design/<feature-slug>/`. Read first: existing phase files to resume from.

## Steps

1. **Show the sequence.** Your agent lists phases 1-6 and asks which to skip.
2. **Clarify and brief.** It runs grill-me, then design-brief to write DESIGN_BRIEF.md.
3. **Structure and tokens.** It runs information-architecture and design-tokens, carrying the brief's choices forward.
4. **Plan the build.** It runs brief-to-tasks to write TASKS.md.
5. **Build task by task.** It runs frontend-design, checking off each task and confirming with you.
6. **Review on request.** Only when you ask, it runs design-review to write DESIGN_REVIEW.md with screenshots.

Stop rule: Stops after one phase per confirmation; you can stop at any phase.

## Permissions

- Writes: .design/**, src/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.design/<feature-slug>/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you start a feature. Verification: phase files and approval. Memory: .design/<feature-slug>/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
