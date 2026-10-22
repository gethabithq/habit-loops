---
name: sendcutsend
title: SendCutSend skill
repo: earthtojake/text-to-cad
license: MIT
url: https://gethabit.dev/skills/earthtojake/sendcutsend
---

# SendCutSend skill

The sendcutsend skill gives makers and engineers a careful preflight report for DXF and STEP uploads, measuring the file and comparing it to the current catalog, specs and ordering guide for cutting, bending and other services.

- Install the skill: `npx skills add earthtojake/text-to-cad --skill sendcutsend`
- Source: https://github.com/earthtojake/text-to-cad/tree/HEAD/skills/sendcutsend
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You plan a SendCutSend order; You export a DXF with bend lines; You want to check a STEP file for CNC routing.
Skip it when: You order from another fabrication shop; You need the model designed, not reviewed.

# Make it a habit: Every part file gets preflighted.

When a DXF or STEP export changes, your agent fetches the current SendCutSend sources, measures the exact upload file and writes a preflight report with pass, fail or need more info per check. You confirm the order context when it is unclear. A log keeps past reports.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** DXF or STEP changed (event; GitHub Actions or Claude Code routine; `push touches **/*.dxf, **/*.step or **/*.stp`)
- **Verification:** you confirm + cited checks. Hard checks: every findings row has a Rule source or says Direct file inspection; no ready verdict if official sources could not be fetched; no ready verdict while any required check is fail or need more info. On fail: notify, max 0 retries.
- **Memory:** past preflight reports at `loops/sendcutsend-preflight-loop/run-log.md`. Read first: the last report per file, its confirmed SKU and services, and the edits it asked for.

## Steps

1. **Collect order intent.** The agent records file type, process, material or SKU, thickness, quantity, services, finish and hardware.
2. **Confirm with you.** If the order context is missing or unclear, it shows candidate SKUs with source links and asks you to choose.
3. **Fetch the sources.** It reads references/official-sources.md and fetches the ordering guide, catalog JSON and specs JSON fresh.
4. **Measure the file.** It inspects the exact upload file with the cad skill if present, else with build123d or ezdxf, reporting facts only.
5. **Compare evidence.** It compares only trustworthy pairs of source requirement and measured fact, including local flange depth along each bend.
6. **Draw the problem.** For each fail it makes a diagnostic image if image tools exist, or describes the intended diagram.
7. **Write the report.** It writes findings ordered by impact with a Rule source column and specific next edits, then logs the result.

Stop rule: Stops after one upload file per run, with no retries.

## Permissions

- Writes: loops/sendcutsend-preflight-loop/**
- Network: sendcutsend.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/sendcutsend-preflight-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: DXF or STEP changed. Verification: you confirm + cited checks. Memory: loops/sendcutsend-preflight-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
