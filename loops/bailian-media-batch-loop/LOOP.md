---
name: bailian-gen
title: Bailian Gen skill
repo: modelstudioai/cli
license: Apache-2.0
url: https://gethabit.dev/skills/modelstudioai/bailian-gen
---

# Bailian Gen skill

The bailian gen skill lets an agent make and understand images, video and speech on Alibaba Cloud Bailian with the bl CLI: text-to-image, image edits, text-to-video, TTS, speech recognition and video understanding. For creators who want media from prompts.

- Install the skill: `npx skills add modelstudioai/cli --skill bailian-gen`
- Source: https://github.com/modelstudioai/cli/tree/HEAD/skills/bailian-gen
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You need images from a prompt; You want a short video clip; You need text-to-speech or transcripts.
Skip it when: The task is plain chat or code; You train your own model.

# Make it a habit: Media requests become saved files.

When a new list of media requests arrives, your agent makes each image, video or speech file with the bl CLI, saves it locally and checks the file exists. It asks once before the first Bailian call and logs each output path.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new media request list (event; Claude Code routine; `new request file in the media folder`)
- **Verification:** files saved, one consent. Hard checks: each bl command exits without error; every output file exists at its path; video jobs finished and were downloaded. On fail: notify, max 1 retries.
- **Memory:** media output log at `loops/bailian-media-batch-loop/runs.md`. Read first: requests already done and their output paths.

## Steps

1. **Read the protocol.** The agent reads the shared bailian-protocol file for consent and setup.
2. **Ask once.** If you did not name Bailian, it asks once before the first call in the task.
3. **Make images.** It runs bl image generate or bl image edit with --out-dir.
4. **Make video and speech.** It runs bl video generate with --download and bl speech synthesize with --out.
5. **Check files.** It checks that each output file exists.
6. **Summarise.** It writes a one-line summary of the bl commands used and the file paths to the log.

Stop rule: Stops after 10 requests and one retry per request.

## Permissions

- Writes: loops/bailian-media-batch-loop/**, ./out/
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/bailian-media-batch-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new media request list. Verification: files saved, one consent. Memory: loops/bailian-media-batch-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
