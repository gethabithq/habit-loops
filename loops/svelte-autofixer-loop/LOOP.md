---
name: svelte-code-writer
title: Svelte code writer skill
repo: sveltejs/ai-tools
license: MIT
url: https://gethabit.dev/skills/sveltejs/svelte-code-writer
---

# Svelte code writer skill

The svelte code writer skill gives your agent the @sveltejs/mcp CLI to look up Svelte 5 and SvelteKit docs and run the svelte-autofixer on components, for developers who write or review Svelte code.

- Install the skill: `npx skills add sveltejs/ai-tools --skill svelte-code-writer`
- Source: https://github.com/sveltejs/ai-tools/tree/HEAD/tools/skills/svelte-code-writer
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You create or edit a Svelte component; You are unsure about runes syntax; You review Svelte code before merge.
Skip it when: Your project does not use Svelte; You only change plain JavaScript files.

# Make it a habit: Ship Svelte components the autofixer accepts.

When a pull request changes .svelte or .svelte.ts files, your agent runs svelte-autofixer on each one with the project's Svelte version, looks up unclear syntax in the docs and fixes the issues. A log keeps the files and the issues found.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Svelte files changed (event; GitHub Actions or Claude Code routine; `pull_request with changes in **/*.svelte, **/*.svelte.ts or **/*.svelte.js`)
- **Verification:** autofixer finds no issues. Hard checks: svelte-autofixer reports no issues for every changed file; --svelte-version matches the version in package.json; the count of checked files equals the count of changed Svelte files. On fail: retry, max 2 retries.
- **Memory:** autofixer issue log at `loops/svelte-autofixer-loop/log.md`. Read first: issues that came back in earlier runs.

## Steps

1. **List changed files.** The agent collects the changed .svelte, .svelte.ts and .svelte.js files, ideally inside the svelte-file-editor subagent.
2. **Read the version.** It takes the full Svelte version from package.json for the --svelte-version option.
3. **Look up docs.** If syntax is unclear, it runs list-sections and then get-documentation for the topics it needs.
4. **Run the autofixer.** npx @sveltejs/mcp svelte-autofixer checks each file, with --async when the project uses async mode.
5. **Fix and recheck.** The agent applies the fixes and runs the autofixer again until no issue is left.
6. **Log the issues.** Each file and its issues go into the log.

Stop rule: Stops when every changed Svelte file passes, or after two fix retries per file.

## Permissions

- Writes: **/*.svelte, **/*.svelte.ts, **/*.svelte.js, loops/svelte-autofixer-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/svelte-autofixer-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Svelte files changed. Verification: autofixer finds no issues. Memory: loops/svelte-autofixer-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
