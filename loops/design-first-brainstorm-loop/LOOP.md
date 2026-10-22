---
name: brainstorming
title: Brainstorming skill
repo: obra/superpowers
license: MIT
url: https://gethabit.dev/skills/obra/brainstorming
---

# Brainstorming skill

The brainstorming skill makes an agent find out what you want and why before building: it reads your project, asks one question at a time, lays out approaches, writes a design doc and waits for approval. For anyone starting new work with an agent.

- Install the skill: `npx skills add obra/superpowers --skill brainstorming`
- Source: https://github.com/obra/superpowers/tree/HEAD/skills/brainstorming
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You start a new feature or project; Your request leaves big questions open; You want a design doc before code.
Skip it when: The request is fully clear, like a color change; You only want a throwaway spike.

# Make it a habit: No build before an approved design.

Whenever you ask for something new, your agent first reads your project, asks one question at a time, lays out two or three approaches for you to pick, writes a short or full design doc, gets it reviewed and approved, then hands off to writing-plans.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new feature request (event; Claude Code; `a request to create, add or change behavior`)
- **Verification:** your approval of the doc. Hard checks: design doc exists with an Approaches part; you approved the design doc before any code, scaffolding or install; for a project, the builder check came back before handover. On fail: stop, max 0 retries.
- **Memory:** committed design docs at `docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md`. Read first: earlier design docs for the same area.

## Steps

1. **Look first.** The agent reads what you pointed at and the code it touches before its first message.
2. **Ask one question.** Each message ends with one specific question, with an offer to just dive in if you did not ask for brainstorming.
3. **Play it back.** As each part becomes clear, it describes that part back and asks what is wrong or missing.
4. **Lay out approaches.** In a message of its own it presents two or three ways to build it, recommends one and lets you pick.
5. **Write the design.** It sizes the work and writes a short or full design doc, committed under docs/superpowers/specs/ in a repo.
6. **Builder check.** For a project, a fresh subagent reads the doc with builder-check-prompt.md and the agent brings back only your questions.
7. **Approve and plan.** After you approve the doc, the agent invokes superpowers:writing-plans and no other skill.

Stop rule: Stops after one design doc per request and one round of builder-check questions.

## Permissions

- Writes: docs/superpowers/specs/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new feature request. Verification: your approval of the doc. Memory: docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
