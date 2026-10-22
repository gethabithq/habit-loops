---
name: brag
title: Brag skill
repo: latent-spaces/brag
license: MIT
url: https://gethabit.dev/skills/latent-spaces/brag
---

# Brag skill

The brag skill turns your project website or app into a short, shareable launch video with Hyperframes. It reads the code, plans a storyboard in a chosen tone, renders the video and writes share copy. For builders who want to show what they made.

- Install the skill: `npx skills add latent-spaces/brag --skill brag`
- Source: https://github.com/latent-spaces/brag/tree/HEAD/skills/brag
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You shipped something and want a launch video; You want a short clip for social posts; You have no screenshots or live URL ready.
Skip it when: You need a long tutorial video; Your project has no visual product to show.

# Make it a habit: A short launch video per release.

When you tag a release, your agent reads the project code, plans a 15 to 25 second brag video, builds it with Hyperframes, checks it, renders brag.mp4 with a poster frame and writes share copy. Each run keeps its own timestamped output folder.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new release tag (event; Claude Code routine; `push tags: v*`)
- **Verification:** check passes, files exist. Hard checks: brag-plan.md exists and scene durations sum to 15 to 25 seconds; npx hyperframes check passes with zero errors; brag.mp4 exists; brag.jpg poster exists and share-copy.txt is written. On fail: retry, max 1 retries.
- **Memory:** past brag plans at `loops/launch-video-loop/run-log.md`. Read first: tones and angles of earlier videos and their output folders.

## Steps

1. **Parse options.** The agent reads the options such as --tone, --format, --duration and --voice.
2. **Inspect the project.** It scans the code until it can answer all 9 questions of the planning rubric.
3. **Plan the storyboard.** It writes brag-plan.md with a hook, scenes, text, timing, transitions and sound cues.
4. **Compose.** It writes a brief and builds the video in composition/ with the hyperframes-core, hyperframes-animation, hyperframes-creative, hyperframes-keyframes and hyperframes-cli skills.
5. **Check.** It runs npx hyperframes check and fixes errors until zero.
6. **Render and deliver.** It renders brag.mp4, picks the best poster as brag.jpg, bakes it as frame 0 and writes share-copy.txt.

Stop rule: Stops after one video per release and at most 1 retry of a failed check.

## Permissions

- Writes: brag-output*/**, loops/launch-video-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/launch-video-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new release tag. Verification: check passes, files exist. Memory: loops/launch-video-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
