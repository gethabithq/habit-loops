---
name: huggingface-gradio
title: Hugging Face Gradio skill
repo: huggingface/skills
license: Apache-2.0
url: https://gethabit.dev/skills/huggingface/huggingface-gradio
---

# Hugging Face Gradio skill

The hugging face gradio skill helps Python developers build Gradio web UIs, demos and chatbots with Interface, Blocks and ChatInterface, and call running apps with the gradio CLI.

- Install the skill: `npx skills add huggingface/skills --skill huggingface-gradio`
- Source: https://github.com/huggingface/skills/tree/HEAD/skills/huggingface-gradio
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You build a Gradio demo or chatbot; You wire Blocks events and layouts; An agent must call a Space.
Skip it when: Your UI is not written in Python; You need a full custom frontend.

# Make it a habit: Your Gradio endpoints keep answering.

Each morning your agent runs gradio info on the Spaces you list, then sends one stored sample payload per endpoint with gradio predict. It checks that each reply holds the expected output keys and logs every result.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning at seven (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** endpoints answer with outputs. Hard checks: gradio info returns at least one endpoint per Space; gradio predict returns JSON with the named output keys; no endpoint parameter list changed since the last run. On fail: notify, max 1 retries.
- **Memory:** endpoint run log at `loops/gradio-space-check-loop/runs.md`. Read first: the endpoints and parameters seen on the last run.

## Steps

1. **Read the log.** The agent loads the endpoints and parameters it saw last time.
2. **Discover endpoints.** gradio info lists every endpoint of each Space with its parameters and return values.
3. **Compare signatures.** Missing endpoints or changed parameters get flagged against the log.
4. **Send samples.** gradio predict sends one stored payload per endpoint, with --token for private Spaces.
5. **Check outputs.** Each reply must be a JSON object with the named output keys.
6. **Write the log.** Results and the current signatures go into the run log.

Stop rule: Stops after five Spaces and one sample call per endpoint.

## Permissions

- Writes: loops/gradio-space-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/gradio-space-check-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning at seven. Verification: endpoints answer with outputs. Memory: loops/gradio-space-check-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
