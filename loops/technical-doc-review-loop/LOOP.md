---
name: technical-writing
title: Technical Writing skill
repo: riekelt/technical-writer
license: MIT
url: https://gethabit.dev/skills/riekelt/technical-writing
---

# Technical Writing skill

The technical writing skill gives your agent a house style for specs, design docs, READMEs, reference docs and reports: conclusion first, every claim sourced, one fact in one place and a list of banned constructions. For teams that keep docs in the repository.

- Install the skill: `npx skills add riekelt/technical-writer --skill technical-writing`
- Source: https://github.com/riekelt/technical-writer/tree/HEAD/plugins/technical-writer/skills/technical-writing
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write a spec or design doc; You update docs to match code; You review a README before merge.
Skip it when: Marketing copy or social posts; UI microcopy.

# Make it a habit: Docs stay sourced, current and plain.

When a pull request adds or changes a technical document, your agent classifies it, checks the hard rules and grounds each claim in a source. It runs the reviewing-technical-prose pass, follows every reference and logs open issues per document.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes a document (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*.md`)
- **Verification:** hard rules pass. Hard checks: no em dash, en dash or ' -- ' in the document; no changelog section or 'last updated' field; all headings are in sentence case; every reference resolves when followed; a new document is listed in the folder's README.md if one exists. On fail: retry, max 1 retries.
- **Memory:** open issues per document at `loops/technical-doc-review-loop/run-log.md`. Read first: documents with unsourced claims or open issues.

## Steps

1. **Read first.** Your agent reads up to two comparable documents and checks whether the topic already has an owner.
2. **Classify.** It sorts the document as normative, descriptive, historical, runbook or reference and applies that edit rule.
3. **Fill the checkpoint.** It notes kind, audience, purpose and non-goals in working notes.
4. **Load the type skill.** It adds the matching sibling skill, such as writing-runbooks or writing-design-docs.
5. **Ground claims.** It traces each claim to code, a test or a source, or names the gap.
6. **Check hard rules.** It removes dashes, history narrative and Title Case headings.
7. **Final review.** It runs reviewing-technical-prose and follows every reference before delivery.

Stop rule: Stops after 5 documents per run and 1 retry each.

## Permissions

- Writes: docs/**, **/README.md, loops/technical-doc-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/technical-doc-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes a document. Verification: hard rules pass. Memory: loops/technical-doc-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
