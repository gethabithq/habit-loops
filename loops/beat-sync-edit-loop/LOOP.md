---
name: beat-sync-editing
title: Beat-Sync Editing skill
repo: iart-ai/motion-design-skills
license: MIT
url: https://gethabit.dev/skills/iart-ai/beat-sync-editing
---

# Beat-Sync Editing skill

The beat-sync editing skill turns music and story structure into frame-accurate cut points, transitions and speed ramps, for editors and motion designers working in an NLE, Remotion or After Effects.

- Install the skill: `npx skills add iart-ai/motion-design-skills --skill beat-sync-editing`
- Source: https://github.com/iart-ai/motion-design-skills/tree/HEAD/skills/beat-sync-editing
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: cutting footage to a music track; fixing pacing that drags; planning speed ramps and match cuts.
Skip it when: single static frames; choosing easing curves only.

# Make it a habit: Every cut lands on beat.

When a new track and footage are ready, your agent writes an edit-timing plan: BPM to frames, phrase cuts, a pacing arc, motivated transitions and speed ramps as frame numbers. Beat markers are checked against detected beat seconds. Plans are logged.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** track and footage ready (event; Claude Code routine; `new edit brief with BPM and fps`)
- **Verification:** beat sync verified. Hard checks: frames_per_beat computed from (60/BPM)*fps and rounded cumulatively; every cut is an absolute frame number; cut markers match detected beat seconds via frame/fps; the arc has Establish, Develop, Climax and Resolve phases. On fail: retry, max 2 retries.
- **Memory:** edit plans at `loops/beat-sync-edit-loop/plans.md`. Read first: BPM, offsets and personality of earlier edits.

## Steps

1. **Find the grid.** Your agent captures BPM, fps and the beat-1 offset and computes frames per beat.
2. **Pick the personality.** It maps the chosen motion personality to phrase length and transition family.
3. **Shape the arc.** It sets frame ranges for each phase and shortens shots toward the climax.
4. **List the cuts.** It places cuts on 2, 4 or 8 beat phrases and the biggest visual on the drop.
5. **Add transitions.** It defaults to hard cuts and gives J and L cuts audio offsets in frames.
6. **Plan retimes.** It writes speed ramps as eased time-remap keyframes landing on the beat.
7. **Verify sync.** It checks frame/fps against detected beat seconds.

Stop rule: Stops after one edit plan per run and at most two sync retries.

## Permissions

- Writes: loops/beat-sync-edit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/beat-sync-edit-loop/plans.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: track and footage ready. Verification: beat sync verified. Memory: loops/beat-sync-edit-loop/plans.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
