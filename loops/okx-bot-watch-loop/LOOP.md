---
name: okx-cex-bot
title: OKX CEX Bot skill
repo: okx/agent-skills
license: MIT
url: https://gethabit.dev/skills/okx/okx-cex-bot
---

# OKX CEX Bot skill

The okx cex bot skill lets an agent create, stop, amend and monitor Grid, DCA Martingale and Smart Portfolio bots on OKX through the okx CLI, for traders who want bot control from chat.

- Install the skill: `npx skills add okx/agent-skills --skill okx-cex-bot`
- Source: https://github.com/okx/agent-skills/tree/HEAD/skills/okx-cex-bot
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You run Grid or DCA bots on OKX; You want daily bot P&L checks; You want to amend TP/SL from chat.
Skip it when: You place regular spot or swap orders; You only need market prices.

# Make it a habit: Your OKX bots, checked daily.

Each morning your agent lists your running Grid, DCA and Smart Portfolio bots on OKX with the okx CLI, reads details and P&L, and logs them. Any change you want, like a stop or amend, waits for your OK and is verified after.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; Claude Code routine or cron; `0 8 * * *`)
- **Verification:** list after every write. Hard checks: okx config show --json or okx auth status --json shows a valid login; after create the bot appears in the orders list; after amend details --algoId shows the new config; after stop the bot appears in orders --history. On fail: notify, max 0 retries.
- **Memory:** bot P&L log at `loops/okx-bot-watch-loop/log.md`. Read first: last run's bot list, algoIds and P&L.

## Steps

1. **Check login.** Run okx config show --json and okx auth status --json; if not logged in, hand over to the okx-cex-auth skill.
2. **Confirm mode.** Use live or demo as you set it, and ask once if it is not clear.
3. **List bots.** Run the orders commands for grid, dca and smart-portfolio to get each algoId.
4. **Read details.** Run details for each bot and note P&L and positions in the log.
5. **Propose changes.** Suggest a stop, amend or margin change and run it only after you confirm.
6. **Verify writes.** Run orders, details or orders --history to confirm each change took effect.

Stop rule: Stops after one pass over all running bots and at most 3 confirmed write commands per run.

## Permissions

- Writes: loops/okx-bot-watch-loop/**
- Network: www.okx.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/okx-bot-watch-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: list after every write. Memory: loops/okx-bot-watch-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
