---
name: story-short-write
title: Story Short Write skill
repo: zenstory-ai/oh-story-claudecode
license: MIT
url: https://gethabit.dev/skills/zenstory-ai/story-short-write
---

# Story Short Write skill

The story short write skill helps writers of Chinese short web fiction go from an idea to a finished story, built around one target emotion, a section outline and pacing checks.

- Install the skill: `npx skills add zenstory-ai/oh-story-claudecode --skill story-short-write`
- Source: https://github.com/zenstory-ai/oh-story-claudecode/tree/HEAD/skills/story-short-write
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Writing a short story from an idea; Planning a twist; Checking a draft's pacing.
Skip it when: Long serial novels; Only removing AI tone.

# Make it a habit: Short stories from emotion to draft.

For each short story, the agent asks for the target emotion, designs 设定.md and 小节大纲.md, writes 正文.md scene by scene and passes the Phase 3 gate with check-ai-patterns.js and check-degeneration.js before polishing. Design files carry state.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** author starts a story (manual; Claude Code routine; `/story-short-write`)
- **Verification:** author + Phase 3 gate. Hard checks: check-ai-patterns.js --check --fail-on=blocking reports no blocking hit; check-degeneration.js --check reports no blocking hit; the section count equals the plan in 小节大纲.md; the word count is inside the locked target range. On fail: retry, max 2 retries.
- **Memory:** story design files at `设定.md`. Read first: target emotion, word range, platform, red lines and rejected ideas.

## Steps

1. **Set the emotion.** The agent asks the author how readers should feel at the end.
2. **Design.** It reads the design references and writes 设定.md and 小节大纲.md.
3. **Read before drafting.** It reads references/workflow-draft.md in full.
4. **Draft scenes.** It writes 正文.md section by section from the outline.
5. **Pass the gate.** It checks word count, section count and both checker scripts, and reworks on failure.
6. **Polish.** It reads references/workflow-revision.md and runs the final pass.

Stop rule: Stops after one story per run, with at most 2 rework rounds at the gate.

## Permissions

- Writes: 设定.md, 小节大纲.md, 正文.md
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`设定.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: author starts a story. Verification: author + Phase 3 gate. Memory: 设定.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
