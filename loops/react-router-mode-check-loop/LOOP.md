---
name: react-router
title: React Router skill
repo: remix-run/react-router
license: MIT
url: https://gethabit.dev/skills/remix-run/react-router
---

# React Router skill

React router helps build apps in framework, data, declarative and unstable RSC modes: routes, loaders, actions, forms, fetchers, navigation, pending UI, SSR and upgrades, using the installed version's docs. For React developers using React Router.

- Install the skill: `npx skills add remix-run/react-router --skill react-router`
- Source: https://github.com/remix-run/react-router/tree/HEAD/.agents/skills/react-router
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You configure routes or route modules; You add loaders or actions; You upgrade React Router.
Skip it when: You use TanStack Router or Next.js; You build a non-React app.

# Make it a habit: Route changes match the app's mode.

On pull requests that touch routing, your agent first identifies the React Router mode, framework, data or declarative, loads the matching reference and the installed version's docs, and reviews the change against that mode. The build must pass and a log keeps the detected mode.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** route code changes (event; GitHub Actions or Claude Code routine; `pull_request paths: app/routes/**, app/routes.ts`)
- **Verification:** mode + build. Hard checks: the app's React Router mode is identified before review; no framework or data pattern is applied to a declarative app; the build passes. On fail: notify, max 1 retries.
- **Memory:** mode and review log at `loops/react-router-mode-check-loop/log.md`. Read first: the app's detected mode and open routing issues.

## Steps

1. **Identify the mode.** Detect framework, data or declarative mode from the config files, imports and route setup.
2. **Load the reference.** Read the matching reference, plus rsc.md for an unstable RSC app.
3. **Read installed docs.** Read the version-matched docs under node_modules/react-router/docs and honour each file's mode marker.
4. **Review the change.** Check loaders, actions, forms, params and pending UI against that mode's patterns.
5. **Build and log.** Run the build and log the detected mode and any issue.

Stop rule: Stops after the changed routes of one pull request, with 1 retry.

## Permissions

- Writes: loops/react-router-mode-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/react-router-mode-check-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: route code changes. Verification: mode + build. Memory: loops/react-router-mode-check-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
