---
name: instagram-api
title: Instagram API skill
repo: fetcher-sh/fetcher-skills
license: MIT
url: https://gethabit.dev/skills/fetcher-sh/instagram-api
---

# Instagram API skill

The instagram api skill from fetcher.sh gives an agent plain HTTP GET endpoints for Instagram profiles, posts, reels, stories, followers, comments, hashtags, locations and audio feeds, with no login. For people building social listening and data pipelines.

- Install the skill: `npx skills add fetcher-sh/fetcher-skills --skill instagram-api`
- Source: https://github.com/fetcher-sh/fetcher-skills/tree/HEAD/skills/instagram-api
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You look up a profile by handle; You monitor a hashtag or location; You export followers.
Skip it when: You need to post to Instagram; You have Graph API access already.

# Make it a habit: Track hashtags and profiles daily.

Each day your agent calls the fetcher.sh Instagram endpoints for your watched hashtags, locations and profiles, keeps only posts it has not seen and writes a short digest. A seen-posts file keeps ids so the next run skips them.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily hashtag watch (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** status 200, new posts. Hard checks: every call returns status 200; no 402 topup_required response; new post count is logged, even when zero. On fail: notify, max 1 retries.
- **Memory:** seen post ids at `loops/instagram-hashtag-watch-loop/seen.json`. Read first: post ids already reported.

## Steps

1. **Load the watch list.** Your agent reads the hashtags, location ids and handles you want to follow.
2. **Resolve profiles.** It calls /api/user/handle/{handle} once to get numeric ids.
3. **Fetch feeds.** It calls /api/hashtag/{name}/posts, /api/location/{id}/posts and /api/user/{id}/posts with your Bearer key.
4. **Drop seen posts.** It keeps only post ids not in seen.json.
5. **Write the digest.** It writes a short digest and adds the new ids to seen.json.

Stop rule: Stops after 30 API calls per run.

## Permissions

- Writes: loops/instagram-hashtag-watch-loop/**
- Network: instagram.fetcher.sh
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/instagram-hashtag-watch-loop/seen.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily hashtag watch. Verification: status 200, new posts. Memory: loops/instagram-hashtag-watch-loop/seen.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
