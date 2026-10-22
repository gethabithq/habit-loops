---
name: cursor-memory-curator
title: Cursor Memory Curator skill
repo: stark-ai-de/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/stark-ai-de/cursor-memory-curator
---

# Cursor Memory Curator skill

The cursor memory curator skill audits Cursor project rules, .cursorrules, AGENTS.md and memory-bank context for stale, conflicting, ignored or sensitive guidance, then routes review, planning or backed-up cleanup.

- Install the skill: `npx skills add stark-ai-de/agent-skills --skill cursor-memory-curator`
- Source: https://github.com/stark-ai-de/agent-skills/tree/HEAD/skills/cursor-operations/cursor-memory-curator
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Cursor follows outdated rules; rule files conflict; you suspect secrets in rules.
Skip it when: you need Codex memory reviewed; you only edit ordinary docs.

# Make it a habit: Cursor rules stay current and safe.

Every month, and when rule files change, your agent runs a read-only review-file pass over your Cursor rules, .cursorrules and AGENTS.md. It flags stale, ignored or sensitive rules in one record, and the next run starts from that record's deferred work.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly Cursor rules review (schedule; Claude Code routine or cron; `0 9 1 * *`)
- **Verification:** complete redacted curation record. Hard checks: inventory script lists Cursor context files; risk scanner returns valid JSON; every atomic claim has one classification and a confidence; plain .md files under .cursor/rules are flagged; no rule file changed. On fail: stop, max 0 retries.
- **Memory:** curation record folder at `.agent-reports/cursor-memory-curation/`. Read first: the latest record's Deferred Work section.

## Steps

1. **Announce the route.** The agent names review-file as the selected route, the target paths and that nothing will be changed.
2. **Inventory context.** It runs node scripts/inventory-cursor-context.mjs --repo . without dumping file contents.
3. **Scan for risks.** It runs node scripts/scan-cursor-context-risks.mjs --repo . --json, where exit 1 means findings.
4. **Parse rule metadata.** It reads description, globs and alwaysApply in each .mdc file and flags plain .md rules as ignored.
5. **Classify claims.** Each atomic rule gets one label such as KEEP, MOVE TO AGENTS.md or DELETE, plus risk tags and confidence.
6. **Write the record.** It fills assets/review-report-template.md into one new redacted record and makes no cleanup.

Stop rule: Stops after one review record per run; cleanup needs your separate request.

## Permissions

- Writes: .agent-reports/cursor-memory-curation/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.agent-reports/cursor-memory-curation/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly Cursor rules review. Verification: complete redacted curation record. Memory: .agent-reports/cursor-memory-curation/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
