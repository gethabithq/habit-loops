---
name: tiktok-api
title: TikTok API skill
repo: fetcher-sh/fetcher-skills
license: MIT
url: https://gethabit.dev/skills/fetcher-sh/tiktok-api
---

# TikTok API skill

The tiktok api skill from fetcher.sh gives an agent plain HTTP GET endpoints for TikTok post search with sort and date filters, profiles, followers, hashtags, sounds, locations and comments, with no login. For social listening and data pipelines.

- Install the skill: `npx skills add fetcher-sh/fetcher-skills --skill tiktok-api`
- Source: https://github.com/fetcher-sh/fetcher-skills/tree/HEAD/skills/tiktok-api
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You search TikTok posts by keyword; You track a hashtag or sound; You pull a profile's posts.
Skip it when: You need to post to TikTok; You already have official API access.

# Make it a habit: Track TikTok trends for your keywords.

Each day your agent searches TikTok posts for your keywords sorted by most liked for yesterday, pulls watched hashtag feeds through the fetcher.sh API, drops posts already seen and writes a short trend digest. A seen-posts file keeps ids.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily TikTok trend watch (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** status 200, new posts. Hard checks: every call returns status 200; no 402 topup_required response; new post count is logged, even when zero. On fail: notify, max 1 retries.
- **Memory:** seen post ids at `loops/tiktok-trend-watch-loop/seen.json`. Read first: post ids already reported.

## Steps

1. **Load keywords.** Your agent reads your keywords and hashtags to watch.
2. **Search posts.** It calls /api/post/search with sortType MOST_LIKED and dateRange YESTERDAY.
3. **Pull hashtags.** It resolves each tag with /api/hashtag/handle/{name}, then calls /api/hashtag/{id}/posts.
4. **Drop seen posts.** It keeps only post ids not in seen.json.
5. **Write the digest.** It lists new top posts and adds their ids to seen.json.

Stop rule: Stops after 30 API calls per run.

## Permissions

- Writes: loops/tiktok-trend-watch-loop/**
- Network: tiktok.fetcher.sh
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/tiktok-trend-watch-loop/seen.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily TikTok trend watch. Verification: status 200, new posts. Memory: loops/tiktok-trend-watch-loop/seen.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
