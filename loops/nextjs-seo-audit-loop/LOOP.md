---
name: nextjs-seo
title: Next.js SEO skill
repo: laguagu/claude-code-nextjs-skills
license: MIT
url: https://gethabit.dev/skills/laguagu/nextjs-seo
---

# Next.js SEO skill

The next.js seo skill helps Next.js App Router developers implement and audit SEO: metadata and social images, sitemap and robots, canonicals, structured data, Core Web Vitals and AI crawler policy.

- Install the skill: `npx skills add laguagu/claude-code-nextjs-skills --skill nextjs-seo`
- Source: https://github.com/laguagu/claude-code-nextjs-skills/tree/HEAD/skills/nextjs-seo
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You audit a Next.js site for SEO; Pages are not getting indexed; You set up metadata and sitemaps.
Skip it when: You build Next.js features unrelated to SEO; You use the Pages Router only.

# Make it a habit: Next.js pages stay indexable.

Each week your agent audits public Next.js routes: status codes, canonicals, metadata with the production metadataBase, sitemap and robots, structured data that matches visible content, and field Core Web Vitals. A run log keeps the evidence per route.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly SEO audit (schedule; Claude Code routine or GitHub Actions; `0 7 * * 2`)
- **Verification:** production HTML checks pass. Hard checks: each audited route returns the expected status code; emitted metadata URLs are absolute and use the production base; structured data describes visible content; field LCP, INP and CLS are reported or marked unavailable. On fail: notify, max 0 retries.
- **Memory:** route evidence log at `loops/nextjs-seo-audit-loop/run-log.md`. Read first: routes audited last week and open issues.

## Steps

1. **Read the version.** Read the installed Next.js version and matching docs in node_modules/next/dist/docs/.
2. **Verify basics.** Check URLs, redirects, status codes, crawl rules, index directives and canonicals.
3. **Check metadata.** Use the reference for the affected area, such as metadata, sitemaps or structured data.
4. **Keep crawler policy.** Preserve the owner's rules for training, search and user-triggered crawlers.
5. **Separate evidence.** Report field data, indexing reports and Lighthouse lab results apart, with gaps marked.

Stop rule: Stops after 20 routes per run.

## Permissions

- Writes: loops/nextjs-seo-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/nextjs-seo-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly SEO audit. Verification: production HTML checks pass. Memory: loops/nextjs-seo-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
