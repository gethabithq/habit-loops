---
name: huggingface-llm-trainer
title: Hugging Face LLM Trainer skill
repo: huggingface/skills
license: Apache-2.0
url: https://gethabit.dev/skills/huggingface/huggingface-llm-trainer
---

# Hugging Face LLM Trainer skill

The hugging face llm trainer skill fine-tunes language and vision models with TRL or Unsloth on Hugging Face Jobs, with SFT, DPO, GRPO, dataset validation, Trackio monitoring and GGUF conversion, for builders without a local GPU.

- Install the skill: `npx skills add huggingface/skills --skill huggingface-llm-trainer`
- Source: https://github.com/huggingface/skills/tree/HEAD/skills/huggingface-llm-trainer
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You fine-tune without a local GPU; You run SFT, DPO or GRPO; You need a GGUF export.
Skip it when: You train on your own GPUs; Your account has no Jobs access.

# Make it a habit: Fine-tuned models saved to Hub.

When you ask for a training run, your agent validates the dataset, writes a TRL script with Trackio, sets a long enough timeout and Hub push, and submits it with hf_jobs. A run log keeps job IDs, settings and failures for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** training run requested (manual; Claude Code; `on request to train or fine-tune a model`)
- **Verification:** dataset ready, push set. Hard checks: dataset inspector shows READY or mapping applied; push_to_hub=True and hub_model_id are set; secrets include HF_TOKEN; timeout is set above the default. On fail: stop, max 0 retries.
- **Memory:** training job log at `loops/hf-finetune-run-loop/log.md`. Read first: past job IDs, hardware, timeouts and failure modes.

## Steps

1. **Check the login.** Confirm authentication with hf_whoami and a token with write access.
2. **Validate the dataset.** Run the dataset inspector and apply mapping code if it says NEEDS MAPPING.
3. **Pick model and hardware.** Use hf_benchmarks.py for a base model and match the flavor to model size.
4. **Offer an estimate.** Offer estimate_cost.py for time and a recommended timeout with buffer.
5. **Write the script.** Base it on train_sft_example.py or a DPO or GRPO template, with Trackio.
6. **Submit the job.** Submit inline with hf_jobs, with timeout and HF_TOKEN in secrets.
7. **Report and log.** Give the job ID and monitoring URL, then wait for the user to ask for status.

Stop rule: Stops after one submitted job per run; no automatic status polling.

## Permissions

- Writes: loops/hf-finetune-run-loop/**
- Network: huggingface.co
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/hf-finetune-run-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: training run requested. Verification: dataset ready, push set. Memory: loops/hf-finetune-run-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
