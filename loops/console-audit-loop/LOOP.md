---
name: web-debug
title: Web Debug skill
repo: sentimony/skills
license: MIT
url: https://gethabit.dev/skills/sentimony/web-debug
---

# Web Debug skill

The web debug skill lets agents test local web apps with Python Playwright scripts: start servers, wait for rendering, collect console and network signals, take screenshots and tell real errors from noise. For frontend developers.

- Install the skill: `npx skills add sentimony/skills --skill web-debug`
- Source: https://github.com/sentimony/skills/tree/HEAD/plugins/skills/skills/web-debug
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: checking frontend behavior in a browser; collecting console logs and page errors; taking screenshots of a local app.
Skip it when: static reading or tests already find the issue; you test a production site you do not own.

# Make it a habit: Console errors caught before users.

Each night your agent starts the local app with with_server.py, crawls its routes in headless Chromium with a console audit script, confirms each error with a second clean run and keeps a checkpointed log of real errors per route.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** nightly local audit (schedule; Claude Code routine or cron; `0 2 * * *`)
- **Verification:** errors confirmed on rerun. Hard checks: server is reachable on the given host and port; every route finished or is checkpointed; each reported error repeats on a second clean run; network errors are cross-checked with curl. On fail: notify, max 1 retries.
- **Memory:** route audit checkpoint at `loops/console-audit-loop/audit.json`. Read first: finished routes and errors already reported.

## Steps

1. **Start the server.** Your agent runs scripts/with_server.py --help, then starts the dev server with --server, --host and --port.
2. **Confirm the port.** It reads the real port from the server startup log before navigating.
3. **Crawl the routes.** It runs a copy of examples/console_audit.py over the route list, one try block per route.
4. **Collect signals.** It records console errors, warnings, pageerror events, failed requests and HTTP errors.
5. **Filter the noise.** It drops ERR_ABORTED and known headless noise and cross-checks network errors with curl.
6. **Rerun to confirm.** It confirms anomalies with a second clean run and hands root causes to the debugging skill.
7. **Save the checkpoint.** It writes results after every route so the next run resumes.

Stop rule: Stops after one pass over the route list and one confirmation rerun.

## Permissions

- Writes: loops/console-audit-loop/**
- Network: 127.0.0.1
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/console-audit-loop/audit.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: nightly local audit. Verification: errors confirmed on rerun. Memory: loops/console-audit-loop/audit.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
