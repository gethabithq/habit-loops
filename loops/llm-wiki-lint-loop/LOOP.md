---
name: karpathy-llm-wiki
title: LLM wiki skill
repo: astro-han/karpathy-llm-wiki
license: MIT
url: https://gethabit.dev/skills/astro-han/karpathy-llm-wiki
---

# LLM wiki skill

The llm wiki skill builds and maintains a personal knowledge base: it ingests sources into raw/, compiles grounded articles into wiki/, answers questions from it and lints its quality, for researchers and note takers.

- Install the skill: `npx skills add astro-han/karpathy-llm-wiki --skill karpathy-llm-wiki`
- Source: https://github.com/astro-han/karpathy-llm-wiki
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: adding a source to your wiki; asking what you know about a topic; checking wiki quality.
Skip it when: a quick one-off answer; team docs with many editors.

# Make it a habit: Your wiki stays grounded.

Runs weekly on your personal wiki. Your agent fixes index and link problems, runs check_evidence.py to confirm facts still match the raw sources, reports contradictions, and appends the result to wiki/log.md.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly wiki lint (schedule; Claude Code routine or cron; `0 18 * * 0`)
- **Verification:** evidence script passes. Hard checks: scripts/check_evidence.py reports no evidence errors; every index entry points to an existing file; every Raw link resolves inside raw/; lint entry appended to wiki/log.md. On fail: notify, max 0 retries.
- **Memory:** wiki operation log at `wiki/log.md`. Read first: recent ingests and the last lint result.

## Steps

1. **Check structure.** Confirm raw/ and wiki/ exist, otherwise ask for an ingest first.
2. **Fix the index.** Add missing files to wiki/index.md and mark entries for deleted files as [MISSING].
3. **Fix links.** Repair internal, Raw and See Also links when exactly one match exists.
4. **Run evidence check.** Run python3 scripts/check_evidence.py on the project root and judge each suspect.
5. **Report judgment issues.** List contradictions, outdated claims, orphan pages and missing cross-references without fixing them.
6. **Log the run.** Append the issue count and auto-fix count to wiki/log.md.

Stop rule: Stops after one lint pass over the whole wiki per run.

## Permissions

- Writes: wiki/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`wiki/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly wiki lint. Verification: evidence script passes. Memory: wiki/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
