---
name: storage-analyzer
title: Storage Analyzer skill
repo: kkkkhazix/khazix-skills
license: MIT
url: https://gethabit.dev/skills/kkkkhazix/storage-analyzer
---

# Storage Analyzer skill

The storage analyzer skill scans a macOS or Windows disk read-only, sorts big space users into three cleanup tiers with steps, and builds an interactive HTML report for people whose disk is nearly full.

- Install the skill: `npx skills add kkkkhazix/khazix-skills --skill storage-analyzer`
- Source: https://github.com/kkkkhazix/khazix-skills/tree/HEAD/storage-analyzer
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: your disk is almost full; you want cleanup suggestions; you wonder what uses the space.
Skip it when: you mean RAM, not storage; you want silent automatic deletion.

# Make it a habit: Know what fills your disk.

Every month your agent runs a read-only disk scan with scan.py, sorts large items into auto-clean, judge-yourself and careful tiers, and builds an HTML report. It keeps a short history so you can see which folders grow.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly disk scan (schedule; cron or Claude Code routine; `0 10 1 * *`)
- **Verification:** scan and report exist. Hard checks: /tmp/storage_scan.json exists and is valid JSON; every green item has trash_paths; report HTML file exists; no rm or mv command ran. On fail: notify, max 1 retries.
- **Memory:** storage size history at `loops/disk-storage-report-loop/history.md`. Read first: top 5 space users and tier totals from last month.

## Steps

1. **Scan read-only.** The agent runs python3 scripts/scan.py and saves the output to /tmp/storage_scan.json.
2. **Read the platform guide.** It reads references/macos.md or references/windows.md to match the system.
3. **Find top users.** It names the top 5 space users and traces unclear folders such as UUID containers with ls or du.
4. **Sort into tiers.** Each item with a cleanup decision goes into green, yellow or red with estimated size and steps.
5. **Build the report.** It writes the analysis JSON and runs scripts/build_report.py to create a static HTML report.
6. **Summarize and log.** You get a short summary of the biggest wins and risks, and the totals go into the history.

Stop rule: Stops after one scan and one report per run.

## Permissions

- Writes: /tmp/storage_scan.json, /tmp/storage_analysis.json, ~/Desktop/storage-report.html, loops/disk-storage-report-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/disk-storage-report-loop/history.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly disk scan. Verification: scan and report exist. Memory: loops/disk-storage-report-loop/history.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
