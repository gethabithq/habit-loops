---
name: okx-cex-market
title: OKX CEX Market skill
repo: okx/agent-skills
license: MIT
url: https://gethabit.dev/skills/okx/okx-cex-market
---

# OKX CEX Market skill

The okx cex market skill gives agents read-only OKX market data through the okx CLI: tickers, order books, candles, funding rates, open interest, screeners and over 70 technical indicators.

- Install the skill: `npx skills add okx/agent-skills --skill okx-cex-market`
- Source: https://github.com/okx/agent-skills/tree/HEAD/skills/okx-cex-market
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a ticker or order book; You scan open interest or top movers; You need RSI, MACD or other indicators.
Skip it when: You want to place or cancel orders; You need your account balance.

# Make it a habit: Log a daily market snapshot.

Every morning your agent runs read-only okx market commands: a screener with okx market filter, an open interest scan with okx market oi-change and indicators for your watchlist. It logs raw values only, with no advice, and the next run compares against the log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** data returned, range confirmed. Hard checks: okx market filter prints Total: N with N above zero; no indicator query ends with the No indicator values returned hint; candle requests over 500 bars were confirmed by you first. On fail: retry, max 1 retries.
- **Memory:** daily snapshot log at `loops/okx-market-snapshot-loop/run-log.md`. Read first: the last snapshot, so changes since yesterday stand out.

## Steps

1. **Run preflight.** Your agent follows the shared preflight file the skill points to and checks the okx CLI version.
2. **Screen instruments.** It runs okx market filter with --quoteCcy USDT to rank top movers and high-volume pairs.
3. **Scan open interest.** It runs okx market oi-change for SWAP contracts to find the largest open interest shifts.
4. **Read indicators.** It runs okx market indicator for each watchlist instId, with bar values such as 1H or 1Dutc.
5. **Confirm large ranges.** If a candle history would exceed 500 bars, it tells you the estimate and waits for your yes.
6. **Log the snapshot.** It writes the raw values to the run log, with no recommendation.

Stop rule: One snapshot per run, at most 10 watchlist instruments.

## Permissions

- Writes: loops/okx-market-snapshot-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/okx-market-snapshot-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: data returned, range confirmed. Memory: loops/okx-market-snapshot-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
