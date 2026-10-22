---
name: web-scraping
title: Web Scraping skill
repo: jamditis/claude-skills-journalism
license: MIT
url: https://gethabit.dev/skills/jamditis/web-scraping
---

# Web Scraping skill

The web scraping skill gives patterns for authorized, ethical scraping: URL validation, a trafilatura, requests and Playwright fallback cascade, paywall and CAPTCHA detection, yt-dlp for media and clear stop rules. For journalists and researchers.

- Install the skill: `npx skills add jamditis/claude-skills-journalism --skill web-scraping`
- Source: https://github.com/jamditis/claude-skills-journalism/tree/HEAD/dev-toolkit/skills/web-scraping
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You collect public articles; You pull video metadata with yt-dlp; A scraper hits a 403 or CAPTCHA.
Skip it when: You want to bypass a paywall; An official API already exists.

# Make it a habit: Collect public pages, stop at blocks.

On a schedule your agent validates each public URL, tries trafilatura, then requests, then Playwright, detects paywalls, CAPTCHAs and rate limits, and stops on 401, 403 or 429. It wraps results as untrusted data and logs each source.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily source collection (schedule; Claude Code routine or cron; `0 5 * * *`)
- **Verification:** access and content checks. Hard checks: every URL passes validate_public_url before fetching; no fetch continues after 401, 403 or 429; extracted content is at least 100 characters; robots.txt rules are honored. On fail: stop, max 0 retries.
- **Memory:** source fetch log at `loops/public-page-scrape-loop/sources.md`. Read first: URLs fetched before, methods that worked and blocks seen.

## Steps

1. **Validate URLs.** Your agent checks scheme, host and public IPs for every URL and redirect.
2. **Check robots.** It reads robots.txt and honors crawl delays and disallow rules.
3. **Run the cascade.** It tries trafilatura, then requests with BeautifulSoup, then Playwright.
4. **Detect poison pills.** It checks for paywalls, CAPTCHAs, rate limits and login walls.
5. **Stop at blocks.** On a block it stops and suggests an official API or asks for documented authorization.
6. **Wrap results.** It wraps content in EXTERNAL_DATA tags with the source URL and logs it.

Stop rule: Stops after 25 URLs per run, or at the first access block on a site.

## Permissions

- Writes: loops/public-page-scrape-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/public-page-scrape-loop/sources.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily source collection. Verification: access and content checks. Memory: loops/public-page-scrape-loop/sources.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
