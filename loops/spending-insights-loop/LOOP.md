---
name: financial-insights
title: Financial Insights skill
repo: stripe/link-cli
license: MIT
url: https://gethabit.dev/skills/stripe/financial-insights
---

# Financial Insights skill

The financial insights skill reads a user's Link transactions, balances, connected sources and precomputed insights to answer read-only questions about spending, available funds, connected accounts and account activity.

- Install the skill: `npx skills add stripe/link-cli --skill financial-insights`
- Source: https://github.com/stripe/link-cli/tree/HEAD/packages/integrations/eve/extension/skills/financial-insights
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Checking a balance or available funds; Summarizing spending for a period; Listing connected accounts.
Skip it when: Making a purchase or payment; Changing a connected source.

# Make it a habit: A weekly answer about your spending.

Each week the agent reads Link transactions, balances and precomputed insights, pages through the full week and writes a short spending summary with its limits. A run log keeps the period, the sources and any stale data notes.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** pagination and status check. Hard checks: list_transactions is paged until has_more is false or absent; currencies are kept separate in every total; pending, missing_permissions and no_data insight results are never reported as zero activity. On fail: stop, max 0 retries.
- **Memory:** weekly spending log at `loops/spending-insights-loop/runs.md`. Read first: last week's period, sources and freshness notes.

## Steps

1. **Check access.** If access is denied, the agent says what it could not read and stops without retrying.
2. **Pick the tools.** It uses list_transactions, list_balances and list_sources only as far as the question needs.
3. **Page through.** It follows starting_after with the same filters until has_more is false.
4. **Read insights.** It calls list_available_insight_types, then list_insights with only the IDs it needs.
5. **Format amounts.** It converts minor units with the ISO 4217 exponent and keeps each currency apart.
6. **Write the answer.** The answer comes first, then the period, the sources and limits such as stale balances or pending activity.

Stop rule: Stops after one weekly summary; a pending insight is not called again in the same run.

## Permissions

- Writes: loops/spending-insights-loop/**
- Network: link.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/spending-insights-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: pagination and status check. Memory: loops/spending-insights-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
