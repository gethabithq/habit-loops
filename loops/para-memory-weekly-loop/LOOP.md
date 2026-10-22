---
name: para-memory-files
title: PARA Memory Files skill
repo: paperclipai/paperclip
license: MIT
url: https://gethabit.dev/skills/paperclipai/para-memory-files
---

# PARA Memory Files skill

The para memory files skill gives an agent file-based memory in three layers: a PARA knowledge graph, daily notes and tacit user patterns, with qmd for recall. For agents that must remember across sessions.

- Install the skill: `npx skills add paperclipai/paperclip --skill para-memory-files`
- Source: https://github.com/paperclipai/paperclip/tree/HEAD/skills/para-memory-files
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Your agent forgets between sessions; You want facts sorted by projects and areas; You want search over memory with qmd.
Skip it when: You need a shared database; The agent runs only one-off tasks.

# Make it a habit: Keep agent memory sorted weekly.

Each week your agent moves durable facts from daily notes into PARA entity files, rewrites each summary.md from active facts, archives inactive entities and re-indexes with qmd. Superseded facts stay, so nothing is lost.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly memory synthesis (schedule; Claude Code routine; `0 18 * * 5`)
- **Verification:** files and index check. Hard checks: no fact removed from any items.yaml; superseded facts carry superseded_by; every entity folder has summary.md and items.yaml; qmd index $AGENT_HOME exits without error. On fail: notify, max 1 retries.
- **Memory:** PARA knowledge graph at `$AGENT_HOME/life/index.md`. Read first: this week's daily notes in $AGENT_HOME/memory/ and each summary.md.

## Steps

1. **Read daily notes.** Your agent reads the week's files in $AGENT_HOME/memory/.
2. **Extract facts.** It saves durable facts to items.yaml under projects, areas or resources.
3. **Create entities.** It makes a new entity only when the skill's rules say so; otherwise the note stays daily.
4. **Rewrite summaries.** It rewrites each summary.md from the active facts.
5. **Archive and supersede.** It moves inactive entities to archives and marks old facts superseded, never deleting them.
6. **Update tacit memory.** It adds new user patterns to $AGENT_HOME/MEMORY.md.
7. **Re-index.** It runs qmd index $AGENT_HOME so recall finds the new facts.

Stop rule: Stops after one week of daily notes per run.

## Permissions

- Writes: $AGENT_HOME/life/**, $AGENT_HOME/memory/**, $AGENT_HOME/MEMORY.md
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`$AGENT_HOME/life/index.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly memory synthesis. Verification: files and index check. Memory: $AGENT_HOME/life/index.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
