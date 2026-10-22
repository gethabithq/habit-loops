---
name: market-environment-analysis
title: Market Environment Analysis skill
repo: tradermonty/claude-trading-skills
license: MIT
url: https://gethabit.dev/skills/tradermonty/market-environment-analysis
---

# Market Environment Analysis skill

Market environment analysis reads global markets, US, European, Asian, forex, commodities and economic indicators, and produces a report with a risk-on or risk-off call, sector analysis and strategy implications. For traders and investors tracking conditions.

- Install the skill: `npx skills add tradermonty/claude-trading-skills --skill market-environment-analysis`
- Source: https://github.com/tradermonty/claude-trading-skills/tree/HEAD/examples/weekly-trade-strategy/.claude/skills/market-environment-analysis
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a market conditions report; You assess risk sentiment; You track global markets and forex.
Skip it when: You want single-stock analysis only; You need live trade signals.

# Make it a habit: A daily global market conditions read.

Each morning your agent collects global market data with web search, assesses trend, risk sentiment, volatility and sector rotation, and writes a structured report with an executive summary and strategy implications. A log keeps yesterday's read.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily market report (schedule; Claude Code routine; `0 7 * * 1-5`)
- **Verification:** data + report structure. Hard checks: major indices, forex, commodities, yields and VIX were collected; the report has an executive summary and the standard sections; the risk-on or risk-off call is stated. On fail: notify, max 1 retries.
- **Memory:** market read log at `loops/market-environment-report-loop/log.md`. Read first: yesterday's trend, risk read and levels.

## Steps

1. **Collect data.** Use web search for the major indices, forex, commodities, Treasury yields and VIX.
2. **Assess the environment.** Read trend direction, risk sentiment, volatility from VIX and sector rotation.
3. **Load references.** Read indicators.md and analysis_patterns.md for levels and risk-on or risk-off criteria.
4. **Write the report.** Write the executive summary, global overview, forex and commodities, events and risk analysis.
5. **Log the read.** Record today's trend and risk read for comparison.

Stop rule: Stops after one market report per run, with 1 retry.

## Permissions

- Writes: loops/market-environment-report-loop/**
- Network: bloomberg.com, reuters.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/market-environment-report-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily market report. Verification: data + report structure. Memory: loops/market-environment-report-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
