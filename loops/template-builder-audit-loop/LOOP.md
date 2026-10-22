---
name: template-builder-ui
title: Template Builder UI skill
repo: sentdm/sent-plugin
license: MIT
url: https://gethabit.dev/skills/sentdm/template-builder-ui
---

# Template Builder UI skill

The template builder ui skill designs and audits tenant-facing Sent template editors: draft model, variable entities, validation, SMS, WhatsApp and RCS previews, lifecycle states and safe review submission. For product teams building on Sent.

- Install the skill: `npx skills add sentdm/sent-plugin --skill template-builder-ui`
- Source: https://github.com/sentdm/sent-plugin/tree/HEAD/claude-plugins/sent/skills/template-builder-ui
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you build a template editor; you audit template validation UX; you map editor state to Sent payloads.
Skip it when: you only write one template; you need WABA onboarding.

# Make it a habit: Template editors save valid Sent payloads.

When a pull request changes the template builder, the agent audits it against the Sent v3 definition model, the validation matrix, channel previews and the save and review rules. It runs the waba-template-author linter on serialized drafts and logs every gap.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes template builder (event; GitHub Actions or Claude Code routine; `pull request touching the template editor`)
- **Verification:** linter + audit checklist. Hard checks: waba-template-author linter passes on serialized draft JSON; saved payload has no top-level name, channels, body, header or buttons; save keeps submit_for_review false and never autosubmits; every body is limited to 1,024 characters. On fail: notify, max 0 retries.
- **Memory:** builder audit log at `loops/template-builder-audit-loop/log.md`. Read first: open gaps from the last audit.

## Steps

1. **Read open gaps.** Load the gaps the last audit found from the log.
2. **Check product model.** Confirm one draft object built on definition.body.multiChannel with optional complete overrides.
3. **Check variable UX.** Make sure inserting a variable creates a placeholder and a matching entity that renumber together.
4. **Check validation rules.** Compare limits and button rules with references/template-validation-matrix.md.
5. **Run the linter.** Serialize sample drafts and run the waba-template-author linter on them.
6. **Check save and review.** Confirm sandbox validation, draft save and an explicit review step with previews and warnings.
7. **Check accessibility.** Confirm field-linked errors, no color-only previews and preserved edits after failures.
8. **Log the gaps.** Write each gap with the file it lives in.

Stop rule: One pull request per run, one full audit pass.

## Permissions

- Writes: loops/template-builder-audit-loop/
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/template-builder-audit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes template builder. Verification: linter + audit checklist. Memory: loops/template-builder-audit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
