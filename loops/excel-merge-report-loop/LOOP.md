---
name: office-automation
title: Office Automation skill
repo: texiaoyao/office-automation-skill
license: MIT
url: https://gethabit.dev/skills/texiaoyao/office-automation
---

# Office Automation skill

The office automation skill gives an agent Python scripts to read, write, fill and format Word .docx files and to read, merge, convert and analyze Excel sheets. For people who process office documents in batches.

- Install the skill: `npx skills add texiaoyao/office-automation-skill --skill office-automation`
- Source: https://github.com/texiaoyao/office-automation-skill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You merge many Excel files; You fill Word templates with data; You convert Excel to CSV.
Skip it when: Your files are old .doc format; You need live collaborative editing.

# Make it a habit: One merged sheet every week.

Each Friday your agent merges the Excel files in one folder with excel_processor.py merge, reads the result back to confirm it holds data, and fills a Word report template with word_processor.py template. A run log keeps which files were merged.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Friday afternoon (schedule; cron or Claude Code routine; `0 16 * * 5`)
- **Verification:** merged file has rows. Hard checks: merged.xlsx exists after the merge; excel_processor.py read on merged.xlsx returns at least one row; the filled .docx report exists. On fail: notify, max 1 retries.
- **Memory:** merged files log at `loops/excel-merge-report-loop/run-log.md`. Read first: files merged last week and their row counts.

## Steps

1. **Read the log.** Your agent checks which files it merged last time.
2. **Merge the sheets.** It runs excel_processor.py merge on the folder with --output merged.xlsx.
3. **Read it back.** It runs excel_processor.py read on the merged file to confirm it holds data.
4. **Analyze the data.** It runs excel_processor.py analyze with --pivot for a short summary.
5. **Fill the report.** It runs word_processor.py template with --data to fill the weekly report.
6. **Log the run.** It writes the file names and row counts to the run log.

Stop rule: Stops after one folder per run and one retry; files over 100MB are left for a split run.

## Permissions

- Writes: loops/excel-merge-report-loop/**, merged.xlsx, *.docx
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/excel-merge-report-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Friday afternoon. Verification: merged file has rows. Memory: loops/excel-merge-report-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
