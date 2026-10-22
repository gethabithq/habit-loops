---
name: watch
title: Watch skill
repo: bradautomates/claude-video
license: MIT
url: https://gethabit.dev/skills/bradautomates/watch
---

# Watch skill

The watch skill lets your agent watch a video from a URL or local file: it downloads with yt-dlp, extracts frames with ffmpeg, pulls the transcript, or lets Gemini watch the whole video, then answers your question with timestamps.

- Install the skill: `npx skills add bradautomates/claude-video --skill watch`
- Source: https://github.com/bradautomates/claude-video/tree/HEAD/skills/watch
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You have questions about a video; You want notes from a talk or tutorial; You need what a presenter showed on screen.
Skip it when: A text article covers the same content; The video must stay private and local setup is not possible.

# Make it a habit: Saved videos turned into timestamped notes.

When you add a video URL to your watch list, your agent runs the watch skill with your question, reads every listed frame or the Gemini answer, and writes timestamped notes. It logs which videos are done and what evidence was missing.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** video added to list (event; Claude Code routine; `new line in loops/video-watch-digest-loop/queue.md`)
- **Verification:** setup ok, evidence read. Hard checks: setup.py --check exits 0; watch.py writes a report for the video; every frame listed in the report is read; a Gemini failure stops the run instead of switching engines. On fail: notify, max 0 retries.
- **Memory:** video queue and notes at `loops/video-watch-digest-loop/queue.md`. Read first: videos still waiting and earlier notes.

## Steps

1. **Check setup.** Your agent runs setup.py --check, and on a first run asks you the engine, detail and transcription questions.
2. **Take the next video.** It picks the next URL or local path and the question from the queue.
3. **Watch.** It runs watch.py with the source and --question as separate quoted arguments.
4. **Read the evidence.** It relays the Gemini answer with timestamps, or reads every frame and the transcript on the local engine.
5. **Handle failures.** On a Gemini failure it tells you and offers --engine local instead of switching by itself.
6. **Write notes.** It writes timestamped notes, names missing evidence and marks the video done.
7. **Clean up.** It removes only the disposable work dir from this run.

Stop rule: Stops after 3 videos per run with no automatic retries.

## Permissions

- Writes: loops/video-watch-digest-loop/**, ~/.config/watch/.env
- Network: the video source site, generativelanguage.googleapis.com when the gemini engine is on
- Sends: video to Google only with the gemini engine
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/video-watch-digest-loop/queue.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: video added to list. Verification: setup ok, evidence read. Memory: loops/video-watch-digest-loop/queue.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
