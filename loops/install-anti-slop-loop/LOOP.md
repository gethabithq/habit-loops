---
name: install-anti-slop
title: Install Anti-Slop skill
repo: dmmulroy/anti-slop
license: MIT
url: https://gethabit.dev/skills/dmmulroy/install-anti-slop
---

# Install Anti-Slop skill

The install anti-slop skill installs, updates or migrates the vendored anti-slop Oxlint plugins in a repository, enables their rules and records provenance, for teams who want stricter lint rules against sloppy code.

- Install the skill: `npx skills add dmmulroy/anti-slop --skill install-anti-slop`
- Source: https://github.com/dmmulroy/anti-slop/tree/HEAD/skills/install-anti-slop
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add anti-slop lint rules to a repo; You pick up upstream rule fixes; You migrate an existing vendored copy.
Skip it when: Your project does not use Oxlint or Vite+; You want a managed npm lint package.

# Make it a habit: Lint rules stay current, customizations kept.

Once a month your agent checks the vendored anti-slop Oxlint plugin, installs it fresh or follows the update procedure, enables the rules, runs lint and typecheck, and records the copied source in UPSTREAM.md for the next update.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly upstream check (schedule; Claude Code routine or GitHub Actions; `0 9 1 * *`)
- **Verification:** lint, typecheck, provenance. Hard checks: the repository's lint command passes or every finding is reported; typecheck passes; oxlint and @oxlint/plugins have the same exact version; UPSTREAM.md exists beside the vendored entry point; a second fix and format pass leaves files unchanged. On fail: notify, max 0 retries.
- **Memory:** UPSTREAM.md provenance record at `tools/oxlint/anti-slop/UPSTREAM.md`. Read first: source commit, installed paths and intentional local deviations.

## Steps

1. **Choose the path.** Read the agent instructions, git status, package manager and Oxlint or Vite+ config, and find any existing anti-slop copy referenced by jsPlugins.
2. **Update or install.** Follow references/update.md for an existing copy, or run scripts/install.mjs for a fresh install into tools/oxlint/anti-slop/, and ask you to confirm the target if an update finds no copy.
3. **Match dependencies.** Install @oxlint/plugins pinned to the installed oxlint version, or query npm view for both when oxlint is missing.
4. **Register and enable.** Merge the ignore patterns and jsPlugins entry into the config and enable all generic rules at error, plus Effect rules only with a direct effect dependency.
5. **Run checks.** Run the repository's lint command and typecheck, or vp check for Vite+, without suppressing rules or weakening severity.
6. **Record provenance.** Write the source repository, exact commit, installed paths and deviations into UPSTREAM.md, or mark them unknown.
7. **Report the diff.** Review the final diff and report the path, source identity, config changes and check results.

Stop rule: Stops after one install or update of one repository per run; findings in owned source are reported, not fixed, unless you asked for cleanup.

## Permissions

- Writes: tools/oxlint/anti-slop/**, oxlint.config.ts, .oxlintrc.json, package.json, lockfile
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`tools/oxlint/anti-slop/UPSTREAM.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly upstream check. Verification: lint, typecheck, provenance. Memory: tools/oxlint/anti-slop/UPSTREAM.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
