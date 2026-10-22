---
name: pdf
title: PDF Processing skill
repo: shareAI-lab/learn-claude-code
license: MIT
url: https://gethabit.dev/skills/shareai-lab/pdf
---

# PDF Processing skill

Pdf processing extracts text from PDFs, creates PDFs from Markdown or HTML, and merges or splits documents with pdftotext, PyMuPDF and ReportLab, with OCR for scanned files. For anyone reading or producing PDF files.

- Install the skill: `npx skills add shareAI-lab/learn-claude-code --skill pdf`
- Source: https://github.com/shareAI-lab/learn-claude-code/tree/HEAD/skills/pdf
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You extract text from a PDF; You create a PDF from Markdown; You merge or split PDFs.
Skip it when: You need to fill PDF form fields; You need a designed, styled PDF layout.

# Make it a habit: New PDFs turned into usable text.

When a new PDF lands in your inbox folder, your agent extracts its text with pdftotext or PyMuPDF, falling back to OCR when extraction is empty, and writes a text file. It checks tools are installed first and processes large files page by page.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new PDF added (event; Claude Code routine; `new .pdf in the inbox folder`)
- **Verification:** text output non-empty. Hard checks: pdftotext or PyMuPDF runs without error; the output text file exists; an empty extraction triggers an OCR fallback. On fail: notify, max 1 retries.
- **Memory:** extraction log at `loops/pdf-text-extract-loop/log.md`. Read first: PDFs already processed.

## Steps

1. **Check the tools.** Confirm pdftotext or PyMuPDF is installed before extracting.
2. **Extract text.** Run pdftotext to a file, or PyMuPDF page by page for large files.
3. **OCR if empty.** If extraction returns empty, use pytesseract OCR on the scanned pages.
4. **Write the output.** Write the text file and log the processed PDF.

Stop rule: Stops after the new PDFs of one run, at most 20 files.

## Permissions

- Writes: *.txt, loops/pdf-text-extract-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/pdf-text-extract-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new PDF added. Verification: text output non-empty. Memory: loops/pdf-text-extract-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
