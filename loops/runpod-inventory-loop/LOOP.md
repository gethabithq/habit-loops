---
name: runpod-mcp
title: Runpod MCP skill
repo: runpod/runpod-plugins-official
license: Apache-2.0
url: https://gethabit.dev/skills/runpod/runpod-mcp
---

# Runpod MCP skill

The runpod mcp skill lets an agent manage Runpod pods, serverless endpoints, templates, volumes and billing through the Runpod MCP server, and connect that server when it is missing. For teams that run GPU workloads on Runpod.

- Install the skill: `npx skills add runpod/runpod-plugins-official --skill runpod-mcp`
- Source: https://github.com/runpod/runpod-plugins-official/tree/HEAD/plugins/runpod/skills/runpod-mcp
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You manage Runpod pods; You deploy a serverless endpoint; You audit your Runpod account.
Skip it when: You need file transfer or SSH; You build Docker images locally.

# Make it a habit: Weekly Runpod inventory, nothing touched.

Every Monday your agent checks that the Runpod MCP server is connected, reads the live account state with list and get tools, and writes an inventory table with names and ids. It changes nothing it did not create. A run log keeps last week's ids.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** live read checks. Hard checks: /mcp shows runpod as Connected; a list-endpoints call returns without error; every fact in the report names the read behind it; the table lists each resource with its name and id. On fail: stop, max 0 retries.
- **Memory:** weekly inventory log at `loops/runpod-inventory-loop/runs.md`. Read first: resource ids from the last run.

## Steps

1. **Check connection.** The agent runs /mcp and a list-endpoints call, and falls back to runpodctl if the tools are missing.
2. **Read last run.** It reads the run log to know which ids it saw before.
3. **Route the task.** It follows the lifecycle-crud journey for the inventory and cost-audit for billing.
4. **Read live state.** It confirms every resource and its status with a fresh list or get call.
5. **Audit only.** For resources this run did not create, it lists ids and the actions you could take, and changes nothing.
6. **Write the report.** It closes with one table of names, ids and states, each tied to its read.
7. **Log the run.** It appends the ids and any change since last week to the run log.

Stop rule: Stops after one account audit per run, with no retries.

## Permissions

- Writes: loops/runpod-inventory-loop/**
- Network: mcp.getrunpod.io
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/runpod-inventory-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: live read checks. Memory: loops/runpod-inventory-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
