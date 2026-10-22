---
name: codex-memory-curator
title: Codex Memory Curator skill
repo: stark-ai-de/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/stark-ai-de/codex-memory-curator
---

# Codex Memory Curator skill

The codex memory curator skill audits Codex memory for stale claims, cross-repo leaks, sensitive entries and config problems, then routes review, planning or backed-up cleanup for developers who rely on Codex.

- Install the skill: `npx skills add stark-ai-de/agent-skills --skill codex-memory-curator`
- Source: https://github.com/stark-ai-de/agent-skills/tree/HEAD/plugins/stark-ai-developer/skills/codex-memory-curator
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Codex memory feels stale or wrong; you suspect secrets in memory; memory leaks across repos.
Skip it when: you want to edit repo docs; you need Cursor memory reviewed.

# Make it a habit: Codex memory stays true and safe.

Every month your agent runs a read-only review of Codex memory with the review-file route: inventory, redacted risk scan, one classification per claim. It writes one curation record, and the next run starts from the last record's deferred work.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly memory review (schedule; Claude Code routine or cron; `0 9 1 * *`)
- **Verification:** complete redacted curation record. Hard checks: inventory script runs and lists memory files; risk scanner returns valid JSON; every atomic claim has one classification and a confidence; no full secret printed in the record; no memory or config file changed. On fail: stop, max 0 retries.
- **Memory:** curation record folder at `.agent-reports/codex-memory-curation/`. Read first: the latest record's Deferred Work section.

## Steps

1. **Announce the route.** The agent states review-file as the selected route, the Codex home and that nothing will be changed.
2. **Inventory memory.** It runs node scripts/inventory-memories.mjs to list memory files without dumping them.
3. **Scan for risks.** It runs node scripts/scan-memory-risks.mjs --json, where exit code 1 means findings, not failure.
4. **Classify claims.** Each atomic claim gets one label such as KEEP, DELETE or MOVE TO AGENTS.md, with risk tags and confidence.
5. **Check conflicts.** Disputed claims are checked against only the repo files needed, since current files beat stored memory.
6. **Write the record.** It fills assets/review-report-template.md into one new redacted record and makes no cleanup.

Stop rule: Stops after one review record per run; cleanup always needs a separate request.

## Permissions

- Writes: .agent-reports/codex-memory-curation/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.agent-reports/codex-memory-curation/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly memory review. Verification: complete redacted curation record. Memory: .agent-reports/codex-memory-curation/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
