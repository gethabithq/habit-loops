---
name: media-use
title: Media Use skill
repo: heygen-com/hyperframes
license: Apache-2.0
url: https://gethabit.dev/skills/heygen-com/media-use
---

# Media Use skill

The media use skill by heygen-com gets or makes media for HyperFrames videos: music, sound effects, images, logos, voiceover, avatars, transcripts, cutouts and colour grades, with HeyGen or free local tools.

- Install the skill: `npx skills add heygen-com/hyperframes --skill media-use`
- Source: https://github.com/heygen-com/hyperframes/tree/HEAD/skills/media-use
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Your video needs music or voice; Footage looks dark or flat; You need logos or icons.
Skip it when: You do not use HyperFrames; All media is already in place.

# Make it a habit: Fill media gaps in every video.

When a HyperFrames video is built or reviewed, your agent scans once for media gaps like silent cuts or placeholder images, offers the fixes in one ask, then resolves each file into assets/. A check confirms every resolved file exists locally.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** video built or reviewed (event; Claude Code routine; `a HyperFrames piece is built or reviewed`)
- **Verification:** resolved files + your OK. Hard checks: each resolve call prints a resolved line with a path; every resolved file exists in assets/; media-use resolve --doctor reports the setup works. On fail: notify, max 1 retries.
- **Memory:** media gaps board at `loops/media-gap-loop/board.md`. Read first: gaps offered before, fixes you accepted and gaps you said to leave.

## Steps

1. **Scan for gaps.** Your agent looks once for text with no voiceover, emoji icons, placeholder images, silent cuts, long stretches without music and colour casts.
2. **Offer once.** It lists the specific fixes in one ask, and respects leave it.
3. **Reuse first.** It lists reusable assets with resolve --candidates and judges the fit.
4. **Resolve media.** It runs npx hyperframes media-use resolve with a type and intent, via HeyGen or the free local tools.
5. **Confirm paid calls.** Before a paid call it chose itself, such as an avatar video, it asks you first.
6. **Treat footage.** For dark, flat or dull footage it uses npx hyperframes media-treatment, never CSS stand-ins.
7. **Log the gaps.** It records which gaps were filled or declined on the board.

Stop rule: Stops after one ask and at most 10 resolved files per run.

## Permissions

- Writes: assets/**, loops/media-gap-loop/**
- Network: HeyGen (when signed in), Openverse
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/media-gap-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: video built or reviewed. Verification: resolved files + your OK. Memory: loops/media-gap-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
