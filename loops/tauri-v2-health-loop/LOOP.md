---
name: tauri-v2
title: Tauri v2 skill
repo: nodnarbnitram/claude-code-extensions
license: MIT
url: https://gethabit.dev/skills/nodnarbnitram/tauri-v2
---

# Tauri v2 skill

Tauri v2 helps you build cross-platform desktop and mobile apps with a Rust backend: commands, IPC with invoke, emit and channels, capabilities and permissions, config and troubleshooting. For developers starting or fixing Tauri v2 apps.

- Install the skill: `npx skills add nodnarbnitram/claude-code-extensions --skill tauri-v2`
- Source: https://github.com/nodnarbnitram/claude-code-extensions/tree/HEAD/.claude/skills/tauri-v2
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: adding a Rust command; a permission denied error; setting up tauri.conf.json.
Skip it when: you use Tauri v1; you build a pure web app.

# Make it a habit: Tauri commands and permissions stay wired.

When src-tauri changes, your agent runs the setup checklist: npx tauri info shows v2, capabilities/default.json has core:default, every command is in generate_handler, and logic lives in lib.rs. It logs each problem found and fixed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** src-tauri changed (event; GitHub Actions or Claude Code routine; `push touching src-tauri/**`)
- **Verification:** setup checklist passes. Hard checks: npx tauri info shows Tauri v2 versions; src-tauri/capabilities/default.json contains core:default; every #[tauri::command] is listed in generate_handler!; build passes. On fail: retry, max 2 retries.
- **Memory:** fix log at `loops/tauri-v2-health-loop/log.md`. Read first: issues found last run and how they were fixed.

## Steps

1. **Check versions.** Run npx tauri info and confirm v2 packages.
2. **Check capabilities.** Make sure capabilities/default.json has core:default and each plugin's permission string.
3. **Check commands.** Confirm every command is in generate_handler! and async commands use owned types.
4. **Check structure.** Keep main.rs thin and all logic in lib.rs with the mobile entry point.
5. **Check config.** Confirm devUrl matches the dev server and beforeDevCommand runs it.
6. **Build and log.** Build the app, fix what fails and log each fix.

Stop rule: Stops after one pass over the project, with at most two build retries.

## Permissions

- Writes: src-tauri/**, loops/tauri-v2-health-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/tauri-v2-health-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: src-tauri changed. Verification: setup checklist passes. Memory: loops/tauri-v2-health-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
