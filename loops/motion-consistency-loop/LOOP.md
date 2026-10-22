---
name: motion-art-direction
title: Motion Art Direction skill
repo: iart-ai/motion-design-skills
license: MIT
url: https://gethabit.dev/skills/iart-ai/motion-art-direction
---

# Motion Art Direction skill

The motion art direction skill makes the creative calls for a motion graphics piece: tone, pacing, a motion-language spec, motion hierarchy, restraint and a consistency check across shots. For designers and agents directing animated video.

- Install the skill: `npx skills add iart-ai/motion-design-skills --skill motion-art-direction`
- Source: https://github.com/iart-ai/motion-design-skills/tree/HEAD/skills/motion-art-direction
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: a motion piece has no look yet; animation feels busy or inconsistent; you guide gsap or lottie work.
Skip it when: you need keyframe craft only; the project has no motion.

# Make it a habit: Every shot follows one motion language.

When a new shot or cut is ready, the agent audits it against the project's motion-language spec: one easing family, durations on the base unit, one transition family, one hero per frame. It records pass or fail per shot in the spec file.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new shot ready (event; Claude Code routine; `new or changed shot direction notes`)
- **Verification:** per-shot consistency audit. Hard checks: every duration is a multiple of the base timing unit; no more than two easing curves in use; only the chosen transition family between shots; exactly one hero element per frame. Critic: claude-opus-5-5, pass at 17/20. On fail: notify, max 1 retries.
- **Memory:** motion-language spec at `loops/motion-consistency-loop/spec.md`. Read first: the filled motion-language spec and per-shot pass or fail list.

## Steps

1. **Read the spec.** Load the filled spec with easing family, base timing unit, transition family, stagger, intensity and holds.
2. **Lock it first.** If no spec exists yet, run the brief, tone matrix and personality steps to fill it once.
3. **Rank the hierarchy.** Sort the shot's elements into hero, support and texture tiers.
4. **Restraint pass.** Cut motion that carries no meaning and list what stays still.
5. **Audit the shot.** Check easing, durations, transitions, stagger, holds and the single hero against the spec.
6. **Record the result.** Write pass or fail per shot and the defects to fix before polish.

Stop rule: One cut per run, at most 30 shots audited.

## Permissions

- Writes: loops/motion-consistency-loop/
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/motion-consistency-loop/spec.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new shot ready. Verification: per-shot consistency audit. Memory: loops/motion-consistency-loop/spec.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
