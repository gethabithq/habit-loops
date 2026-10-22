---
name: planetscale-mcp-agent-operating-model
title: PlanetScale MCP Agent Operating Model skill
repo: planetscale/skills
license: MIT
url: https://gethabit.dev/skills/planetscale/planetscale-mcp-agent-operating-model
---

# PlanetScale MCP Agent Operating Model skill

The planetscale mcp agent operating model skill helps database teams set safe rules for agents using PlanetScale MCP, Insights and schema recommendations, with loops that propose work and never mutate production alone.

- Install the skill: `npx skills add planetscale/skills --skill planetscale-mcp-agent-operating-model`
- Source: https://github.com/planetscale/skills/tree/HEAD/planetscale-mcp-agent-operating-model
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You connect agents to PlanetScale MCP; You want daily schema recommendation PRs; You define agent approval gates.
Skip it when: You want fully autonomous production changes; You do not use PlanetScale.

# Make it a habit: Schema fixes proposed, never auto-deployed.

Each day your agent reads open schema recommendations and top Insights regressions, correlates them with repository code, and files ranked issues or PRs with a dev branch and deploy request. You review and approve. A run log stops duplicate issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily recommendation sweep (schedule; Claude Code routine or cron; `0 6 * * *`)
- **Verification:** you approve database changes. Hard checks: no write SQL or DDL ran against production; no issue filed twice for the same fingerprint or recommendation ID; each PR carries fingerprint, metrics and expected effect; report ends with the statement that no MCP write tools were used. On fail: stop, max 0 retries.
- **Memory:** filed recommendations log at `loops/planetscale-recommendation-loop/run-log.md`. Read first: recommendation IDs and fingerprints already filed.

## Steps

1. **Read authorization.** Re-read the project AGENTS.md targeting and approval rules at run start.
2. **Read recommendations.** List open schema recommendations and top Insights regressions with the insights-only MCP server.
3. **Correlate.** Match query patterns to the repository code that issues them.
4. **Propose.** Create a dev branch, apply the DDL there, open a PR and a deploy request, or file an issue.
5. **You review.** You review and make every merge or deploy decision.
6. **Log.** Record filed IDs and send status to the configured channel.

Stop rule: Stops after 3 recommendations per run.

## Permissions

- Writes: loops/planetscale-recommendation-loop/**
- Network: none
- Sends: issues and pull requests, deploy requests to review-protected branches
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/planetscale-recommendation-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily recommendation sweep. Verification: you approve database changes. Memory: loops/planetscale-recommendation-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
