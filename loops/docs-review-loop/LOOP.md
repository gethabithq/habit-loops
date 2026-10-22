---
name: reviewing-technical-prose
title: Reviewing Technical Prose skill
repo: riekelt/technical-writer
license: MIT
url: https://gethabit.dev/skills/riekelt/reviewing-technical-prose
---

# Reviewing Technical Prose skill

The reviewing technical prose skill is a review pass for technical documents, with a severity scale, a findings format, a list of patterns not to flag and a delivery checklist, for writers and reviewers checking docs before they ship.

- Install the skill: `npx skills add riekelt/technical-writer --skill reviewing-technical-prose`
- Source: https://github.com/riekelt/technical-writer/tree/HEAD/plugins/technical-writer/skills/reviewing-technical-prose
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Reviewing someone else's technical text; Writing a review report on a document; Final check before a document ships.
Skip it when: Reviewing code; Reopening decisions already settled.

# Make it a habit: Every doc reviewed before it ships.

When a pull request changes a document, the agent reviews the full text, rates each finding BLOCKER, WARNING or OBS and runs the delivery checklist. Findings go into a review report, and a re-review lists only what is still open.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes a document (event; GitHub Actions; `pull_request with changed .md files`)
- **Verification:** delivery checklist. Hard checks: no em dashes, en dashes or ' -- ' in the prose; every relative link, chapter number and file name in the document exists; no changelog section or last updated field; zero BLOCKER findings remain open. On fail: notify, max 0 retries.
- **Memory:** review findings log at `loops/docs-review-loop/reviews.md`. Read first: open findings from the last review of each document.

## Steps

1. **Load background.** The agent reads the technical-writing skill with references/style.md and references/truth.md.
2. **Read it whole.** It reviews the full document, never a summary of it.
3. **Rate findings.** Each defect gets BLOCKER, WARNING or OBS.
4. **Skip false alarms.** Patterns on the leave-alone list are only flagged when several signs meet in one paragraph.
5. **Write the report.** The verdict comes first, then each finding with location, proposed fix and confidence.
6. **Run the checklist.** It walks the delivery checklist line by line before the document ships.

Stop rule: Stops after one pull request and at most 5 documents per run.

## Permissions

- Writes: loops/docs-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/docs-review-loop/reviews.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes a document. Verification: delivery checklist. Memory: loops/docs-review-loop/reviews.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
