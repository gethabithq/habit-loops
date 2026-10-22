---
name: wiki-status
title: Wiki Status skill
repo: ar9av/obsidian-wiki
license: MIT
url: https://gethabit.dev/skills/ar9av/wiki-status
---

# Wiki Status skill

Wiki Status reports an Obsidian wiki's ingestion state: the new, modified and deleted source delta, a token footprint, a ranked next-steps list and optional structural insights. For people maintaining an LLM-built wiki.

- Install the skill: `npx skills add ar9av/obsidian-wiki --skill wiki-status`
- Source: https://github.com/ar9av/obsidian-wiki/tree/HEAD/.skills/wiki-status
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: checking what is left to ingest; seeing the delta since last ingest; finding the wiki's hubs and bridges.
Skip it when: the vault has almost no pages; you want to ingest rather than audit.

# Make it a habit: Always know what the wiki needs.

On a schedule, your agent reads the manifest, scans sources, computes the new, modified and deleted delta, and writes a ranked What to Do Next list with a token footprint. It appends a status line to the vault log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly status check (schedule; cron; `0 8 * * 1`)
- **Verification:** delta and next steps. Hard checks: the manifest at .manifest.json is read; the delta lists new, modified and deleted sources with counts; a ranked What to Do Next list is produced. On fail: notify, max 0 retries.
- **Memory:** ingest manifest at `.manifest.json`. Read first: the manifest's ingested sources and last_updated time.

## Steps

1. **Resolve config.** Your agent resolves the vault path and source directories and reads .manifest.json.
2. **Scan sources.** It inventories documents, Claude history and Codex history available to ingest right now.
3. **Compute delta.** It classifies each source as new, modified, touched, unchanged, deleted or unavailable.
4. **Report status.** It writes the overview, delta tables and an estimated token footprint.
5. **Rank next steps.** It gathers signals and renders the ranked What to Do Next list, capped at six items.
6. **Log.** It appends one status line to log.md.

Stop rule: Stops after one status pass per run; it only reads and reports, except _insights.md in insights mode.

## Permissions

- Writes: log.md, _insights.md in insights mode
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.manifest.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly status check. Verification: delta and next steps. Memory: .manifest.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
