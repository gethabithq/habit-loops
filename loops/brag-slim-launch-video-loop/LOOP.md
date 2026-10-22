---
name: brag-slim
title: Brag Slim skill
repo: latent-spaces/brag
license: MIT
url: https://gethabit.dev/skills/latent-spaces/brag-slim
---

# Brag Slim skill

The brag slim skill turns a project folder or a website URL into a short launch video with music, motion, a poster frame and share copy, for builders who want to show what they made without video tools.

- Install the skill: `npx skills add latent-spaces/brag --skill brag-slim`
- Source: https://github.com/latent-spaces/brag/tree/HEAD/skills/brag-slim
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You shipped a project or feature; You want a short launch video; You need postable share copy.
Skip it when: You need a long tutorial video; The project has nothing visible to show.

# Make it a habit: A launch video per release.

When a project ships something new, your agent runs /brag-slim: it reads the code or site, writes brag-plan.md, renders brag.mp4 with poster and share-copy.txt, checks length and files, and logs the angle and tone used.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new feature or release (event; Claude Code routine; `a release or new feature is marked done in the project`)
- **Verification:** stills, files and you. Hard checks: brag.mp4 runs between 15 and 25 seconds; brag.jpg and share-copy.txt exist next to the video; storyboard durations in brag-plan.md sum to the target; no secrets, emails or real user names in the plan or share copy. On fail: retry, max 1 retries.
- **Memory:** past angles and tones at `loops/brag-slim-launch-video-loop/run-log.md`. Read first: angles, tones and hooks used in earlier videos so the next one differs.

## Steps

1. **Inspect the source.** Read the project code or the live site for copy, colors, fonts and the main flow, skipping secrets and build output.
2. **Answer the questions.** Decide what it is, who it is for, the hook, the tone and the share caption, and ask the user if the input is unclear.
3. **Write the plan.** Save brag-plan.md with angle, highlights, punchline and a timed storyboard.
4. **Build and preview.** Build the scenes with the tools on the machine and fix overflow and contrast in stills before rendering.
5. **Render and deliver.** Render brag.mp4 into brag-output/, set brag.jpg as frame 0 and write share-copy.txt.
6. **Offer a re-roll.** Tell the user where the files are and offer another tone or a new scene.
7. **Log the run.** Write the angle, tone and duration to the run log.

Stop rule: One video per run; at most one re-render after the stills check.

## Permissions

- Writes: brag-output/**, loops/brag-slim-launch-video-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/brag-slim-launch-video-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new feature or release. Verification: stills, files and you. Memory: loops/brag-slim-launch-video-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
