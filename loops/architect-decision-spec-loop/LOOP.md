---
name: architect
title: Architect skill
repo: jsmastery-pro/skills
license: MIT
url: https://gethabit.dev/skills/jsmastery-pro/architect
---

# Architect skill

The architect skill runs structured discovery for a technical decision, recommends an answer with a runner up, and writes a build spec in docs/specs/ for features, stacks, enhancements or codebase standards. For developers who want decisions written down.

- Install the skill: `npx skills add jsmastery-pro/skills --skill architect`
- Source: https://github.com/jsmastery-pro/skills/tree/HEAD/skills/architect
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You pick between approaches; You design a feature or page; You choose a tech stack.
Skip it when: The decision is trivial; You want code written now.

# Make it a habit: Turn open decisions into build specs.

When a load bearing decision is open, your agent asks the questions only you can answer, recommends a pick with a runner up, writes a numbered spec in docs/specs/ and offers a read only cross check. Specs and their status lines keep the record.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** decision owed or Assumed (event; Claude Code routine; `/develop records an Assumed spec, or you run /architect <topic>`)
- **Verification:** you confirm the spec. Hard checks: spec file exists in docs/specs/ with the next free NNNN; spec has Requirements, Decision and Build plan sections; no spec left in Assumed status after a ratify run. On fail: notify, max 0 retries.
- **Memory:** spec folder at `docs/specs/`. Read first: titles of existing specs and any Assumed spec for the topic.

## Steps

1. **Pre-flight.** Your agent checks git freshness, resolves the spec folder, lists specs and reads AGENTS.md and the scope row.
2. **Check overlap.** It asks whether to create, update or supersede if a spec already overlaps.
3. **Design conversation.** It reads internal/design-conversation.md and asks only what you alone know.
4. **Recommend.** It states a pick, a one line reason and a runner up for each choice.
5. **Write the spec.** It reads agent-prompt.md, spec-template.md and the mode file, then writes the spec.
6. **Cross check.** It asks if you want a read only review of the drafted spec.
7. **Confirm and link.** You confirm, and it follows internal/after-subagent.md to update status and the scope row.

Stop rule: Stops after one decision spec per run.

## Permissions

- Writes: docs/specs/**, docs/scope/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`docs/specs/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: decision owed or Assumed. Verification: you confirm the spec. Memory: docs/specs/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
