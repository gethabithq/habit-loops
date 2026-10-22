---
name: sound-effects
title: ElevenLabs Sound Effects skill
repo: elevenlabs/skills
license: MIT
url: https://gethabit.dev/skills/elevenlabs/sound-effects
---

# ElevenLabs Sound Effects skill

The elevenlabs sound effects skill generates sound effects from text with the ElevenLabs API: ambient textures, cinematic impacts and UI sounds, with duration, looping and prompt influence control, for developers and creators.

- Install the skill: `npx skills add elevenlabs/skills --skill sound-effects`
- Source: https://github.com/elevenlabs/skills/tree/HEAD/sound-effects
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need UI or game sounds; You want looping ambient audio; You need a cinematic impact.
Skip it when: You need spoken voice; You have no ElevenLabs API key.

# Make it a habit: Every listed sound gets generated.

When new sound requests land in the loop's list, your agent turns each one into an ElevenLabs sound effect with set duration, loop and prompt influence. A hard check confirms each audio file exists and the call returned no error, and the list keeps what is done.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new sound request listed (event; Claude Code routine; `new line added to loops/sound-effects-loop/board.md`)
- **Verification:** audio file exists, no error. Hard checks: output audio file exists and is not empty; duration_seconds is between 0.5 and 30 or left on auto; prompt_influence is between 0 and 1; the call returned no 401, 422 or 429 error. On fail: retry, max 2 retries.
- **Memory:** sound request board at `loops/sound-effects-loop/board.md`. Read first: open sound requests and the settings used for finished ones.

## Steps

1. **Read the board.** The agent picks the open sound requests from the board.
2. **Sharpen the prompt.** Each request gets a specific description with elements, style and mood.
3. **Set parameters.** It chooses duration_seconds, prompt_influence, loop and an output format for each sound.
4. **Generate.** It calls the text to sound effects convert function through the SDK or the elevenlabs CLI.
5. **Check the file.** The hard checks confirm the file is there and no error came back.
6. **Update the board.** Finished sounds move to done with their prompt and settings.

Stop rule: Stops after ten sounds per run, with at most two retries per sound.

## Permissions

- Writes: loops/sound-effects-loop/**, the generated audio files
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/sound-effects-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new sound request listed. Verification: audio file exists, no error. Memory: loops/sound-effects-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
