---
name: ponytail-debt
title: Ponytail Debt skill
repo: DietrichGebert/ponytail
license: MIT
url: https://gethabit.dev/skills/dietrichgebert/ponytail-debt
---

# Ponytail Debt skill

Ponytail debt collects every shortcut: comment in a repo into one debt ledger with its limit and upgrade trigger, and flags markers with no trigger. For developers who take deliberate shortcuts and want to track them.

- Install the skill: `npx skills add DietrichGebert/ponytail --skill ponytail-debt`
- Source: https://github.com/DietrichGebert/ponytail/tree/HEAD/.openclaw/skills/ponytail-debt
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You mark shortcuts with comments; You want one list of deferred work; You want to spot shortcuts with no plan.
Skip it when: Your repo has no marker comments; You want the shortcuts fixed for you.

# Make it a habit: No shortcut quietly becomes permanent.

Every week your agent runs ponytail-debt: it greps the repo for shortcut: comments, writes one ledger row per marker with its ceiling and upgrade trigger, and tags rows with no trigger. The ledger file keeps the count, so growth shows up.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly debt scan (schedule; Claude Code routine or GitHub Actions; `0 8 * * 5`)
- **Verification:** ledger matches grep. Hard checks: ledger row count equals the number of git grep hits kept; ledger ends with the <N> markers, <M> with no trigger. line; every row without an upgrade path carries the no-trigger tag. On fail: retry, max 1 retries.
- **Memory:** debt ledger file at `PONYTAIL-DEBT.md`. Read first: last week's marker count and no-trigger rows.

## Steps

1. **Read last ledger.** The agent opens PONYTAIL-DEBT.md and notes last week's totals.
2. **Grep for markers.** It runs git grep --no-index --exclude-standard for shortcut: and ponytail: comments.
3. **Drop non-deferrals.** It skips hits that only mention the word, like a note about a keyboard shortcut.
4. **Write ledger rows.** It writes one row per marker, grouped by file, with the ceiling and upgrade trigger.
5. **Flag rot risk.** It tags rows that name no upgrade path with no-trigger and writes the totals line.

Stop rule: Stops after one full repo scan per run.

## Permissions

- Writes: PONYTAIL-DEBT.md
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`PONYTAIL-DEBT.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly debt scan. Verification: ledger matches grep. Memory: PONYTAIL-DEBT.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
