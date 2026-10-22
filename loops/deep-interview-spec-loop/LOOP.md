---
name: deep-interview
title: Deep Interview skill
repo: yeachan-heo/oh-my-claudecode
license: MIT
url: https://gethabit.dev/skills/yeachan-heo/deep-interview
---

# Deep Interview skill

The deep interview skill runs a Socratic requirements interview with ambiguity scoring and writes a spec before any code is written. For developers using oh-my-claudecode who start from vague ideas.

- Install the skill: `npx skills add yeachan-heo/oh-my-claudecode --skill deep-interview`
- Source: https://github.com/yeachan-heo/oh-my-claudecode/tree/HEAD/skills/deep-interview
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Your idea is still vague; You want no wrong assumptions; The task is large and unclear.
Skip it when: You already have a detailed request; You want a quick single fix.

# Make it a habit: Vague ideas become clear specs.

When you start a vague idea, your agent interviews you one question at a time, scores ambiguity after every answer and stops only below the threshold. It writes the spec to .omc/specs and keeps interview state in .omc/state so it can resume.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you run deep-interview (manual; Claude Code; `/deep-interview <idea>`)
- **Verification:** ambiguity below threshold. Hard checks: ambiguity score is at or below the resolved threshold, or early exit is marked; spec file exists at .omc/specs/deep-interview-{slug}.md; spec has topology, acceptance criteria and clarity breakdown. On fail: retry, max 0 retries.
- **Memory:** interview state file at `.omc/state/deep-interview-state.json`. Read first: last completed round and its scores.

## Steps

1. **Resolve the threshold.** Your agent reads omc.deepInterview.ambiguityThreshold from the settings files, or uses the default.
2. **Explore the code.** For an existing repo it runs the explore agent and reads related specs in .omc/specs.
3. **Confirm the topology.** It lists the top-level parts of your idea and asks you to confirm them.
4. **Interview you.** It asks one question per round at the weakest dimension and shows the ambiguity score.
5. **Challenge assumptions.** Contrarian, Simplifier and Ontologist modes each run once at set rounds.
6. **Write the spec.** It writes the spec to .omc/specs/deep-interview-{slug}.md and marks it pending approval.
7. **You pick next.** You choose omc-plan consensus, autopilot, ralph, team or more questions; nothing runs before that.

Stop rule: Stops at the resolved threshold, on early exit after round 3, or at the hard cap of 20 rounds.

## Permissions

- Writes: .omc/specs/**, .omc/state/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.omc/state/deep-interview-state.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you run deep-interview. Verification: ambiguity below threshold. Memory: .omc/state/deep-interview-state.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
