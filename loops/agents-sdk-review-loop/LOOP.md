---
name: agents-sdk
title: Agents SDK skill
repo: cloudflare/skills
license: Apache-2.0
url: https://gethabit.dev/skills/cloudflare/agents-sdk
---

# Agents SDK skill

The agents sdk skill helps agents build, debug and review Cloudflare Agents SDK apps with the agents package: state, callable RPC, scheduling, workflows, MCP, chat and email, using current docs. For Workers developers.

- Install the skill: `npx skills add cloudflare/skills --skill agents-sdk`
- Source: https://github.com/cloudflare/skills/tree/HEAD/skills/agents-sdk
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You build an agent on Cloudflare; You add scheduling or workflows; You connect or build MCP servers.
Skip it when: You do not deploy on Cloudflare Workers; You only need a stateless Worker.

# Make it a habit: Cloudflare agents reviewed on every change.

When a pull request changes a Cloudflare Agents SDK app, your agent pulls the current docs, checks the install, the wrangler config and migrations against the skill's gotchas, and runs the tests. A board keeps open findings for the next pull request.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches agent code (event; GitHub Actions or Claude Code routine; `pull_request paths: wrangler.jsonc, files importing agents`)
- **Verification:** tests and config checks. Hard checks: npm ls agents shows the agents package; test suite passes; tsconfig does not enable experimentalDecorators; diff changes no existing migration tag; every agent class has its own DO binding and migration entry. On fail: notify, max 0 retries.
- **Memory:** open agent findings at `loops/agents-sdk-review-loop/board.md`. Read first: findings still open from earlier reviews.

## Steps

1. **Fetch current docs.** Pull the matching pages from developers.cloudflare.com/agents instead of relying on old knowledge.
2. **Verify the install.** Run npm ls agents and note if the package is missing.
3. **Check the config.** Compare wrangler.jsonc against the gotchas: nodejs_compat, one binding and migration per class, no edited old migrations.
4. **Review the code.** Check state, routing, callable methods and scheduling against the matching files in references/.
5. **Run the tests.** Run the project's test suite and record the result.
6. **Update the board.** Add new findings and close the ones the change fixed.

Stop rule: One pull request per run, no retries.

## Permissions

- Writes: loops/agents-sdk-review-loop/**
- Network: developers.cloudflare.com, api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/agents-sdk-review-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches agent code. Verification: tests and config checks. Memory: loops/agents-sdk-review-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
