---
name: recall
title: Recall skill
repo: rohitg00/agentmemory
license: Apache-2.0
url: https://gethabit.dev/skills/rohitg00/recall
---

# Recall skill

The recall skill searches agentmemory for past observations, sessions and learnings with hybrid BM25, vector and graph search, so developers get real context from earlier sessions without invented answers.

- Install the skill: `npx skills add rohitg00/agentmemory --skill recall`
- Source: https://github.com/rohitg00/agentmemory/tree/HEAD/plugin/skills/recall
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You ask what we did about something; You need context from past sessions; You check if a problem was seen before.
Skip it when: agentmemory is not installed; You want to save, not search.

# Make it a habit: Past context before new work.

When you ask what we did about a topic, your agent searches agentmemory with memory_smart_search, expands the chosen ids, groups results by session with high importance first, and never invents a match. A log keeps queries that found nothing.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you ask about past work (event; Claude Code routine; `user message asks to recall or what we did about a topic`)
- **Verification:** only returned results shown. Hard checks: every shown observation comes from the tool response; ids are expanded with expandIds before full content is quoted; results are grouped by session with importance 7 or more first; an empty search returns 2-3 alternative search terms. On fail: stop, max 0 retries.
- **Memory:** recall query log at `loops/memory-recall-loop/queries.md`. Read first: earlier queries that matched nothing and the terms tried.

## Steps

1. **Search.** Call memory_smart_search with the question as query and limit 10, plus project, agentId or targetLayer when scoped.
2. **Expand the ids.** Call memory_smart_search again with expandIds and the same filters before quoting any full content.
3. **Group by session.** Show type, title and narrative per session, with provenance only when the response gives it.
4. **Lead with importance.** Put observations with importance 7 or higher at the top.
5. **Check the budget.** With memory_recall, read matched_count, excluded_by_budget and content_truncated before calling a result empty.
6. **Handle no match.** If nothing matched, suggest 2-3 other search terms and stop without guessing.

Stop rule: Stops after one search question and at most 10 results.

## Permissions

- Writes: loops/memory-recall-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/memory-recall-loop/queries.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you ask about past work. Verification: only returned results shown. Memory: loops/memory-recall-loop/queries.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
