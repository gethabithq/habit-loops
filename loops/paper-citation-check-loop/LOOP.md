---
name: ml-paper-writing
title: ML Paper Writing skill
repo: orchestra-research/ai-research-skills
license: MIT
url: https://gethabit.dev/skills/orchestra-research/ml-paper-writing
---

# ML Paper Writing skill

The ml paper writing skill helps an agent draft and format papers for NeurIPS, ICML, ICLR, ACL, AAAI and COLM from a research repo, with LaTeX templates, verified citations and venue checklists. For ML researchers preparing submissions.

- Install the skill: `npx skills add orchestra-research/ai-research-skills --skill ml-paper-writing`
- Source: https://github.com/orchestra-research/ai-research-skills/tree/HEAD/20-ml-paper-writing/ml-paper-writing
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You turn a research repo into a paper; You need verified citations; You convert a paper to another venue.
Skip it when: You target a systems venue; You write a blog post, not a paper.

# Make it a habit: No unverified citation reaches submission.

On every push to a paper repo, your agent compiles the draft with latexmk, checks each citation against Semantic Scholar and a second source, fetches BibTeX by DOI and marks anything unverified as a placeholder. A log keeps verified and open citations.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** push to paper repo (event; GitHub Actions or Claude Code routine; `push to the branch holding main.tex`)
- **Verification:** compiles, citations all verified. Hard checks: latexmk -pdf main.tex compiles without errors; every \cite key has a BibTeX entry fetched by DOI or arXiv; count of PLACEHOLDER and [CITATION NEEDED] markers is zero before submission; a Limitations section exists. On fail: notify, max 0 retries.
- **Memory:** citation status log at `loops/paper-citation-check-loop/citations.md`. Read first: citations already verified and placeholders still open.

## Steps

1. **Compile the draft.** Your agent runs latexmk -pdf main.tex and stops on errors.
2. **Collect citations.** It lists every \cite key and the matching entries in the .bib file.
3. **Verify each paper.** It searches Semantic Scholar and confirms the paper in arXiv or CrossRef too.
4. **Fetch BibTeX by DOI.** It pulls BibTeX through doi.org instead of writing entries from memory.
5. **Check the claim.** It confirms the cited claim really appears in the paper.
6. **Mark placeholders.** Anything it cannot verify becomes a placeholder, and the scientist gets the list.
7. **Run the checklist.** It checks the venue checklist from references/checklists.md and the page limit.

Stop rule: Stops after one draft and at most 50 new citations per run.

## Permissions

- Writes: loops/paper-citation-check-loop/**, *.bib
- Network: api.semanticscholar.org, doi.org
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/paper-citation-check-loop/citations.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: push to paper repo. Verification: compiles, citations all verified. Memory: loops/paper-citation-check-loop/citations.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
