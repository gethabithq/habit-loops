---
name: ziniao-access-policy
title: Ziniao Access Policy skill
repo: ziniao-open/skills
license: MIT
url: https://gethabit.dev/skills/ziniao-open/ziniao-access-policy
---

# Ziniao Access Policy skill

Ziniao access policy lets an agent query and maintain Ziniao web access rules, web pages and page groups, rule members and accounts, and account policy bindings through ziniao-cli api. For teams who manage ERP browser access in Ziniao.

- Install the skill: `npx skills add ziniao-open/skills --skill ziniao-access-policy`
- Source: https://github.com/ziniao-open/skills/tree/HEAD/skills/ziniao-access-policy
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You audit Ziniao access rules; You bind a policy to an account; You restrict downloads for a role.
Skip it when: You do not use Ziniao; You need shortcut commands, not raw API calls.

# Make it a habit: Access rules reviewed every week.

Each week your agent lists Ziniao access rules, web pages, page groups and the policies bound to key accounts through ziniao-cli api. It reports disabled rules and changes since last week, and any edit waits for your approval.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly access rule review (schedule; Claude Code routine; `0 9 * * 1`)
- **Verification:** API calls + your approval. Hard checks: every ziniao-cli api call returns a meta.requestId; the rule list count is above zero; no edit, delete or bind call runs without approval. On fail: notify, max 1 retries.
- **Memory:** rule snapshot log at `loops/ziniao-access-rule-review-loop/log.md`. Read first: last week's rule list, states and request IDs.

## Steps

1. **Read shared rules.** Read ../ziniao-shared/SKILL.md first, as the skill requires.
2. **List rules.** Call the access_rule/list endpoint with paging and fetch details for changed rules.
3. **List pages and groups.** Call the access_rule_url list and the group list with isAll true.
4. **Check accounts.** Call access_rule/list/one_account for each watched account.
5. **Report changes.** Compare with last week's snapshot and list disabled or new rules with their request IDs.
6. **Apply approved edits.** Run edit, active, change_user or bind calls only after you approve them.

Stop rule: Stops after one full listing and at most 5 approved edits per run.

## Permissions

- Writes: loops/ziniao-access-rule-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ziniao-access-rule-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly access rule review. Verification: API calls + your approval. Memory: loops/ziniao-access-rule-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
