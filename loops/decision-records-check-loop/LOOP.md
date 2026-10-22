---
name: decision-records
title: Decision Records skill
repo: skymavis/skills
license: MIT
url: https://gethabit.dev/skills/skymavis/decision-records
---

# Decision Records skill

The decision records skill drafts, promotes, archives and supersedes ADR-style records with the bundled decisions.py tool, and keeps INDEX.md and cross-links generated. For teams who record architecture, product or policy decisions in git.

- Install the skill: `npx skills add skymavis/skills --skill decision-records`
- Source: https://github.com/skymavis/skills/tree/HEAD/skills/decision-records
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You draft a new decision record; You supersede an old decision; You set up ADRs in a repo.
Skip it when: You keep decisions in a wiki; You need a one-off note.

# Make it a habit: Keep decision records valid and linked.

On every commit and pull request your agent runs decisions.py check, rebuilds INDEX.md with build --relink and flags cites of superseded records. Drafts are promoted only with your explicit go-ahead. Git history keeps the record.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** decision docs change (event; GitHub Actions or pre-commit hook; `pull request touches docs/decisions/`)
- **Verification:** check passes, you promote. Hard checks: python scripts/decisions.py check exits 0; INDEX.md is up to date after build; no accepted record references a draft. On fail: notify, max 1 retries.
- **Memory:** decision record history at `docs/decisions/INDEX.md`. Read first: INDEX.md and WARN lines from the last check.

## Steps

1. **Check.** Your agent runs python scripts/decisions.py check.
2. **Read warnings.** It reads WARN lines for ID collisions with origin/main and cites of superseded records.
3. **Rebuild.** It runs decisions.py build --relink to regenerate INDEX.md and links.
4. **Tidy drafts.** It checks drafts against drafts/_template.md and removes padding.
5. **Ask before promote.** It runs promote only after your explicit go-ahead in that turn.

Stop rule: Stops after one check and rebuild per run.

## Permissions

- Writes: docs/decisions/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`docs/decisions/INDEX.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: decision docs change. Verification: check passes, you promote. Memory: docs/decisions/INDEX.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
