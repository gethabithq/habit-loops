---
name: neon-functions
title: Neon Functions skill
repo: neondatabase/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/neondatabase/neon-functions
---

# Neon Functions skill

The neon functions skill helps developers deploy long-running Node.js HTTP functions on a Neon branch, for APIs, agents, WebSocket and SSE servers, webhooks and MCP servers.

- Install the skill: `npx skills add neondatabase/agent-skills --skill neon-functions`
- Source: https://github.com/neondatabase/agent-skills/tree/HEAD/plugins/neon-postgres/skills/neon-functions
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Your agent stream outlasts lambda timeouts; You need a WebSocket or SSE server; You want a backend that branches with your data.
Skip it when: You host a static site; Your region is not supported.

# Make it a habit: Functions deploy locked down.

When neon.ts or function code changes, your agent plans and deploys the Neon Functions on the branch, then checks that the public URL rejects callers without a valid token, that the pg pool is attached, and logs the result.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** function code changed (event; GitHub Actions or Claude Code routine; `push touching neon.ts or src/**`)
- **Verification:** auth holds after deploy. Hard checks: neon config plan shows no pending change after deploy; a request without a bearer token gets 401 from the invocation URL; one test user cannot read another user's rows; every new Pool is followed by attachDatabasePool(pool); no declared function env key is coerced to an empty string. On fail: stop, max 1 retries.
- **Memory:** deploy check log at `loops/neon-function-deploy-check-loop/run-log.md`. Read first: slugs, URLs and failed checks from last run.

## Steps

1. **Load neon skill.** The agent first uses the parent neon skill for the branch-first workflow, as this skill asks.
2. **Check region.** It confirms the project is in a region where Neon Functions is available.
3. **Check the code.** It looks for a module-scope pg pool with a small max, attachDatabasePool, and env keys present in the --env file.
4. **Plan and deploy.** It runs neon config plan, then neon deploy --env <file>.
5. **Get the URL.** It reads the invocation_url with neon functions get <slug>.
6. **Test auth.** It calls the URL without a token and as two users to confirm access stays scoped.
7. **Read logs and record.** It checks neon logs query with source function, then writes results to the run log.

Stop rule: Stops after one branch deploy per run, with at most one retry.

## Permissions

- Writes: loops/neon-function-deploy-check-loop/**
- Network: neon.com, *.aws.neon.tech
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/neon-function-deploy-check-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: function code changed. Verification: auth holds after deploy. Memory: loops/neon-function-deploy-check-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
