---
name: humanizer-zh
title: Humanizer-zh skill
repo: op7418/Humanizer-zh
license: MIT
url: https://gethabit.dev/skills/op7418/humanizer-zh
---

# Humanizer-zh skill

Humanizer-zh is an editing skill for Chinese articles, comments and docs. It removes filler, repetition and formulaic phrases while it keeps facts, certainty and the author's voice. For writers and teams who polish existing Chinese text.

- Install the skill: `npx skills add op7418/Humanizer-zh --skill humanizer-zh`
- Source: https://github.com/op7418/Humanizer-zh
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A Chinese draft sounds stiff or formulaic; You polish docs without changing facts; You want to keep the author's voice.
Skip it when: You need to prove who wrote a text; The text is not in Chinese.

# Make it a habit: Chinese drafts read natural, facts kept.

When a Chinese draft changes in your docs folder, your agent edits empty phrases and template wording with humanizer-zh. A diff check makes sure code, links, front matter and headings stay the same, and a log keeps which files were polished.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Chinese draft changed (event; GitHub Actions or Claude Code routine; `push touching docs/**/*.md`)
- **Verification:** protected parts unchanged. Hard checks: code blocks, inline code, paths and URLs are byte-identical to the original; YAML front matter is unchanged; heading count and heading text are unchanged; no new numbers or dates appear that are not in the original. Critic: claude-opus-5-5, pass at 17/20. On fail: retry, max 1 retries.
- **Memory:** polished files log at `loops/chinese-prose-polish-loop/runs.md`. Read first: files already polished and the voice notes per author.

## Steps

1. **Read the draft.** The agent reads the whole text, notes its genre and the claims, numbers and limits it must keep.
2. **Fix real problems.** It changes only phrases that are empty, repeated or unclear, using the 31 patterns as hints.
3. **Compare with original.** It checks that no claim was added, lost or made stronger, and that negation, scope and attribution match.
4. **Read it through.** It reads the result again for tone and flow and leaves smooth parts alone.
5. **Run final checklist.** It walks the pre-delivery checklist and takes back any detail not found in the source.
6. **Log the file.** It records the file and the voice notes in the run log.

Stop rule: Stops after 5 changed files per run, with at most 1 retry per file.

## Permissions

- Writes: docs/**/*.md, loops/chinese-prose-polish-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/chinese-prose-polish-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Chinese draft changed. Verification: protected parts unchanged. Memory: loops/chinese-prose-polish-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
