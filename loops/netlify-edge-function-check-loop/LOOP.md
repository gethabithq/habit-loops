---
name: netlify-edge-functions
title: Netlify Edge Functions skill
repo: netlify/context-and-tools
license: MIT
url: https://gethabit.dev/skills/netlify/netlify-edge-functions
---

# Netlify Edge Functions skill

The netlify edge functions skill helps an agent write, route, cache and debug Deno-based edge handlers on Netlify, from auth gates and geo redirects to streaming SSR. For developers who deploy sites on Netlify.

- Install the skill: `npx skills add netlify/context-and-tools --skill netlify-edge-functions`
- Source: https://github.com/netlify/context-and-tools/tree/HEAD/agent-plugin/skills/netlify-edge-functions
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add auth middleware at the edge; You redirect visitors by country or cookie; An edge function silently does nothing.
Skip it when: The job is long-running work; Your site is not on Netlify.

# Make it a habit: No silent edge functions ship.

When a pull request changes netlify/edge-functions, your agent checks every function for a route, both caching parts, env access through Netlify.env.get and no duplicate .ts and .js names. A notes file keeps the footguns found before.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** edge function file changed (event; GitHub Actions or Claude Code routine; `pull_request paths netlify/edge-functions/**`)
- **Verification:** every function has route. Hard checks: each function has config.path, pattern or an [[edge_functions]] entry; cache: "manual" appears only together with cache headers on the Response; no foo.ts and foo.js with the same name; no process.env outside Next.js middleware. On fail: notify, max 0 retries.
- **Memory:** edge footgun notes at `loops/netlify-edge-function-check-loop/notes.md`. Read first: footguns this repo hit before.

## Steps

1. **Collect changed functions.** Your agent lists the changed files under netlify/edge-functions and the netlify.toml declarations.
2. **Check routes.** Each function needs a path, a pattern or a toml entry, or it never runs.
3. **Check caching.** A function with cache: "manual" must also set Cache-Control or a related header on its Response.
4. **Check scope.** A path of /* without excludedPath gets flagged, because it runs on every asset.
5. **Check env access.** Env reads must use Netlify.env.get, and no variables may rely on netlify.toml.
6. **Report findings.** The agent comments the failed checks and adds new footguns to the notes file.

Stop rule: Stops after one pull request and at most 20 functions per run.

## Permissions

- Writes: loops/netlify-edge-function-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/netlify-edge-function-check-loop/notes.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: edge function file changed. Verification: every function has route. Memory: loops/netlify-edge-function-check-loop/notes.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
