---
name: obsidian-markdown
title: Obsidian Markdown skill
repo: kepano/obsidian-skills
license: MIT
url: https://gethabit.dev/skills/kepano/obsidian-markdown
---

# Obsidian Markdown skill

The obsidian markdown skill helps agents create and edit Obsidian Flavored Markdown with wikilinks, embeds, callouts, properties, tags, comments, math and Mermaid. For anyone keeping notes in an Obsidian vault.

- Install the skill: `npx skills add kepano/obsidian-skills --skill obsidian-markdown`
- Source: https://github.com/kepano/obsidian-skills/tree/HEAD/skills/obsidian-markdown
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write notes in Obsidian; You need wikilinks or embeds; You add callouts or frontmatter.
Skip it when: You write plain CommonMark only; Your notes live outside Obsidian.

# Make it a habit: New notes use clean Obsidian syntax.

Each evening your agent checks the notes you changed today: frontmatter properties, wikilinks for vault notes, embeds, callouts and tags. A hard check needs every wikilink to point to a note that exists. A run log keeps notes that still need a fix.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** evening note check (schedule; Claude Code routine or cron; `0 21 * * *`)
- **Verification:** links resolve, frontmatter present. Hard checks: every changed note has frontmatter; every [[wikilink]] target exists in the vault; tags do not start with a number. On fail: notify, max 0 retries.
- **Memory:** notes needing fixes at `loops/obsidian-note-tidy-loop/run-log.md`. Read first: notes flagged last time that are still broken.

## Steps

1. **Find changed notes.** List the .md files in the vault changed since the last run.
2. **Check frontmatter.** Make sure each note has properties such as title, tags and aliases at the top.
3. **Check links.** Use wikilinks for vault notes and Markdown links only for external URLs.
4. **Check syntax.** Check embeds, callouts with > [!type], block IDs and tags against the skill's syntax.
5. **Log the rest.** Write notes that still need a fix to the run log, to verify in reading view.

Stop rule: Stops after the notes changed today, at most 50 per run.

## Permissions

- Writes: changed notes in the vault, loops/obsidian-note-tidy-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/obsidian-note-tidy-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: evening note check. Verification: links resolve, frontmatter present. Memory: loops/obsidian-note-tidy-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
