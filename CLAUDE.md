# Exam Distribution (`ExamDistribution`)

A teaching tool that merges Canvas exam scores into the gradebook, previews a curve, and exports
Canvas-ready files plus a PDF report. Live at
<https://rossdavilla.github.io/ExamDistribution/>.

**`README.md` is the real documentation** — every feature, every input, the exact export file
names and what each column means. Read it before changing behaviour, and update it in the same
change.

## Layout

```
index.html                     the whole tool — one file, no build step, no server
vendor/xlsx.mini.min.js        SheetJS Community Edition 0.20.3 (Apache-2.0), reads/writes .xlsx
vendor/SHEETJS-LICENSE
```

CSV import and export work without SheetJS; only `.xlsx` needs it.

## ⚠️ Student data never leaves the browser

The files Ross drops in are real Canvas exports: student names, Canvas IDs, SIS login IDs, and
scores. Everything is parsed and written **in the browser** — nothing is uploaded, and there is no
backend or analytics. That is a hard constraint, not a current implementation detail:

- Never add a fetch, upload, CDN call, telemetry hook or error reporter that could carry row data
  off the page.
- Never commit a real export, a gradebook, or a screenshot showing student rows. The repo is
  public.

The emails the tool copies are built from SIS Login ID + `@ucmerced.edu` so Ross can paste them
into a makeup-exam email; they are assembled on demand and not stored.

## Things that are easy to break

- **Canvas file shapes.** Import depends on the quiz *Student Analysis* export and the *gradebook*
  export as Canvas writes them: the course number is read from the file name
  (`…Grades-PSY_157_…`), the term from the exam file's `section_sis_id` (`202630` = 2026 Fall,
  `10` Spring, `20` Summer), and students are matched by Canvas ID then SIS ID. Keep the
  "in the exam file but not the gradebook" flag working — it is how Ross catches a bad merge.
- **The exports have to import cleanly into Canvas.** `… - Exam 1.xlsx` carries live Excel
  formulas for the curve and percentage with the item total / `Curve +N` / 100 in row 2, and
  `… - Exam 1 GB.csv` carries only the final percentage with blanks for students who have no
  score. Changing either layout means re-checking an actual Canvas import.
- **Drop-lowest is display-only.** It leaves low raw scores out of the charts, stats and PDF, but
  those students still get their curved score in both downloads. Keep that split.

## Publishing

GitHub Pages serves `main` from the repository root, so a push to `main` is the deploy. Already
listed in `data/sites.json` in the
[`rossdavilla.github.io`](https://github.com/rossdavilla/rossdavilla.github.io) repo under the
`tools` tag.
