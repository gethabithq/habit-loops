---
name: genshijin-compress
title: Genshijin Compress skill
repo: interfacex-co-jp/genshijin
license: MIT
url: https://gethabit.dev/skills/interfacex-co-jp/genshijin-compress
---

# Genshijin Compress skill

The genshijin compress skill shrinks natural-language memory files such as CLAUDE.md and todo lists into a terse caveman style to save input tokens, while it keeps code, URLs, paths and structure. For people with long agent memory files.

- Install the skill: `npx skills add interfacex-co-jp/genshijin --skill genshijin-compress`
- Source: https://github.com/interfacex-co-jp/genshijin/tree/HEAD/skills/genshijin-compress
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: your CLAUDE.md has grown long; you want fewer input tokens per run; your notes are full of polite filler.
Skip it when: the file is code or config; the file holds secrets or keys.

# Make it a habit: Smaller memory files, same facts.

When you name a memory file such as CLAUDE.md, your agent runs genshijin compress: it backs the file up as FILE.original.md, rewrites the prose in terse form and keeps code, URLs, paths and headings intact. The built-in validation checks the result. A run log keeps which files were done.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you name a file (manual; Claude Code routine; `/genshijin-compress <filepath>`)
- **Verification:** output validation passes. Hard checks: the skill's output validation passes; FILE.original.md backup exists before overwrite; every fenced code block matches the original exactly; heading count is the same as in the original. On fail: retry, max 2 retries.
- **Memory:** compressed files log at `loops/genshijin-compress-loop/log.md`. Read first: files already compressed, so .original.md copies are skipped.

## Steps

1. **Check the file.** The agent refuses code files and secret files like .env, keys or anything under .ssh.
2. **Back it up.** The readable version is saved as FILE.original.md before anything changes.
3. **Compress the prose.** The CLI from the scripts folder drops polite filler and hedges, but leaves code, URLs, paths and numbers alone.
4. **Validate.** The output check runs; on errors only the broken parts are fixed, up to 2 times.
5. **Report.** You get the result, or an error report with the original file left unchanged.
6. **Log the run.** The file name and outcome go into the run log.

Stop rule: Stops after one file per run, with at most 2 fix retries.

## Permissions

- Writes: <target file>, <target file>.original.md, loops/genshijin-compress-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/genshijin-compress-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you name a file. Verification: output validation passes. Memory: loops/genshijin-compress-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
