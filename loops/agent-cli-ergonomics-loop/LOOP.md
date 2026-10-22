---
name: axi
title: AXI skill
repo: kunchenguid/axi
license: MIT
url: https://gethabit.dev/skills/kunchenguid/axi
---

# AXI skill

Axi defines Agent eXperience Interface standards for CLI tools agents use through the shell: TOON output, minimal schemas, truncation, structured errors, exit codes, session hooks and fast version checks. For developers building agent-facing CLIs.

- Install the skill: `npx skills add kunchenguid/axi --skill axi`
- Source: https://github.com/kunchenguid/axi/tree/HEAD/.agents/skills/axi
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a CLI for agents; You review CLI output for token cost; You add session hooks to a tool.
Skip it when: Your CLI is only for humans; You build a GUI app.

# Make it a habit: Agent-facing CLIs stay AXI-compliant.

On every pull request to an agent-facing CLI, your agent checks the AXI standards: TOON output, minimal schemas, truncation with totals, definitive empty states, structured errors on stdout, unknown-flag rejection and a fast --version. A log keeps open violations.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** CLI code changes (event; GitHub Actions or Claude Code routine; `pull_request paths: src/**, bin/**`)
- **Verification:** flag and exit checks. Hard checks: an unknown flag exits with code 2 and lists valid flags; --version, -v and -V print the bare version and exit 0; running the CLI with no arguments prints live content, not usage; the version fast-path test passes. On fail: notify, max 0 retries.
- **Memory:** AXI violation log at `loops/agent-cli-ergonomics-loop/log.md`. Read first: open AXI violations per command.

## Steps

1. **Read the TOON spec.** Read the TOON specification before judging output.
2. **Check output.** Check TOON on stdout, 3-4 default fields, truncation with total size and total counts in lists.
3. **Check empty states.** Make sure empty results state the zero with context.
4. **Check errors.** Make sure errors go to stdout with a fix hint, mutations are idempotent and no prompts appear.
5. **Check flags and help.** Run an unknown flag, --help and --version and check exit codes and output.
6. **Log violations.** Record each violation with the command and the AXI section it breaks.

Stop rule: Stops after the changed commands of one pull request, at most 20 commands.

## Permissions

- Writes: loops/agent-cli-ergonomics-loop/**
- Network: toonformat.dev
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/agent-cli-ergonomics-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: CLI code changes. Verification: flag and exit checks. Memory: loops/agent-cli-ergonomics-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
