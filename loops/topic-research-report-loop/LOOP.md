---
name: active-research
title: Active Research skill
repo: actionbook/actionbook
license: Apache-2.0
url: https://gethabit.dev/skills/actionbook/active-research
---

# Active Research skill

The active research skill researches any topic, paper or technology with the Actionbook browser, searching arXiv and the web, reading sources in depth and producing a structured json-ui report rendered as HTML. For people who need deep-dive reports.

- Install the skill: `npx skills add actionbook/actionbook --skill active-research`
- Source: https://github.com/actionbook/actionbook/tree/HEAD/skills/active-research
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: you need a deep-dive report; you analyze an arXiv paper; you compare tools in a field.
Skip it when: a quick answer is enough; Actionbook is not installed.

# Make it a habit: Tracked topics get fresh research reports.

Every week the agent researches a topic you track with the Actionbook browser: several query angles, arXiv first, then web search, deep reads of the best sources. It writes a json-ui report, renders it to HTML and keeps the last report for comparison.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly topic research (schedule; cron or Claude Code routine; `0 6 * * 1`)
- **Verification:** report renders with sources. Hard checks: ./output/<topic-slug>.json exists and includes BrandHeader and BrandFooter; json-ui render writes the HTML file; the Sources LinkGroup lists at least 3 sources; MetricsGrid value and suffix fields are plain strings. Critic: claude-opus-5-5, pass at 17/20. On fail: retry, max 1 retries.
- **Memory:** last topic report at `./output/<topic-slug>.json`. Read first: the previous report's key findings and sources.

## Steps

1. **Read last report.** Open the previous JSON report to see earlier findings and sources.
2. **Plan the queries.** Write 5-8 queries from angles such as overview, latest news, technical detail and comparisons.
3. **Look up selectors.** Run actionbook search and actionbook get for known sites before browsing them.
4. **Search arXiv first.** Use URL-based arXiv search, then add Google or Bing results for non-academic sources.
5. **Deep read sources.** Read pages with actionbook browser fetch and skip dead links without retrying.
6. **Write the report.** Synthesize overview, key findings, analysis, evidence and sources into a json-ui JSON file.
7. **Render to HTML.** Run json-ui render with absolute paths, trying all three methods before giving up.
8. **Close the browser.** Run actionbook browser close, even after errors.

Stop rule: One topic per run, 5-8 queries and at most 20 source pages.

## Permissions

- Writes: ./output/
- Network: arxiv.org, ar5iv.org, huggingface.co, scholar.google.com, www.google.com, www.bing.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`./output/<topic-slug>.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly topic research. Verification: report renders with sources. Memory: ./output/<topic-slug>.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
