---
name: architecture-compass
title: Architecture Compass skill
repo: stark-ai-de/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/stark-ai-de/architecture-compass
---

# Architecture Compass skill

The architecture compass skill sets up ADR governance, audits architecture and drift, and plans or runs bounded refactors for teams that want binding, traceable architecture decisions in their repository.

- Install the skill: `npx skills add stark-ai-de/agent-skills --skill architecture-compass`
- Source: https://github.com/stark-ai-de/agent-skills/tree/HEAD/plugins/stark-ai-developer/skills/architecture-compass
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: you want ADR governance; reviewing a PR for architecture drift; planning a bounded refactor.
Skip it when: the change is tiny or style-only; you want general framework tutoring.

# Make it a habit: Code keeps to your ADRs.

When a pull request lands, your agent runs the read-only audit workflow: it checks the change against your accepted ADRs, ranks evidence and lists drift and risk by severity. The loop keeps each report so repeat drift stands out.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR opened or updated (event; GitHub Actions or Claude Code routine; `pull_request.opened or synchronize`)
- **Verification:** read-only audit completed. Hard checks: repository diff is empty after the audit; every finding names the ADR it conflicts with; findings listed in severity order. On fail: notify, max 0 retries.
- **Memory:** ADR drift log at `loops/architecture-drift-audit-loop/log.md`. Read first: open drift findings and the ADRs they touch.

## Steps

1. **Announce audit.** The agent shows all five workflows and selects audit, which writes nothing.
2. **Load the catalog.** It starts from references/adr-catalog.md and reads only the Short entries that apply.
3. **Inspect the change.** It reads the diff, nearest AGENTS.md or CLAUDE.md, and the accepted local ADRs.
4. **Rank evidence.** Accepted ADRs outrank current code, so a conflict is reported, not blended into a compromise.
5. **Report findings.** It lists drift and risk by severity with the decision owner, without patches.
6. **Log the run.** The loop saves the report in its own folder for the next audit.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/architecture-drift-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/architecture-drift-audit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR opened or updated. Verification: read-only audit completed. Memory: loops/architecture-drift-audit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
