---
name: ffmpeg
title: FFmpeg skill
repo: digitalsamba/claude-code-video-toolkit
license: MIT
url: https://gethabit.dev/skills/digitalsamba/ffmpeg
---

# FFmpeg skill

The ffmpeg skill gives video creators and Remotion users ready FFmpeg recipes for conversion, resizing, compression, trimming, speed changes, audio extraction and platform-specific exports.

- Install the skill: `npx skills add digitalsamba/claude-code-video-toolkit --skill ffmpeg`
- Source: https://github.com/digitalsamba/claude-code-video-toolkit/tree/HEAD/.claude/skills/ffmpeg
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you prepare assets for Remotion; you export one video for many platforms; you convert GIF to MP4.
Skip it when: you edit video on a timeline; you need live streaming setup.

# Make it a habit: Each render ready for every platform.

When Remotion writes a new out/video.mp4, your agent uses FFmpeg to export versions for YouTube, Twitter/X, LinkedIn and web embed. ffprobe confirms each file is playable and within platform limits; a run log keeps settings used.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new Remotion render (event; Claude Code routine or cron; `out/video.mp4 created or changed`)
- **Verification:** ffprobe checks every export. Hard checks: each out/video-*.mp4 file exists and is above zero bytes; ffprobe returns a video codec name for each export; Twitter export duration and size stay within the platform table limits. On fail: retry, max 1 retries.
- **Memory:** export settings log at `loops/ffmpeg-platform-export-loop/board.md`. Read first: the CRF and scale settings used last time and any export that failed.

## Steps

1. **Inspect the master.** Your agent reads duration, resolution and codecs of out/video.mp4 with ffprobe.
2. **Export per platform.** FFmpeg writes out/video-youtube.mp4, out/video-twitter.mp4, out/video-linkedin.mp4 and out/video-web.mp4 with the settings for each.
3. **Make a preview.** It renders a short out/preview.gif with a generated palette.
4. **Validate outputs.** ffprobe checks that every export has a video stream and fits the platform limits.
5. **Fix and retry.** If a file is too large it raises CRF or lowers resolution and exports again.
6. **Log the run.** The run log records settings, file sizes and any failed export.

Stop rule: Stops after one master render, four platform exports and at most one retry each.

## Permissions

- Writes: out/**, loops/ffmpeg-platform-export-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ffmpeg-platform-export-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new Remotion render. Verification: ffprobe checks every export. Memory: loops/ffmpeg-platform-export-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
