---
name: domain-context
title: Domain Context skill
repo: customware-ai/skills
license: MIT
url: https://gethabit.dev/skills/customware-ai/domain-context
---

# Domain Context skill

The domain context skill helps teams building business apps grow a living domain knowledge file, so the agent uses their terms, entities and business rules across sessions.

- Install the skill: `npx skills add customware-ai/skills --skill domain-context`
- Source: https://github.com/customware-ai/skills/tree/HEAD/skills/domain-context
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Your agent misreads business terms; Domain knowledge grows over time; You onboard new developers.
Skip it when: The project is a small one-off script; Your domain is fully documented elsewhere.

# Make it a habit: Your agent learns your business.

At the start of every session your agent reads .tasks/domain.md, flags unknown terms and unclear rules inline while it works, and ends with proposed domain updates. You approve them, and the next session reads the updated file.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every session start (event; Claude Code routine; `session starts in a project with .tasks/domain.md`)
- **Verification:** you approve updates. Hard checks: final response has a Proposed Domain Updates section; unknown terms are marked [UNKNOWN: term]; version number goes up by one minor step on each approved update. On fail: notify, max 0 retries.
- **Memory:** domain knowledge file at `.tasks/domain.md`. Read first: Tier 1 core context, then the Tier 2 files the task touches.

## Steps

1. **Read the domain.** Read .tasks/domain.md, or the index plus relevant Tier 2 files in split mode.
2. **Work with flags.** Use terms exactly as defined and mark unknowns, unclear relationships and inferred rules inline.
3. **Propose updates.** End with a Proposed Domain Updates section that names the target file for each change.
4. **You review.** You approve or edit the proposals and update the domain file.
5. **Version it.** On approval, raise the minor version, update the date and changes line, and add a changelog entry.
6. **Offer a split.** When the file passes about 200 lines, offer to split it into tiers.

Stop rule: Stops after one session's set of proposed updates.

## Permissions

- Writes: .tasks/domain.md, docs/domain/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.tasks/domain.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every session start. Verification: you approve updates. Memory: .tasks/domain.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
