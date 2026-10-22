---
name: ziniao-account
title: Ziniao Account skill
repo: ziniao-open/skills
license: MIT
url: https://gethabit.dev/skills/ziniao-open/ziniao-account
---

# Ziniao Account skill

Ziniao account lets an agent manage Ziniao store accounts: list, create, update and delete stores, grant or revoke staff access, and manage store tags through ziniao-cli. For e-commerce teams running many stores in the Ziniao browser.

- Install the skill: `npx skills add ziniao-open/skills --skill ziniao-account`
- Source: https://github.com/ziniao-open/skills/tree/HEAD/skills/ziniao-account
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You list or create store accounts; You grant staff access to stores; You tag stores in bulk.
Skip it when: You want to open a store browser window; You manage employees, not stores.

# Make it a habit: Store access and tags stay clean.

Each week your agent lists Ziniao store accounts, their authorized staff and their tags with ziniao-cli account commands. It reports stores without tags and access changes since last week, and runs any fix only after you approve it.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly store access audit (schedule; Claude Code routine; `0 9 * * 1`)
- **Verification:** listing check + approval. Hard checks: account list --page-all returns more than zero stores; auth-users runs for every listed store; no high-risk command runs without your approval. On fail: notify, max 1 retries.
- **Memory:** store access snapshot at `loops/ziniao-store-auth-audit-loop/log.md`. Read first: last week's store list, staff grants and tags.

## Steps

1. **Read shared rules.** Read ../ziniao-shared/SKILL.md and the references file of each shortcut before running it.
2. **Check account type.** Use ziniao-cli config show to confirm the isBoss field, since member accounts cannot run account list.
3. **List stores.** Run ziniao-cli account list --page-all to get every store account.
4. **List grants and tags.** Run account auth-users and account tag-of-store for each store.
5. **Report changes.** Compare with last week and list new grants, removed grants and untagged stores.
6. **Apply approved fixes.** Run auth-remove, tag-bind or other changes only after you approve each one.

Stop rule: Stops after one full listing and at most 10 approved fixes per run.

## Permissions

- Writes: loops/ziniao-store-auth-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ziniao-store-auth-audit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly store access audit. Verification: listing check + approval. Memory: loops/ziniao-store-auth-audit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
