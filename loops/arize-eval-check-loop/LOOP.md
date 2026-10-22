---
name: arize-evaluator
title: Arize Evaluator skill
repo: arize-ai/arize-skills
license: MIT
url: https://gethabit.dev/skills/arize-ai/arize-evaluator
---

# Arize Evaluator skill

The arize evaluator skill creates LLM-as-judge and code evaluators on Arize with the ax CLI, wires column mappings, and runs evaluation tasks on spans or experiments. For teams that monitor LLM app quality.

- Install the skill: `npx skills add arize-ai/arize-skills --skill arize-evaluator`
- Source: https://github.com/arize-ai/arize-skills/tree/HEAD/skills/arize-evaluator
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need a hallucination or correctness judge; You want to score spans or experiments; You set up continuous monitoring.
Skip it when: You do not use Arize; You only need a one-time manual review.

# Make it a habit: Score new spans every week.

Each week your agent triggers an Arize evaluation task with ax tasks trigger-run on a capped span window, waits for it, and checks that spans were really scored. Failures are reported, never replaced by guessed scores. A run log keeps task ids and results.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine or cron; `0 7 * * 1`)
- **Verification:** spans scored, not zero. Hard checks: ax tasks get-run shows the run completed; scored span count is above zero; every template variable has a column mapping. On fail: notify, max 1 retries.
- **Memory:** eval task run log at `loops/arize-eval-check-loop/run-log.md`. Read first: task id, last data window and last scores.

## Steps

1. **Read the log.** Your agent loads the task id and the window it scored last time.
2. **Pick evaluator once.** On the first run it samples spans with ax spans export and lets you choose one of a few evaluator ideas.
3. **Check mappings.** It exports a few spans and confirms each template variable maps to a real field.
4. **Trigger the run.** It calls ax tasks trigger-run with --max-spans and --wait on a window that ended at least two hours ago.
5. **Check the result.** ax tasks get-run must show a completed run with scored spans.
6. **Report honestly.** If the run fails or scores nothing, the agent reports the error instead of inventing scores.

Stop rule: Stops after one task run of at most 100 spans and one retry.

## Permissions

- Writes: loops/arize-eval-check-loop/**
- Network: app.arize.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/arize-eval-check-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: spans scored, not zero. Memory: loops/arize-eval-check-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
