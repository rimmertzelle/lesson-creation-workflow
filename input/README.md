# Input

Put material here *before* starting `/create-lesson`, so Claude can use it without you pasting paths or answering every question again.

```text
input/
├── _shared/              # Course-wide material, used for every lesson
├── _template/
│   └── brief.md          # Copy this to start a new lesson
└── <topic-slug>/         # One folder per lesson, same slug as lessons/<topic-slug>/
    ├── brief.md          # Your answers to the workflow questions (optional fields)
    └── sources/          # PDFs, old slides, articles, transcripts, screenshots…
```

## How to use

1. Copy `_template/` to a new folder named after the lesson, e.g. `input/wifi-shared-medium/`.
2. Fill in what you already know in `brief.md`. Leave the rest empty; Claude will ask.
3. Drop source files into `sources/`.
4. Run `/create-lesson wifi-shared-medium`.

Claude then reads `brief.md` and confirms it with you instead of asking Steps 1, 2 and 4 from scratch, and scans `_shared/` and `sources/` before asking for more sources.

## What goes in `_shared/`

Material that applies to every lesson in the course, for example:

- course guide / module description
- learning outcomes (e.g. an export from the `it-learning-outcomes` project)
- assessment criteria or rubrics
- house style or terminology lists

## Git

Everything in `sources/` folders is ignored by git (see `.gitignore`), so copyrighted material does not end up in the repo. `brief.md` files and `_shared/` are committed.
