---
name: home-assistant-best-practices
title: Home Assistant Best Practices skill
repo: homeassistant-ai/skills
license: MIT
url: https://gethabit.dev/skills/homeassistant-ai/home-assistant-best-practices
---

# Home Assistant Best Practices skill

Home assistant best practices steers an agent toward native Home Assistant triggers, conditions and helpers instead of templates, safe entity renames, correct automation modes and careful backups. For anyone who builds Home Assistant automations with an agent.

- Install the skill: `npx skills add homeassistant-ai/skills --skill home-assistant-best-practices`
- Source: https://github.com/homeassistant-ai/skills/tree/HEAD/skills/home-assistant-best-practices
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You create or edit automations; You rename entities or devices; You plan a backup restore or upgrade.
Skip it when: You do not run Home Assistant; You only browse dashboards.

# Make it a habit: Automations use native Home Assistant features.

Each week your agent reviews new or changed Home Assistant automations against the skill's anti-pattern table: templates where native triggers fit, device_id instead of entity_id, wrong modes. It proposes fixes, waits for your OK, then checks the config.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Sunday evening (schedule; Claude Code routine or cron; `0 18 * * 0`)
- **Verification:** config check, your OK. Hard checks: the configuration check passes after the change; no device_id remains in reviewed triggers except allowed Zigbee2MQTT cases; no file under .storage/ was edited. On fail: notify, max 0 retries.
- **Memory:** review notes at `loops/home-assistant-review-loop/notes.md`. Read first: automations already reviewed and fixes still open.

## Steps

1. **Read the version.** Get version from GET /api/config or Settings, About, since features depend on the release.
2. **Gate refactors.** For renames or restructures, follow the safe-refactoring reference before any change.
3. **Check triggers.** Prefer purpose-specific triggers, then generic native ones, before any template.
4. **Check helpers and mode.** Swap template sensors for built-in helpers and pick the right automation mode.
5. **Propose fixes.** Show the user each exact change and wait for their OK before saving.
6. **Apply and check.** Save through the config API or UI, then run the configuration check and reload.
7. **Note the review.** Record which automations were fixed and which wait.

Stop rule: Stops after five automations per run; backups, restores and upgrades always need a fresh yes.

## Permissions

- Writes: automations.yaml, loops/home-assistant-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/home-assistant-review-loop/notes.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Sunday evening. Verification: config check, your OK. Memory: loops/home-assistant-review-loop/notes.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
