---
name: youtube-api
title: YouTube API skill
repo: fetcher-sh/fetcher-skills
license: MIT
url: https://gethabit.dev/skills/fetcher-sh/youtube-api
---

# YouTube API skill

The YouTube API skill (youtube-api) returns YouTube search, channel, video, playlist, comment, hashtag and trending data as clean JSON through fetcher.sh, with real filters and no OAuth or daily quota. For agents building YouTube data pipelines.

- Install the skill: `npx skills add fetcher-sh/fetcher-skills --skill youtube-api`
- Source: https://github.com/fetcher-sh/fetcher-skills/tree/HEAD/skills/youtube-api
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: searching YouTube videos with filters; monitoring a channel's uploads; pulling trending or hashtag feeds.
Skip it when: you only need one occasional lookup; you must use the official YouTube Data API.

# Make it a habit: A daily record of channel uploads.

On a schedule, your agent pulls each watched channel's newest videos and a topic search through the youtube-api, reads the clean JSON and records what is new. A run log keeps the last video id per channel.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily channel check (schedule; cron; `0 7 * * *`)
- **Verification:** video data returned. Hard checks: each channel videos call returns status 200; results come back with entries, count above zero; the record file is written. On fail: notify, max 1 retries.
- **Memory:** channel video log at `loops/youtube-channel-watch-loop/run-log.md`. Read first: the last recorded video id per watched channel.

## Steps

1. **Load watchlist.** Your agent reads the channels and topics to watch, by id, handle or custom path.
2. **Pull channel videos.** It calls the channel videos, shorts and live-streams endpoints for each channel.
3. **Search topics.** It searches videos with upload-date, duration and sort filters for your tracked topics.
4. **Read JSON.** It reads the clean JSON responses and finds the new items since last run.
5. **Record.** It writes the new videos and the last id per channel to the run log.

Stop rule: Stops after one pass over the watchlist per run, with at most one retry.

## Permissions

- Writes: loops/youtube-channel-watch-loop/**
- Network: youtube.fetcher.sh
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/youtube-channel-watch-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily channel check. Verification: video data returned. Memory: loops/youtube-channel-watch-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
