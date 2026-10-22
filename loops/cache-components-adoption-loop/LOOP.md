---
name: next-cache-components-adoption
title: Next Cache Components Adoption skill
repo: vercel/next.js
license: MIT
url: https://gethabit.dev/skills/vercel/next-cache-components-adoption
---

# Next Cache Components Adoption skill

The next cache components adoption skill turns on Cache Components in a Next.js App Router app and works through blocking routes feature by feature until next build passes.

- Install the skill: `npx skills add vercel/next.js --skill next-cache-components-adoption`
- Source: https://github.com/vercel/next.js/tree/HEAD/skills/next-cache-components-adoption
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You enable cacheComponents in Next.js; The build floods with blocking-prerender errors; You want to adopt route by route in small PRs.
Skip it when: The app only uses the pages router; Next.js is below 16.3 and you cannot upgrade.

# Make it a habit: One feature adopted per run.

Each run, your agent picks the next feature still marked TODO: Cache Components adoption, removes its opt-outs top-down, fixes blockers from the linked docs and verifies in next dev and the browser. next build must pass, then you decide on the PR.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** next feature to adopt (manual; Claude Code session; `grep -rln "TODO: Cache Components adoption" app finds files`)
- **Verification:** build, browser, your OK. Hard checks: next build completes without blocking-route errors; no bare TODO: Cache Components adoption left in the feature; codemod run reports a file count above zero; dev overlay is clean on every route of the feature. On fail: retry, max 2 retries.
- **Memory:** TODO markers as queue at `app/`. Read first: files still holding // TODO: Cache Components adoption.

## Steps

1. **Check requires.** The agent confirms an App Router project, Next.js 16.3+, a bootable app and no experimental.dynamicIO.
2. **Choose a strategy.** It asks if you want one opt-out PR first or everything on one branch.
3. **Pre-step.** For the PR-first path it runs npx @next/codemod@latest cache-components-instant-false and gets next build passing.
4. **Install verifier.** It adds the next-dev-loop skill for runtime checks unless a real blocker stops it.
5. **Adopt a feature.** It removes opt-outs top-down, fixes each blocker from its docs page and checks siblings.
6. **Verify.** It confirms the static shell renders first and each Suspense fallback resolves.
7. **Check in.** It shows you the routes and asks whether to open a PR or stop; it never commits without your yes.

Stop rule: One feature per run, at most two fix rounds per route.

## Permissions

- Writes: app/**, next.config.ts
- Network: nextjs.org, github.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`app/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: next feature to adopt. Verification: build, browser, your OK. Memory: app/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
