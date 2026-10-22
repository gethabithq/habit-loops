---
name: ccxt-python
title: CCXT for Python skill
repo: ccxt/ccxt
license: MIT
url: https://gethabit.dev/skills/ccxt/ccxt-python
---

# CCXT for Python skill

CCXT for Python is a guide to the CCXT cryptocurrency exchange library in Python: install, connect to exchanges, fetch market data, place orders, stream live data over WebSocket, handle auth and errors, sync and async. For developers building crypto tools.

- Install the skill: `npx skills add ccxt/ccxt --skill ccxt-python`
- Source: https://github.com/ccxt/ccxt/tree/HEAD/.claude/skills/ccxt-python
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You query a crypto exchange in Python; You fetch tickers or order books; You build a trading bot or data script.
Skip it when: You do not use crypto exchanges; You want a hosted dashboard, not code.

# Make it a habit: Live prices streamed, read-only.

Each day your agent connects to your exchange with CCXT in Python, loads markets, and reads tickers and order books for your watched symbols, read-only. It uses the async API, closes the exchange when done, enables rate limiting and retries only on NetworkError.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily price snapshot (schedule; Claude Code routine; `0 7 * * *`)
- **Verification:** tickers fetched, closed. Hard checks: enableRateLimit is set on the exchange; await exchange.close() runs after the fetches; every symbol exists in load_markets; a NetworkError is retried but an ExchangeError is not. On fail: notify, max 2 retries.
- **Memory:** price snapshot log at `loops/crypto-price-watch-loop/log.md`. Read first: watched symbols and yesterday's prices.

## Steps

1. **Create the exchange.** Create the exchange with ccxt.async_support and enableRateLimit set true.
2. **Load markets.** Call await exchange.load_markets() and confirm each watched symbol exists.
3. **Fetch data.** Use await exchange.fetch_ticker and fetch_order_book for each symbol.
4. **Handle errors.** Retry on NetworkError with backoff and do not retry on ExchangeError.
5. **Close and log.** Call await exchange.close(), then log today's prices and changes.

Stop rule: Stops after at most 20 symbols per run, with 2 retries on network errors.

## Permissions

- Writes: loops/crypto-price-watch-loop/**
- Network: api.binance.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/crypto-price-watch-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily price snapshot. Verification: tickers fetched, closed. Memory: loops/crypto-price-watch-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
