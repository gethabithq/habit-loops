---
name: open-code-review-delegate
title: Open Code Review Delegate skill
repo: alibaba/open-code-review
license: Apache-2.0
url: https://gethabit.dev/skills/alibaba/open-code-review-delegate
---

# Open Code Review Delegate skill

The open code review delegate skill uses the ocr CLI for file selection and review rules while the host agent does the code review itself, file by file, with required coverage reporting. For teams using Alibaba's open-code-review.

- Install the skill: `npx skills add alibaba/open-code-review --skill open-code-review-delegate`
- Source: https://github.com/alibaba/open-code-review/tree/HEAD/plugins/open-code-review/skills/open-code-review-delegate
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You review a branch with ocr; You want rule-based reviews per file; You need review coverage numbers.
Skip it when: ocr is not installed; You want OCR to call its own LLM.

# Make it a habit: Review every changed file, report coverage.

On each pull request, your agent runs ocr delegate preview to pick reviewable files, ocr delegate rule for their rules, reads each diff with git, reviews every file against its rule group and reports findings by severity with full coverage numbers.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions or Claude Code routine; `pull_request.opened or new commits on a branch`)
- **Verification:** full coverage check. Hard checks: every reviewable file is marked reviewed or skipped with a reason; report includes total_files, reviewed_files, skipped_files and coverage_rate; each comment has path and content. On fail: retry, max 1 retries.
- **Memory:** review coverage log at `loops/ocr-delegated-review-loop/reviews.md`. Read first: files skipped last time and recurring finding categories.

## Steps

1. **Preview.** Your agent runs ocr delegate preview --format json with --from and --to for the branch.
2. **Get rules.** It runs ocr delegate rule --format json on the reviewable paths.
3. **Get diffs.** It reads each diff with git --no-pager diff --no-ext-diff --no-textconv --no-color.
4. **Review each file.** It reviews every file against its rule group and marks it reviewed or skipped.
5. **Format comments.** It writes comments with path, content, lines, category and severity.
6. **Report.** It groups findings by severity and reports coverage numbers.

Stop rule: Stops after one pull request per run, in batches of 20 files.

## Permissions

- Writes: loops/ocr-delegated-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ocr-delegated-review-loop/reviews.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: full coverage check. Memory: loops/ocr-delegated-review-loop/reviews.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
