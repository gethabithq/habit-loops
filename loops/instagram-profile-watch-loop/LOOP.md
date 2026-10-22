---
name: instagram-scraper
title: Instagram Scraper skill
repo: skillify-sh/skills
license: MIT
url: https://gethabit.dev/skills/skillify-sh/instagram-scraper
---

# Instagram Scraper skill

Instagram scraper pulls public Instagram data such as profiles, posts, reels, comments, hashtags and mentions through Apify, without an Instagram login. For marketers tracking competitors, influencers or brand mentions.

- Install the skill: `npx skills add skillify-sh/skills --skill instagram-scraper`
- Source: https://github.com/skillify-sh/skills/tree/HEAD/skills/instagram-scraper
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: checking follower or post counts; tracking a competitor's posts; finding posts under a hashtag.
Skip it when: you need private account data; you cannot use an Apify account.

# Make it a habit: Fresh public Instagram numbers, logged.

On a schedule, your agent runs the preflight, then pulls public profile details or recent posts for a short list of accounts through apify/instagram-scraper with a fixed resultsLimit. It logs follower and post counts so each run shows the change.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly profile check (schedule; Claude Code routine or cron; `0 8 * * 1`)
- **Verification:** preflight and result check. Hard checks: preflight prints AUTH_OK; run status is SUCCEEDED, not FAILED or ABORTED; result count is above zero or the account is reported as private or empty; resultsLimit is set on every call. On fail: stop, max 0 retries.
- **Memory:** profile numbers history at `loops/instagram-profile-watch-loop/history.md`. Read first: last run's follower and post counts per account.

## Steps

1. **Run the preflight.** Check for APIFY_TOKEN or a logged-in Apify CLI before any data call.
2. **Pick the mode.** Use resultsType details for profile numbers and posts only when recent posts are needed.
3. **Fetch the data.** Call the actor with curl or apify call and a small resultsLimit.
4. **Read the quirks.** Report a likesCount of -1 as hidden and an empty array as private or quiet.
5. **Log the change.** Compare counts with the last run and append them to the history file.

Stop rule: Stops after one call per account on the list, and never repeats a call after a 401 or 402.

## Permissions

- Writes: loops/instagram-profile-watch-loop/**
- Network: api.apify.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/instagram-profile-watch-loop/history.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly profile check. Verification: preflight and result check. Memory: loops/instagram-profile-watch-loop/history.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
