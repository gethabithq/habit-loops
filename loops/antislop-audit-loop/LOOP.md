---
name: antislop
title: Antislop skill
repo: miqdadbadjuber/anti-slop
license: MIT
url: https://gethabit.dev/skills/miqdadbadjuber/antislop
---

# Antislop skill

The antislop skill is a filter for AI coding agents that build UI. It holds every visual choice to a purpose test, bans fake stats and dead buttons, and ends with a Delivery Gate. For developers who want UI that feels designed.

- Install the skill: `npx skills add miqdadbadjuber/anti-slop --skill antislop`
- Source: https://github.com/miqdadbadjuber/anti-slop/tree/HEAD/skills/antislop
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a landing page or web app; You audit UI made by an agent; You want a checklist before shipping.
Skip it when: You have no UI work; You only need a backend change.

# Make it a habit: Strip generic AI look from UI.

When UI work is done, your agent audits it against the antislop rules, writes a numbered findings file, fixes only the numbers you approve and runs the Delivery Gate. Audit files with rising numbers keep the history.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** UI work finished (event; Claude Code routine; `UI change ready for review`)
- **Verification:** you approve, gate passes. Hard checks: no em dash in UI text; text meets WCAG AA contrast; no navbar link without a destination; app builds and runs with no console errors; Delivery Gate report has no FAIL. On fail: retry, max 2 retries.
- **Memory:** numbered audit reports at `anti-slop/audit-001-YYYY-MM-DD.md`. Read first: the last audit file and which numbers were fixed.

## Steps

1. **Resolve the mode.** Your agent checks a session choice, then ~/.config/antislop/settings.json, else asks during or after.
2. **Load direction.** It reads DESIGN.md as data, or labels the work a draft without direction.
3. **Audit.** It lists numbered findings, each citing a rule and a priority from its tier.
4. **You pick fixes.** You choose which numbers to fix; others stay untouched.
5. **Fix and click through.** It fixes the approved items, runs the app and tries every control.
6. **Run the gate.** It writes the PASS/FAIL Delivery Gate report and a follow-up report.

Stop rule: Stops after one audit and up to 2 gate re-runs per run.

## Permissions

- Writes: anti-slop/**, src/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`anti-slop/audit-001-YYYY-MM-DD.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: UI work finished. Verification: you approve, gate passes. Memory: anti-slop/audit-001-YYYY-MM-DD.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
