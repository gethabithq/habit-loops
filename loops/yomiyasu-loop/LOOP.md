---
name: yomiyasu
title: yomiyasu skill
repo: nanaism/yomiyasu
license: MIT
url: https://gethabit.dev/skills/nanaism/yomiyasu
---

# yomiyasu skill

The yomiyasu skill edits AI-written Japanese into natural prose. It keeps meaning and certainty, fixes strange metaphors and vague subjects, and checks the result with a bundled linter and diff tool. For writers and teams publishing in Japanese.

- Install the skill: `npx skills add nanaism/yomiyasu --skill yomiyasu`
- Source: https://github.com/nanaism/yomiyasu/tree/HEAD/skills/yomiyasu
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You publish Japanese text drafted by AI; Drafts read stiff or full of odd metaphors; You need edits that keep the original meaning.
Skip it when: The text is not in Japanese; You only want spelling unified.

# Make it a habit: Natural Japanese in every draft.

When a new Japanese draft lands, your agent runs yomiyasu on it: lint first, then a careful rewrite that keeps meaning, then the bundled lint and diff check and a hash verify. The final goes beside the original and the run is logged.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new Japanese draft added (event; Claude Code routine; `new .md or .txt draft in the writing folder`)
- **Verification:** lint, diff, hash verify. Hard checks: yomiyasu_check.py run finishes on source and final; verify reports the hash matches the record; original file is unchanged; final saved under a new file name. On fail: retry, max 1 retries.
- **Memory:** polished drafts log at `loops/yomiyasu-loop/runs.md`. Read first: drafts already polished and open questions for the writer.

## Steps

1. **Pick the draft.** Take the new .md or .txt file, skipping instruction files like AGENTS.md, CLAUDE.md and earlier .material.txt extracts.
2. **Read the context.** Decide document type, reader and stance, then load the matching references/doc-types and references/domains files.
3. **Lint the original.** Run yomiyasu_lint.py on the source to collect candidate spots before rewriting.
4. **Rewrite carefully.** Fix odd metaphors, unclear subjects and copy-style phrasing while keeping claim, weight, certainty and sentence role.
5. **Run the check.** Save the final as a separate file and run yomiyasu_check.py run with --source and --final.
6. **Fix once.** Review the diff candidates, correct once, and run the check again.
7. **Verify and log.** Run verify --final on the file and note changes and writer questions in the log.

Stop rule: Stops after one draft per run and at most one fix round.

## Permissions

- Writes: <final draft next to the original, new name>, loops/yomiyasu-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/yomiyasu-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new Japanese draft added. Verification: lint, diff, hash verify. Memory: loops/yomiyasu-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
