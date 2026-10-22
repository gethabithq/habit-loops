---
name: documentation-update
title: Documentation Update skill
repo: geoffjay/claude-plugins
license: MIT
url: https://gethabit.dev/skills/geoffjay/documentation-update
---

# Documentation Update skill

Documentation update is a skill for plugin marketplace maintainers that regenerates agents.md, agent-skills.md, plugins.md and usage.md from marketplace.json with Jinja templates whenever plugins change.

- Install the skill: `npx skills add geoffjay/claude-plugins --skill documentation-update`
- Source: https://github.com/geoffjay/claude-plugins/tree/HEAD/plugins/claude-plugin/skills/documentation-update
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add a plugin to the marketplace; You update a plugin's agents; Docs no longer match the catalog.
Skip it when: You have no marketplace.json; You write docs by hand.

# Make it a habit: Plugin docs match the marketplace.

Whenever marketplace.json changes, your agent runs doc_generator.py to rebuild agents.md, agent-skills.md, plugins.md and usage.md from the Jinja templates, checks the result and stages the docs with the plugin change.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** marketplace.json changes (event; GitHub Actions or Claude Code routine; `push touching .claude-plugin/marketplace.json`)
- **Verification:** generator runs clean. Hard checks: python doc_generator.py exits 0; all four docs files exist in docs/; no template rendering errors are printed. On fail: retry, max 1 retries.
- **Memory:** docs commit history at `docs/`. Read first: the last generated docs and plugin stats.

## Steps

1. **Validate first.** Run marketplace validation and fix errors before generating.
2. **Dry run.** Run python doc_generator.py --dry-run to preview the output.
3. **Generate.** Run python doc_generator.py to write the docs into docs/.
4. **Review output.** Check links, formatting and stats against the marketplace.
5. **Stage changes.** Commit the docs together with the plugin change.

Stop rule: Stops after one regeneration per change, with one retry.

## Permissions

- Writes: docs/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`docs/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: marketplace.json changes. Verification: generator runs clean. Memory: docs/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
