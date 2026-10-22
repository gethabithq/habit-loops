---
name: firebase-security-rules-auditor
title: Firebase Security Rules Auditor skill
repo: firebase/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/firebase/firebase-security-rules-auditor
---

# Firebase Security Rules Auditor skill

Firebase security rules auditor is a skill that red-teams Firestore and Cloud Storage rules for bypasses, privilege escalation, missing limits and type checks, and returns a 1 to 5 score in JSON. For Firebase developers.

- Install the skill: `npx skills add firebase/agent-skills --skill firebase-security-rules-auditor`
- Source: https://github.com/firebase/agent-skills/tree/HEAD/skills/firebase-security-rules-auditor
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You review Firestore or Storage rules; You want a red-team pass before deploy; You want a score for a rules change.
Skip it when: You need to deploy or log in to the CLI; You work on Auth setup or queries.

# Make it a habit: No rules change ships unaudited.

When a pull request changes Firestore or Cloud Storage security rules, your agent red-teams them against the six-point checklist and returns a JSON score from 1 to 5 with findings. The run fails below 4. A log keeps scores and open findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** rules file changed (event; GitHub Actions; `pull_request that changes security rules`)
- **Verification:** score 4 or higher. Hard checks: the audit is valid JSON with score, summary and findings; every finding names a checklist item and a severity; no finding has severity critical or major. Critic: claude-opus-5-5, pass at 4/5. On fail: notify, max 0 retries.
- **Memory:** scores and open findings at `loops/firebase-rules-audit-loop/run-log.md`. Read first: open findings from the last audit.

## Steps

1. **Read the rules.** Read the changed Firestore or Cloud Storage rules and the app's purpose.
2. **Test update bypass.** Compare create and update rules for ways to move a valid document into a bad state.
3. **Check authority.** Flag sensitive fields like role or ownerId that trust request.resource.data.
4. **Check limits and types.** Check size limits, type checks, and that hasOnly or diff rules also check ownership.
5. **Score.** Score from 1 to 5 and return the JSON assessment with findings and fixes.

Stop rule: Stops after one audit per pull request, with no retries.

## Permissions

- Writes: loops/firebase-rules-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/firebase-rules-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: rules file changed. Verification: score 4 or higher. Memory: loops/firebase-rules-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
