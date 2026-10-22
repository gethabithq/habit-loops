---
name: wiki-lint
title: Wiki Lint skill
repo: ar9av/obsidian-wiki
license: MIT
url: https://gethabit.dev/skills/ar9av/wiki-lint
---

# Wiki Lint skill

Wiki Lint audits an Obsidian wiki for broken links, orphans, stale content, frontmatter and lifecycle problems, reports them, and in consolidate mode applies safe fixes. For people maintaining an LLM-built Obsidian wiki.

- Install the skill: `npx skills add ar9av/obsidian-wiki --skill wiki-lint`
- Source: https://github.com/ar9av/obsidian-wiki/tree/HEAD/.skills/wiki-lint
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: checking wiki health; finding broken links and orphan pages; catching stale or mis-tagged pages.
Skip it when: you want to merge duplicate pages; you have no Obsidian wiki.

# Make it a habit: Your wiki stays linked and current.

On a schedule, your agent audits the Obsidian wiki for broken links, orphans, stale pages, bad frontmatter and lifecycle issues, and writes a health report. In consolidate mode it fixes safe issues after your yes. It logs each run to log.md.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly health check (schedule; cron; `0 8 * * 1`)
- **Verification:** report and safe fixes. Hard checks: broken wikilinks point to no existing page, count reported; orphan pages with zero incoming links are listed; the LINT line is appended to log.md. On fail: notify, max 0 retries.
- **Memory:** lint log at `log.md`. Read first: index.md for the page inventory and log.md for recent activity.

## Steps

1. **Resolve schema.** Your agent resolves the config, reads any AGENTS.md owner rules and forms the effective schema.
2. **Scan cheaply.** It uses frontmatter greps and section reads, preferring obsidian-wiki lint --json when the CLI is there.
3. **Run checks.** It runs the checks in order: orphans, broken links, frontmatter, stale, contradictions and lifecycle.
4. **Report.** It writes the Wiki Health Report with a count per issue type.
5. **Consolidate.** In consolidate mode it dry-runs the safe fixes and applies only those you confirm, never merging pages.
6. **Log.** It appends one LINT line to log.md with the issue counts.

Stop rule: Stops after one full audit per run; writes only in consolidate mode after your confirmation.

## Permissions

- Writes: log.md, wiki pages in consolidate mode after confirmation, synthesis/consolidation-<date>.md
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly health check. Verification: report and safe fixes. Memory: log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
