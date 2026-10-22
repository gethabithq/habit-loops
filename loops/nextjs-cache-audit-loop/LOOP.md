---
name: nextjs-cache-architecture
title: Next.js Cache Architecture skill
repo: mohamed-hossam1/nextjs-skills
license: MIT
url: https://gethabit.dev/skills/mohamed-hossam1/nextjs-cache-architecture
---

# Next.js Cache Architecture skill

Next.js Cache Architecture helps agents design caching in Next.js 16+ App Router: use cache, a tag registry, revalidation utilities, Suspense boundaries, personalized content and migration from unstable_cache. For developers fixing or building Next.js caching.

- Install the skill: `npx skills add mohamed-hossam1/nextjs-skills --skill nextjs-cache-architecture`
- Source: https://github.com/mohamed-hossam1/nextjs-skills/tree/HEAD/skills/nextjs-cache-architecture
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add caching to a Next.js app; You debug stale data; You migrate off unstable_cache.
Skip it when: You use the Pages Router; Your app has no server data.

# Make it a habit: Cache tags and invalidation stay correct.

On every pull request that touches data or actions, your agent runs scripts/audit.mjs, walks the common cache mistakes and checks that tags live in lib/cache/tags.ts and updateTag only in lib/cache/revalidate.ts. next build runs last, and a log keeps open issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** data or action change (event; GitHub Actions or Claude Code routine; `pull_request paths: lib/**, app/**`)
- **Verification:** audit script + build. Hard checks: scripts/audit.mjs passes on the project root; no updateTag call outside lib/cache/revalidate.ts; no raw tag strings outside lib/cache/tags.ts; next build passes. On fail: notify, max 1 retries.
- **Memory:** cache issue log at `loops/nextjs-cache-audit-loop/log.md`. Read first: open cache issues and routes marked dynamic last run.

## Steps

1. **Run the audit.** Run scripts/audit.mjs on the project root to check the static parts.
2. **Check the registry.** Make sure every tag string lives in lib/cache/tags.ts.
3. **Check invalidation.** Make sure mutations call revalidation utilities and updateTag lives only in lib/cache/revalidate.ts.
4. **Walk the mistakes.** Check that use cache is the first statement, personal data is read outside the boundary and filtered pages use SuspenseOnSearchParams.
5. **Build last.** Run next build and trace any route that turned dynamic unexpectedly.
6. **Log issues.** Write each issue with its file and fix to the log.

Stop rule: Stops after one audit and one build per pull request.

## Permissions

- Writes: loops/nextjs-cache-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/nextjs-cache-audit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: data or action change. Verification: audit script + build. Memory: loops/nextjs-cache-audit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
