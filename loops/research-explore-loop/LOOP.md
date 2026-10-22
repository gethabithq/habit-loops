---
name: ai-research-explore
title: AI Research Explore skill
repo: lllllllama/RigorPilot-Skills
license: MIT
url: https://gethabit.dev/skills/lllllllama/ai-research-explore
---

# AI Research Explore skill

The ai research explore skill runs candidate-only deep learning research on top of a current_research anchor, with repo understanding, idea gates, fair comparison and governed experiments in explore_outputs/. For researchers who already fixed task, dataset and evaluation.

- Install the skill: `npx skills add lllllllama/RigorPilot-Skills --skill ai-research-explore`
- Source: https://github.com/lllllllama/RigorPilot-Skills/tree/HEAD/skills/ai-research-explore
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You test new model variants; You run a bounded sweep; You need auditable experiment records.
Skip it when: You want a trusted reproduction; You have not chosen task and evaluation.

# Make it a habit: One ranked research candidate per run.

When you authorize exploration on a current_research anchor, your agent freezes task, dataset and evaluation, gates ideas, runs one bounded candidate and ranks it on real evidence. Outputs and the scientific changelog land in explore_outputs/.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you authorize exploration (manual; Claude Code; `explicit candidate-only request with a current_research anchor`)
- **Verification:** evidence + checkpoint. Hard checks: current_research anchor exists before any candidate work; evaluation_source and sota_reference stay unchanged in the campaign; the candidate smoke check passes; SCIENTIFIC_CHANGELOG.md and COMPARABILITY_REPORT.md are written. On fail: stop, max 0 retries.
- **Memory:** scientific changelog at `explore_outputs/SCIENTIFIC_CHANGELOG.md`. Read first: past candidates, their evidence and comparison limits.

## Steps

1. **Confirm the anchor.** The agent confirms current_research and your explicit candidate-only authorization.
2. **Freeze the campaign.** It freezes task, dataset, benchmark, evaluation source, SOTA reference and compute budget.
3. **Understand the repo.** It builds only the repo artifacts it needs, usually with analyze-project.
4. **Gate ideas.** It keeps your ideas, may add a few single-variable ones and ranks them with explicit gates.
5. **Run one candidate.** It uses explore-code or explore-run, and minimal-run-and-audit or run-train only when real execution is needed.
6. **Rank on evidence.** It ranks by command status, metrics and smoke results, and stops for your checkpoint when top ideas are too close.
7. **Write outputs.** scripts/write_outputs.py writes candidate-only results, never as trusted reproduction.

Stop rule: Stops after one candidate per inner loop, or when the compute_budget is used up.

## Permissions

- Writes: analysis_outputs/**, sources/**, explore_outputs/**, an isolated branch or worktree
- Network: optional web lookup for sources
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`explore_outputs/SCIENTIFIC_CHANGELOG.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you authorize exploration. Verification: evidence + checkpoint. Memory: explore_outputs/SCIENTIFIC_CHANGELOG.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
