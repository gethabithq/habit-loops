---
name: prompt-videos
title: Prompt Videos skill
repo: replicate/skills
license: Apache-2.0
url: https://gethabit.dev/skills/replicate/prompt-videos
---

# Prompt Videos skill

The prompt videos skill helps creators and developers write prompts for AI video models on Replicate: scene description, camera language, audio, time-coded shots, references and style.

- Install the skill: `npx skills add replicate/skills --skill prompt-videos`
- Source: https://github.com/replicate/skills/tree/HEAD/skills/prompt-videos
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You write a prompt for a video model; You build a video generation feature; You need consistent characters across clips.
Skip it when: You edit existing footage; You need image prompts only.

# Make it a habit: Video prompts that direct the shot.

When you need a video clip, your agent picks a current model with the find-models skill, writes a scene prompt with subject, camera, audio and time codes, and checks it against the common pitfalls. A character sheet keeps descriptions identical across clips.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new clip brief (manual; Claude Code routine; `run when a video clip is requested`)
- **Verification:** prompt covers all layers. Hard checks: prompt names subject, context, action, style, camera, composition and ambiance; audio is described, including ambient sound; dialogue uses a colon and the prompt says (no subtitles); character description matches the sheet word for word. On fail: retry, max 1 retries.
- **Memory:** character sheet at `loops/video-prompt-loop/characters.md`. Read first: exact character descriptions used in earlier clips.

## Steps

1. **Pick a model.** Use the find-models skill to query the Replicate API and read the schema.
2. **Describe the scene.** Layer subject, context, action, style, camera, composition and ambiance.
3. **Add audio.** Prompt dialogue, ambient sound, effects and music, sized to the clip length.
4. **Time-code shots.** For multi-shot clips, add time codes and explicit transitions.
5. **Check pitfalls.** Confirm camera motion, unchanged elements and resolution are stated.

Stop rule: Stops after one clip prompt per run, with at most one rewrite.

## Permissions

- Writes: loops/video-prompt-loop/**
- Network: replicate.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/video-prompt-loop/characters.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new clip brief. Verification: prompt covers all layers. Memory: loops/video-prompt-loop/characters.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
