---
name: remember
title: Remember skill
repo: rohitg00/agentmemory
license: Apache-2.0
url: https://gethabit.dev/skills/rohitg00/remember
---

# Remember skill

The remember skill saves an insight, decision or learning to agentmemory long-term storage with specific concept tags and file paths, so developers can find it again in later sessions.

- Install the skill: `npx skills add rohitg00/agentmemory --skill remember`
- Source: https://github.com/rohitg00/agentmemory/tree/HEAD/plugin/skills/remember
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You say remember this; A decision should outlive the session; You want searchable project facts.
Skip it when: You want a behavior rule, use lesson; agentmemory is not installed.

# Make it a habit: Every decision saved with tags.

When you say remember this or note that, your agent saves the insight to agentmemory with memory_save, tags 2-5 specific concepts and real file paths, and echoes the tags back. A run log keeps what was saved.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you say remember this (event; Claude Code routine; `user message asks to remember, save or note something`)
- **Verification:** save confirmed with concepts. Hard checks: memory_save returns a saved memory id; between 2 and 5 lowercased concepts are tagged; every tagged file path exists in the repo; the confirmation echoes the exact concepts. On fail: retry, max 1 retries.
- **Memory:** saved memories log at `loops/memory-save-loop/saved.md`. Read first: concepts already used for earlier saves.

## Steps

1. **Find the insight.** Take the core fact, decision or learning out of the request.
2. **Tag concepts.** Pick 2-5 specific lowercased concept phrases, never generic ones like code or notes.
3. **Collect file paths.** Add only file paths the insight really refers to, or leave the field empty.
4. **Save it.** Call memory_save with content, concepts and files, plus agentId in a multi-agent setup.
5. **Confirm the tags.** Tell the user the save worked and repeat the concepts they can search for.
6. **Correct old facts.** To change a fact, save the corrected version so it replaces the old record.

Stop rule: Stops after one saved memory per request and one retry.

## Permissions

- Writes: loops/memory-save-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/memory-save-loop/saved.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you say remember this. Verification: save confirmed with concepts. Memory: loops/memory-save-loop/saved.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
