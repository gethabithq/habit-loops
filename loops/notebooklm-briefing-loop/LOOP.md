---
name: notebooklm
title: NotebookLM skill
repo: teng-lin/notebooklm-py
license: MIT
url: https://gethabit.dev/skills/teng-lin/notebooklm
---

# NotebookLM skill

The notebooklm skill drives Gemini Notebook through the notebooklm-py CLI or Python API: notebook and source management, grounded chat, research and artifact generation such as audio or reports, for researchers and builders.

- Install the skill: `npx skills add teng-lin/notebooklm-py --skill notebooklm`
- Source: https://github.com/teng-lin/notebooklm-py
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You manage Gemini Notebook sources; You want audio or report artifacts; You automate grounded research.
Skip it when: You need the generic Gemini API; You need unrelated content creation.

# Make it a habit: Weekly sources become one briefing.

Once a week, your agent adds new sources to a Gemini Notebook through the notebooklm CLI, waits until each is ready, then asks a grounded question or generates an artifact after your OK. Hard checks gate on auth, ready sources and a completed artifact; a board keeps every ID.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly source briefing (schedule; Claude Code routine or cron; `0 8 * * 1`)
- **Verification:** ready gates and your OK. Hard checks: notebooklm auth check --test --json returns status ok and token_fetch true; every source wait exits 0 with status ready; artifact wait exits 0 and the artifact status is completed; the downloaded file exists and is not empty. On fail: notify, max 0 retries.
- **Memory:** notebook IDs and sources at `loops/notebooklm-briefing-loop/board.md`. Read first: the notebook ID, source IDs already added and the last artifact ID.

## Steps

1. **Check auth.** The agent runs the auth check with --test and --json and stops unless it reports ok.
2. **Add new sources.** Each new input goes in with source add, pinned to the notebook ID, and its source ID is kept.
3. **Wait for ready.** It runs source wait for every new source and goes on only when all are ready.
4. **Ask for approval.** Before generation, long waits or downloads that were not already authorized, it asks you to confirm.
5. **Ask or generate.** It runs an ID-pinned ask for analysis, or generate with the chosen type, such as audio or report.
6. **Wait and download.** It runs artifact wait on the exact artifact ID, then downloads only that artifact.
7. **Log the IDs.** Notebook, source and artifact IDs and their status go onto the board.

Stop rule: Stops after one notebook and one generated artifact per run; failed generation is not retried without your OK.

## Permissions

- Writes: loops/notebooklm-briefing-loop/**, the downloaded artifact file
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/notebooklm-briefing-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly source briefing. Verification: ready gates and your OK. Memory: loops/notebooklm-briefing-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
