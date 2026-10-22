---
name: okx-cex-portfolio
title: OKX CEX Portfolio skill
repo: okx/agent-skills
license: MIT
url: https://gethabit.dev/skills/okx/okx-cex-portfolio
---

# OKX CEX Portfolio skill

The okx cex portfolio skill lets an agent read OKX account balances, open and closed positions, bills and fee tiers through the okx CLI, and move funds between funding and trading accounts after confirmation. For OKX traders.

- Install the skill: `npx skills add okx/agent-skills --skill okx-cex-portfolio`
- Source: https://github.com/okx/agent-skills/tree/HEAD/skills/okx-cex-portfolio
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a full balance overview; You need position PnL or bills; You must move funds before a trade.
Skip it when: You need market prices; You want to place or cancel orders.

# Make it a habit: Know your exchange balances daily.

Each morning your agent checks OKX credentials, asks live or demo if unclear, then takes a read-only snapshot with okx account balance-all, open positions and closed PnL. It flags partial failures and keeps a dated log for comparison.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning at seven (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** snapshot complete, mode tagged. Hard checks: okx config show --json or okx auth status --json shows a usable login; balance-all returns meta.partialFailure false; every result carries a [mode: live] or [mode: demo] tag; no write command (transfer, set-position-mode) ran. On fail: notify, max 1 retries.
- **Memory:** dated snapshot log at `loops/okx-portfolio-snapshot-loop/log.md`. Read first: the last snapshot totals and the mode used.

## Steps

1. **Check login.** Run okx config show --json and okx auth status --json to find API key or OAuth mode, and stop if not logged in.
2. **Confirm mode.** Reuse the mode from the log, or ask you once whether to read live or demo funds.
3. **Take snapshot.** Run okx account balance-all for trading, funding and valuation in one call.
4. **Read positions.** Run okx account positions and okx account positions-history for open trades and realized PnL.
5. **Compare.** Set today's totals next to the last logged snapshot and note big changes.
6. **Log and tag.** Append the snapshot with its mode tag to the run log and flag any partial failure.

Stop rule: One snapshot per run, read commands only, at most one retry after an error.

## Permissions

- Writes: loops/okx-portfolio-snapshot-loop/
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/okx-portfolio-snapshot-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning at seven. Verification: snapshot complete, mode tagged. Memory: loops/okx-portfolio-snapshot-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
