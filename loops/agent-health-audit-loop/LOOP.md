---
name: health
title: Health skill
repo: tw93/Waza
license: MIT
url: https://gethabit.dev/skills/tw93/health
---

# Health skill

Health audits your agent setup and AI coding maintainability: config, instruction drift, hooks, MCP, skills and verifiers, for developers whose Claude, Codex or Pi agent ignores rules or behaves oddly.

- Install the skill: `npx skills add tw93/Waza --skill health`
- Source: https://github.com/tw93/Waza/tree/HEAD/plugins/waza/skills/health
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Your agent ignores instructions; Hooks or MCP seem broken; You suspect AI coding code rot.
Skip it when: You need to fix an app bug; You want a pull request review.

# Make it a habit: Weekly agent setup health report.

Each week your agent runs the health collector in summary mode, checks agent config, instruction drift, hooks, MCP and AI maintainability, and writes a report-only list of findings with actions. The next run compares against the last report.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly health audit (schedule; Claude Code routine; `0 9 * * 1`)
- **Verification:** collector + finding format. Hard checks: collect-data.sh runs and prints the summary sections; every finding names its layer, evidence and a copy-pasteable action; no secret appears unless shown as [REDACTED]; no project test, build or installer was run. On fail: notify, max 1 retries.
- **Memory:** last health report at `loops/agent-health-audit-loop/report.md`. Read first: open findings and global items already reported once.

## Steps

1. **Set the scope.** Use instructions for a static-only request, otherwise auto, and keep it when escalating.
2. **Collect.** Run collect-data.sh, or run-health.ps1 on Windows, in summary mode.
3. **Check runtime.** Inventory hooks and MCP servers and probe only servers that are already connected.
4. **Check safety.** Run the deny-list, environment override and skill supply chain checks.
5. **Ask before escalating.** Tell the user before a deep audit, and ask before calling a hook broken.
6. **Analyse.** Sort findings into critical, structural and incremental, with evidence for each.
7. **Report.** Write the health report and report global findings only once.

Stop rule: One summary audit per run, with at most three recent sessions scanned unless the user asks for a deep audit.

## Permissions

- Writes: loops/agent-health-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/agent-health-audit-loop/report.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly health audit. Verification: collector + finding format. Memory: loops/agent-health-audit-loop/report.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
