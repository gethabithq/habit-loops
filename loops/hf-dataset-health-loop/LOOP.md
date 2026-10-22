---
name: huggingface-datasets
title: Hugging Face Datasets skill
repo: huggingface/skills
license: Apache-2.0
url: https://gethabit.dev/skills/huggingface/huggingface-datasets
---

# Hugging Face Datasets skill

The hugging face datasets skill lets an agent explore datasets through the Dataset Viewer API: splits, row pages, text search, filters, parquet links, size and statistics, plus upload flows. For ML engineers working with Hub datasets.

- Install the skill: `npx skills add huggingface/skills --skill huggingface-datasets`
- Source: https://github.com/huggingface/skills/tree/HEAD/skills/huggingface-datasets
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You explore a Hub dataset; You need parquet links or row counts; You search or filter dataset rows.
Skip it when: Your data is not on the Hub; You need SQL over parquet.

# Make it a habit: Spot dataset changes every week.

Each week your agent calls the Hugging Face Dataset Viewer API for your datasets: /is-valid, /splits, /size and /statistics, all read-only. It compares row totals with the last run and keeps them in a run log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday at nine (schedule; Claude Code routine or cron; `0 9 * * 1`)
- **Verification:** dataset valid, rows counted. Hard checks: /is-valid reports the dataset as valid; /splits returns at least one config and split; /size returns a row total above zero. On fail: notify, max 1 retries.
- **Memory:** dataset size log at `loops/hf-dataset-health-loop/run-log.md`. Read first: last row totals per dataset and split.

## Steps

1. **Read the log.** Your agent loads the dataset list and last week's totals.
2. **Validate datasets.** It calls /is-valid for each dataset.
3. **Resolve splits.** It calls /splits to get each config and split.
4. **Read size and stats.** It calls /size and /statistics, with a bearer token for gated or private datasets.
5. **Preview rows.** It calls /first-rows to confirm rows still come back.
6. **Compare and log.** It compares totals with the last run and writes changes to the log.

Stop rule: Stops after at most 10 datasets per run and one retry each.

## Permissions

- Writes: loops/hf-dataset-health-loop/**
- Network: datasets-server.huggingface.co
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/hf-dataset-health-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday at nine. Verification: dataset valid, rows counted. Memory: loops/hf-dataset-health-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
