---
name: netlify-config
title: Netlify Config skill
repo: netlify/context-and-tools
license: MIT
url: https://gethabit.dev/skills/netlify/netlify-config
---

# Netlify Config skill

The netlify config skill configures Netlify builds and routing through netlify.toml, _redirects and _headers: build commands, redirects and proxies, SPA fallback, custom headers, env vars and secrets, ignore builds and monorepos. For developers on Netlify.

- Install the skill: `npx skills add netlify/context-and-tools --skill netlify-config`
- Source: https://github.com/netlify/context-and-tools/tree/HEAD/agent-plugin/skills/netlify-config
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: adding redirects or an SPA fallback; scoping env vars per deploy context; configuring a monorepo build.
Skip it when: you host elsewhere; you only write serverless functions.

# Make it a habit: Netlify config changes ship without surprises.

When netlify.toml, _redirects or _headers change, your agent checks them against the skill's rules: rule order, splat placement, scoped env vars, secrets and headers, and fixes problems. A run log keeps findings per change.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** netlify config changes (event; GitHub Actions or Claude Code routine; `pull request touching netlify.toml, _redirects or _headers`)
- **Verification:** config rules hold. Hard checks: no 307 status in redirects; no $VAR injection in netlify.toml outside signed proxies; no secrets in client-prefixed env vars; netlify build passes. On fail: retry, max 2 retries.
- **Memory:** config findings log at `loops/netlify-config-review-loop/run-log.md`. Read first: rules that failed in earlier changes.

## Steps

1. **Read config.** Your agent reads netlify.toml, _redirects and _headers from the root or base directory.
2. **Check redirects.** It checks rule order, splats at segment ends, the SPA fallback and no trailing-slash loops.
3. **Check headers.** It confirms headers are global and not expected on function or proxied responses.
4. **Check env vars.** It keeps secrets in the UI or CLI, marks them --secret, and keeps .env gitignored.
5. **Build.** It runs netlify build locally to confirm the config works.

Stop rule: Stops after one change set per run, with at most 2 fix retries.

## Permissions

- Writes: netlify.toml, _redirects, _headers, loops/netlify-config-review-loop/**
- Network: docs.netlify.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/netlify-config-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: netlify config changes. Verification: config rules hold. Memory: loops/netlify-config-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
