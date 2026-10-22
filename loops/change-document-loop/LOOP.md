---
name: document
title: Document skill
repo: jsmastery-pro/skills
license: MIT
url: https://gethabit.dev/skills/jsmastery-pro/document
---

# Document skill

Document writes the human-facing prose about a change, a PR description, changelog entry, release note or postmortem, drafting from the real commits and diff and writing to the right place. For developers who want accurate, reader-focused change docs.

- Install the skill: `npx skills add jsmastery-pro/skills --skill document`
- Source: https://github.com/jsmastery-pro/skills/tree/HEAD/skills/document
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need a PR description; You add a changelog or release note; You write a postmortem.
Skip it when: You want code or tests written; There is no change to describe.

# Make it a habit: Every change gets human-facing prose.

When a change ships, your agent writes the human-facing document, a PR body, changelog entry, release note or postmortem, drafting from the real commits and diff, not imagination. Every sentence traces to a commit or a given fact, and it writes to the right place.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** change ready to document (event; Claude Code routine; `/document pr or on merge`)
- **Verification:** sourced + confirmed. Hard checks: every statement traces to a commit, diff or given incident fact; the document is written to the right place for its type; no gh command or push runs without your confirmation. On fail: notify, max 0 retries.
- **Memory:** commit and diff at `git log`. Read first: the branch commits, the diff against base and recent spec paths for the why.

## Steps

1. **Pick the type.** Use the given type or infer pr, changelog, release-note or postmortem, confirming with one question.
2. **Gather the source.** Collect the commit list and diff, and for a postmortem ask you for the incident facts git cannot hold.
3. **Write the document.** Read the agent prompt and the chosen template and write the document from the real record.
4. **Match the format.** Match an existing CHANGELOG style and resolve the release range from tags.
5. **Confirm before gh.** For a PR, show the body and confirm before any gh pr create, edit or push.
6. **Relay the result.** Report the type, where it landed and the full PR body in chat.

Stop rule: Stops after one document per run.

## Permissions

- Writes: CHANGELOG.md, docs/releases/**, docs/postmortems/**
- Network: none
- Sends: a PR body to GitHub after your confirmation
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`git log`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: change ready to document. Verification: sourced + confirmed. Memory: git log. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
