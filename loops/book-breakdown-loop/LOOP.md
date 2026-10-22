---
name: story-long-analyze
title: Story Long Analyze skill
repo: zenstory-ai/oh-story-claudecode
license: MIT
url: https://gethabit.dev/skills/zenstory-ai/story-long-analyze
---

# Story Long Analyze skill

The story long analyze skill breaks down a long Chinese web novel: the first three chapters, chapter summaries, plot, emotion, rhythm, characters, settings and style, in stages that can resume. For writers studying reference books.

- Install the skill: `npx skills add zenstory-ai/oh-story-claudecode --skill story-long-analyze`
- Source: https://github.com/zenstory-ai/oh-story-claudecode/tree/HEAD/skills/story-long-analyze
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Breaking down a reference novel; Analyzing the first three chapters; Resuming a half-done breakdown.
Skip it when: Short stories; Copying another book's plot.

# Make it a habit: Reference novels broken down in stages.

When a novel text is added, the agent runs the inspector, builds the chapter index, breaks down the first three chapters, extracts summaries in batches and builds plot, character, report and style outputs. _progress.md lets runs resume.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** novel text added (event; Claude Code routine; `new 原文/原文.txt under 拆文库/`)
- **Verification:** stage checks + author. Hard checks: inspect_existing_assets.py finds the book folder; chapter_index.csv has continuous chapter numbers with no duplicates; each finished stage is marked in _progress.md; existing chapter summaries are never overwritten. On fail: stop, max 0 retries.
- **Memory:** progress file at `拆文库/{书名}/_progress.md`. Read first: which stages are done and which chapters remain.

## Steps

1. **Inspect.** The agent runs inspect_existing_assets.py on the book folder and follows recommended_path.
2. **Build the index.** It builds chapter_index.csv and checks the chapter numbers.
3. **Golden chapters.** It writes deep breakdowns of chapters 1 to 3 and 快速预览.md, then marks stage1.
4. **Ask to continue.** It stops and asks the author before the full run, unless told to go straight through.
5. **Extract batches.** It sends chapter-extractor batches, three per round, and commits the summaries.
6. **Synthesize.** It builds plot and rhythm, characters and settings, then 拆文报告.md.
7. **Style and checks.** It writes 文风.md and runs the final checks.

Stop rule: Stops after one book per run, with at most 3 extraction batches per round.

## Permissions

- Writes: 拆文库/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`拆文库/{书名}/_progress.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: novel text added. Verification: stage checks + author. Memory: 拆文库/{书名}/_progress.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
