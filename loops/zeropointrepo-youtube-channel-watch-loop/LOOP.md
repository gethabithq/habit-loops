---
name: youtube-full
title: YouTube Full skill
repo: zeropointrepo/youtube-skills
license: MIT
url: https://gethabit.dev/skills/zeropointrepo/youtube-full
---

# YouTube Full skill

The youtube full skill helps agents and researchers get YouTube transcripts, search videos and channels, browse channel feeds and playlists, and search within a channel through TranscriptAPI.

- Install the skill: `npx skills add zeropointrepo/youtube-skills --skill youtube-full`
- Source: https://github.com/zeropointrepo/youtube-skills/tree/HEAD/clawhub/youtube-full
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need a video transcript; You research a topic on YouTube; You follow new uploads from channels.
Skip it when: You want to upload or manage videos; Your research needs written sources only.

# Make it a habit: New videos from your channels, summarized.

Each day your agent calls channel/latest for each watched channel, picks uploads it has not seen, fetches their transcripts with timestamps and metadata, and writes short notes. A log keeps video IDs already covered.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily channel check (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** requests succeed, notes written. Hard checks: every request sends Authorization and a User-Agent header; channel/latest returns without 401 or 403; each new video note has a transcript or a 404 reason. On fail: notify, max 1 retries.
- **Memory:** seen videos log at `loops/youtube-channel-watch-loop/run-log.md`. Read first: video IDs already summarized per channel.

## Steps

1. **Check the key.** Confirm TRANSCRIPT_API_KEY is set, else follow references/auth-setup.md.
2. **Latest uploads.** Call channel/latest with each @handle.
3. **Skip seen videos.** Drop video IDs already in the log.
4. **Fetch transcripts.** Call transcript with format=text, include_timestamp=true and send_metadata=true.
5. **Write notes.** Summarize each video with timestamps and log the IDs.

Stop rule: Stops after 10 channels and 3 new videos per channel per run.

## Permissions

- Writes: loops/youtube-channel-watch-loop/**
- Network: transcriptapi.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/youtube-channel-watch-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily channel check. Verification: requests succeed, notes written. Memory: loops/youtube-channel-watch-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
