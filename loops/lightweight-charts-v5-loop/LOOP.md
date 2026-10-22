---
name: lightweight-charts
title: Lightweight Charts skill
repo: tradingview/lightweight-charts
license: Apache-2.0
url: https://gethabit.dev/skills/tradingview/lightweight-charts
---

# Lightweight Charts skill

The lightweight charts skill helps developers build TradingView lightweight-charts v5 charts: series, scales, realtime data, panes, markers, plugins, SSR loading and React or Vue wrappers.

- Install the skill: `npx skills add tradingview/lightweight-charts --skill lightweight-charts`
- Source: https://github.com/tradingview/lightweight-charts/tree/HEAD/.github/skills/lightweight-charts
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You build a candlestick chart; You migrate from v4 to v5; Your chart snaps on every update.
Skip it when: You use the Python wrapper; You use another chart library.

# Make it a habit: Chart code stays on v5.

On every pull request that touches chart code, your agent reads the installed lightweight-charts version and typings, flags v4 calls with their v5 replacements and checks the time and wrapper foot-guns. A log keeps the version and open findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** chart code changes (event; GitHub Actions or Claude Code routine; `pull_request touches files importing lightweight-charts`)
- **Verification:** no v4 API left. Hard checks: no addLineSeries, addCandlestickSeries or series.setMarkers calls; UTCTimestamp values are in seconds, not Date.now(); no timeScale timezone option; every API name exists in dist/typings.d.ts. On fail: notify, max 0 retries.
- **Memory:** chart findings log at `loops/lightweight-charts-v5-loop/run-log.md`. Read first: installed version and open findings.

## Steps

1. **Read version.** Read node_modules/lightweight-charts/package.json and grep the typings.
2. **Map v4 calls.** Replace v4 snippets using the v4 to v5 replacement matrix.
3. **Check time.** Check seconds timestamps, ascending unique times and update versus setData.
4. **Check wrappers.** Confirm one chart per mount, chart.remove() on cleanup and client-only loading in Next.js.
5. **Report.** Name the v5 API, the foot-gun and what source was checked.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/lightweight-charts-v5-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/lightweight-charts-v5-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: chart code changes. Verification: no v4 API left. Memory: loops/lightweight-charts-v5-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
