# Exam Distribution

A web tool for merging Canvas exam scores into the gradebook, turning them into
a clean letter-grade distribution, applying a curve, and exporting files for
Canvas plus a professional PDF report.

No install and no server — just open `index.html` in a browser. Files you import
are processed entirely in the browser and never uploaded.

## Features

- **Import from Canvas** — drop in the quiz *Student Analysis* export (exam
  scores) and the *gradebook* export (.csv or .xlsx). The course number, term,
  exam name, date, total exam items, and raw scores fill in automatically.
  Students are matched by Canvas ID (then SIS ID); anyone in the exam file but
  not the gradebook is flagged.
- **Canvas downloads**
  - `PSY157 (2026 Fall) - Exam 1.xlsx` — student columns plus raw score, curved
    score, and final percentage, sorted highest score first. Row 2 shows the
    item total, `Curve +N`, and 100. The curve and percentage cells are live
    Excel formulas.
  - `PSY157 (2026 Fall) - Exam 1 GB.csv` — the gradebook import file with only
    the final percentage (out of 100). Students with no exam score are left
    blank.
- **Missed-exam emails** — one click copies the email addresses of students
  with no exam score (SIS Login ID + `@ucmerced.edu`), ready to paste into an
  email about the makeup exam.
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
2. **From Canvas:** drop the exam scores and gradebook files into **Import from
   Canvas**, and check the gradebook column it picked (the first empty exam
   column). **Or by hand:** enter the course number, total exam items, and exam
   name, and paste the raw scores, one per line.
3. Enter a **curve** value (in points) to preview a curved distribution.
4. Download the **.xlsx** (raw and curved scores) and the **GB.csv** (import it
   in Canvas under Grades → Import).
5. Click **Print / Save as PDF** and choose "Save as PDF" as the destination.

## Inputs

| Input | Meaning |
|-------|---------|
| Course number | Shown in the printed report and file names (read from the file name, e.g. `…Grades-PSY_157_…`) |
| Term | Used in file names; read from the exam file's `section_sis_id` (`202630` = 2026 Fall, `10` Spring, `20` Summer) |
| Exam name | Optional label (e.g. "Exam 3") |
| Date | Auto-filled to today; editable |
| Total exam items | The maximum raw score (e.g. 50 questions) |
| Curve | Raw points added to every score, capped at 100% |
| Raw scores | One score per line |

## Dependencies

`vendor/xlsx.mini.min.js` is [SheetJS Community Edition](https://sheetjs.com)
0.20.3 (Apache-2.0, see `vendor/SHEETJS-LICENSE`), used to read and write .xlsx
files. CSV import and export work without it.
