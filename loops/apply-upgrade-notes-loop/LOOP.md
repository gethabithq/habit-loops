---
name: om-apply-upgrade-notes
title: Apply Upgrade Notes skill
repo: open-mercato/skills
license: MIT
url: https://gethabit.dev/skills/open-mercato/om-apply-upgrade-notes
---

# Apply Upgrade Notes skill

The Apply Upgrade Notes skill (om-apply-upgrade-notes) re-syncs installed tracker and browser descriptors under .ai/ after a skills upgrade, preserving local edits, reporting custom-provider gaps and checking config. For teams running the open-mercato agent pipeline.

- Install the skill: `npx skills add open-mercato/skills --skill om-apply-upgrade-notes`
- Source: https://github.com/open-mercato/skills/tree/HEAD/skills/om-apply-upgrade-notes
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: after upgrading the skills collection; re-syncing installed pipeline descriptors; checking for stale pipeline artifacts.
Skip it when: no agent pipeline is installed; nothing was upgraded.

# Make it a habit: Installed pipeline artifacts stay current.

After a skills upgrade, your agent reads UPGRADE_NOTES.md, re-syncs the installed tracker and browser descriptors under .ai/ while keeping local edits, reports custom-provider gaps and checks the config. It leaves changes uncommitted for review.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** after skills upgrade (event; Claude Code routine; `skills collection upgraded`)
- **Verification:** descriptors synced, config parses. Hard checks: each descriptor still has every operation the installed skills name; the browser provider resolves to an existing descriptor; the config parses with jq; a second run reports already current and changes nothing. On fail: notify, max 1 retries.
- **Memory:** agentic config at `.ai/agentic.config.json`. Read first: the config's tracker and browser.provider keys and installed descriptors.

## Steps

1. **Agentic setup.** Your agent loads .ai/agentic.config.json and the override contract; no config means nothing to upgrade.
2. **Locate sources.** It finds the shipped descriptors next to the skill and resolves UPGRADE_NOTES.md.
3. **Diff tracker.** It compares the installed tracker descriptor operation by operation and classifies each difference.
4. **Diff browser.** It applies the same diff to the browser-provider descriptor, defaulting a missing provider to playwright.
5. **Walk the log.** It checks each UPGRADE_NOTES entry against this repo and adds missing config keys additively.
6. **Apply and report.** It applies approved changes or dry-runs them, sanity-checks the result and reports what changed, uncommitted.

Stop rule: Stops after one upgrade sync per run; conflicting changes wait for your answer.

## Permissions

- Writes: .ai/trackers/*.md, .ai/browsers/*.md, .ai/agentic.config.json
- Network: raw.githubusercontent.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.ai/agentic.config.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: after skills upgrade. Verification: descriptors synced, config parses. Memory: .ai/agentic.config.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
