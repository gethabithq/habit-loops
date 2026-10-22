---
name: faster-whisper
title: Faster Whisper skill
repo: theplasmak/faster-whisper
license: MIT
url: https://gethabit.dev/skills/theplasmak/faster-whisper
---

# Faster Whisper skill

Faster whisper is a skill for local speech-to-text with faster-whisper: transcripts, SRT and VTT subtitles, speaker diarization, YouTube and podcast feed input, batch runs, transcript search and chapter detection.

- Install the skill: `npx skills add theplasmak/faster-whisper --skill faster-whisper`
- Source: https://github.com/theplasmak/faster-whisper
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You transcribe a meeting; You need subtitles for a video; You transcribe a podcast feed.
Skip it when: You have no local compute; The clip is under ten seconds.

# Make it a habit: New episodes transcribed on their own.

Every day, your agent runs faster-whisper on your podcast RSS feed with --skip-existing, so only new episodes are transcribed into one file each. Failed downloads retry, and a run log keeps what was done.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily feed check (schedule; cron or Claude Code routine; `0 6 * * *`)
- **Verification:** one file per episode. Hard checks: ./setup.sh --check passes; each new episode has an output file in the -o directory; the batch summary reports no failed files. On fail: retry, max 2 retries.
- **Memory:** transcripts folder at `transcripts/`. Read first: episodes already transcribed, used by --skip-existing.

## Steps

1. **Check setup.** Run ./setup.sh --check for GPU, Python, ffmpeg and yt-dlp.
2. **Fetch the feed.** Run ./scripts/transcribe with --rss, the feed URL and -o ./transcripts/.
3. **Skip done episodes.** Add --skip-existing so only new episodes run.
4. **Retry failures.** Add --retries 2 for flaky network files.
5. **Add extras on request.** Add --diarize or --format srt only when the user asked for them.
6. **Log the run.** Write the batch summary into the run log.

Stop rule: Stops after the five newest episodes per run, with two retries each.

## Permissions

- Writes: transcripts/**, loops/podcast-transcript-loop/**
- Network: hf.co
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`transcripts/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily feed check. Verification: one file per episode. Memory: transcripts/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
