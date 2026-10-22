---
name: okx-cex-skill-mp
title: OKX skills marketplace skill
repo: okx/agent-skills
license: MIT
url: https://gethabit.dev/skills/okx/okx-cex-skill-mp
---

# OKX skills marketplace skill

The okx skills marketplace skill searches, installs, updates, removes and verifies AI trading skills from the OKX marketplace with the okx CLI, for traders who extend their assistant.

- Install the skill: `npx skills add okx/agent-skills --skill okx-cex-skill-mp`
- Source: https://github.com/okx/agent-skills/tree/HEAD/skills/okx-cex-skill-mp
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: finding a trading skill; checking for skill updates; verifying a skill signature.
Skip it when: placing orders; reading market data.

# Make it a habit: Installed skills stay verified.

Runs weekly. Your agent lists installed marketplace skills with okx skill list, re-verifies each signature with okx skill verify, checks for updates with okx skill check, and notes failures in the run log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly skill check (schedule; Claude Code routine or cron; `0 9 * * 1`)
- **Verification:** signatures verified. Hard checks: okx skill verify exits 0 for each skill; no skill shows status bypassed in registry.json; okx skill list returns at least one skill. On fail: notify, max 1 retries.
- **Memory:** skill registry at `~/.okx/skills/registry.json`. Read first: installed skills and their verification status.

## Steps

1. **List skills.** Run okx skill list to see what is installed.
2. **Verify each.** Run okx skill verify for every installed skill and note failures.
3. **Check updates.** Run okx skill check for each skill and list newer versions.
4. **Ask before updating.** Show available updates and ask you before running okx skill add.
5. **Report.** Summarize verified, failed and updatable skills.

Stop rule: Stops after checking 20 installed skills per run.

## Permissions

- Writes: ~/.okx/skills/registry.json
- Network: www.okx.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`~/.okx/skills/registry.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly skill check. Verification: signatures verified. Memory: ~/.okx/skills/registry.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
