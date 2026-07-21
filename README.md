# Exam Distribution

A single-file web tool for turning raw exam scores into a clean letter-grade
distribution, applying a curve, and printing a professional report to PDF.

No install, no server, no dependencies — just open `index.html` in a browser.

## Features

- **Paste-friendly input** — paste a column of raw scores straight from Excel.
  Blank lines, stray text, commas, and tabs are tolerated, and anything ignored
  is flagged.
- **Grade distribution** — counts of A / B / C / D / F on the standard scale
  (A ≥ 90%, B 80–89%, C 70–79%, D 60–69%, F < 60%).
- **Curve** — enter the number of raw points to add to everyone's score; a curved
  distribution is shown next to the original on a **shared axis** for direct
  comparison. Curved scores are capped at 100%.
- **Summary stats** — student count, raw median, curved median, and curved mean,
  plus a full grade-breakdown table.
- **Print / Save as PDF** — a clean landscape report with the course number,
  auto-filled date, median score, and the distribution chart.

## Usage

1. Open `index.html` in any modern browser.
2. Enter the **course number**, **total exam items**, and optionally an **exam
   name** (the date auto-fills to today and is editable).
3. Paste the **raw scores**, one per line.
4. Enter a **curve** value (in points) to preview a curved distribution.
5. Click **Print / Save as PDF** and choose "Save as PDF" as the destination.

## Inputs

| Input | Meaning |
|-------|---------|
| Course number | Shown in the printed report title |
| Exam name | Optional label (e.g. "Exam 3") |
| Date | Auto-filled to today; editable |
| Total exam items | The maximum raw score (e.g. 50 questions) |
| Curve | Raw points added to every score, capped at 100% |
| Raw scores | One score per line |
