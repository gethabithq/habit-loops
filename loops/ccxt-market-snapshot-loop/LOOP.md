---
name: ccxt-cli
title: CCXT CLI skill
repo: ccxt/ccxt
license: MIT
url: https://gethabit.dev/skills/ccxt/ccxt-cli
---

# CCXT CLI skill

The ccxt cli skill calls any unified CCXT method on 100+ crypto exchanges from the terminal, with API key setup, sandbox mode, WebSocket streams, OHLCV charts and raw JSON output for scripts.

- Install the skill: `npx skills add ccxt/ccxt --skill ccxt-cli`
- Source: https://github.com/ccxt/ccxt/tree/HEAD/.claude/skills/ccxt-cli
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You query an exchange from a shell; You test API credentials; You debug exchange requests.
Skip it when: You write a full trading program; You want hands-off live trading.

# Make it a habit: Daily read-only market snapshots.

Every morning your agent runs read-only ccxt calls such as fetchTicker and fetchOHLCV with --raw for a watch list of symbols, checks the exit code, and appends the JSON to a snapshot file. It places no orders. A log keeps errors per exchange.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; cron or Claude Code routine; `0 7 * * *`)
- **Verification:** exit code and JSON. Hard checks: each ccxt call exits with code 0; each --raw output parses as JSON; count of saved snapshots equals the watch list size. On fail: notify, max 1 retries.
- **Memory:** snapshot and error log at `loops/ccxt-market-snapshot-loop/snapshots.md`. Read first: watch list, last snapshot and exchanges that failed before.

## Steps

1. **Read the watch list.** Load the exchanges and symbols from the snapshot file.
2. **Fetch the tickers.** Run ccxt <exchangeId> fetchTicker <symbol> --raw for each entry.
3. **Fetch the candles.** Run fetchOHLCV with a timeframe, padding skipped optionals with undefined.
4. **Check each result.** Treat a non-zero exit code or non-JSON output as an error.
5. **Handle known errors.** Use --refresh-markets for BadSymbol and log geo-block errors.
6. **Save the snapshot.** Append the results and errors to the snapshot file.

Stop rule: Stops after 20 symbols per run; never calls createOrder or withdraw.

## Permissions

- Writes: loops/ccxt-market-snapshot-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ccxt-market-snapshot-loop/snapshots.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: exit code and JSON. Memory: loops/ccxt-market-snapshot-loop/snapshots.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
