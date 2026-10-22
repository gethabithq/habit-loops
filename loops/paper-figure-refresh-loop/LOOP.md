---
name: academic-plotting
title: Academic Plotting skill
repo: orchestra-research/ai-research-skills
license: MIT
url: https://gethabit.dev/skills/orchestra-research/academic-plotting
---

# Academic Plotting skill

Academic plotting is a skill for ML researchers that makes publication-quality paper figures: data charts with matplotlib and seaborn, and architecture diagrams generated with Gemini, sized for venues like NeurIPS and ICML.

- Install the skill: `npx skills add orchestra-research/ai-research-skills --skill academic-plotting`
- Source: https://github.com/orchestra-research/ai-research-skills/tree/HEAD/20-ml-paper-writing/academic-plotting
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need a figure for a paper; Your results changed before a deadline; You need an architecture diagram.
Skip it when: You need interactive charts; You draw diagrams in TikZ by hand.

# Make it a habit: Paper figures rebuilt from latest results.

When experiment results change, your agent picks the chart type from the data, rebuilds each data figure with matplotlib or seaborn using a saved script and exports PDF and PNG. Diagrams go through Gemini with three attempts.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** results file changes (event; Claude Code routine; `event: new CSV or JSON results in the repo`)
- **Verification:** figures and scripts exist. Hard checks: figures/gen_fig_<name>.py exists for every figure; each data figure has fig_<name>.pdf and a 300 DPI PNG; the generation script runs without error. On fail: retry, max 2 retries.
- **Memory:** figure scripts folder at `figures/`. Read first: existing gen_fig scripts, chosen style and palette.

## Steps

1. **Read the context.** Read the results or paper section and find methods, metrics and comparisons.
2. **Pick the workflow.** Use matplotlib for numeric axes and Gemini for boxes-and-arrows diagrams.
3. **Choose the chart.** Pick line, grouped bar, scatter, heatmap or horizontal bar from the data shape.
4. **Apply styling.** Use the publication defaults, a colorblind-safe palette and a distinct color for our method.
5. **Generate diagrams.** For diagrams, write the six-section prompt and run three attempts with GEMINI_API_KEY from the environment.
6. **Export and save.** Save the script as figures/gen_fig_<name>.py and export PDF and PNG.

Stop rule: Stops after five figures per run, with two retries each.

## Permissions

- Writes: figures/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`figures/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: results file changes. Verification: figures and scripts exist. Memory: figures/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
