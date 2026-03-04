# Lesson Creation Workflow

This file defines a step-by-step workflow Claude should follow when asked to create a lesson.
Always follow these steps in order. Create a dedicated folder for each new lesson under `lessons/<topic-slug>/`.

---

## Workflow Overview

```text
Step 1 → Ask for topic
Step 2 → Ask for sources
Step 3 → Create lesson plan (markdown)
Step 4 → Ask for exercise context
Step 5 → Create exercises + answer key
Step 6 → Create MARP slides
```

---

## Step 1 — Ask for the Topic

Ask the user:

> "What is the topic of the lesson? Please describe it briefly, including the target audience (e.g., age group, prior knowledge level) and the intended duration of the lesson."

Wait for the answer before proceeding.

---

## Step 2 — Ask for Sources

Ask the user:

> "What sources should I use for this lesson? You can provide:
>
> - URLs to online articles, videos, or documentation
> - File paths to documents in this project folder
> - General references (books, papers) I should be aware of
>
> Leave blank to rely only on the educational_context.MD and my general knowledge."

Fetch or read all provided sources before proceeding.

---

## Step 3 — Create the Lesson Plan

Create a folder: `lessons/<topic-slug>/`

Create the file: `lessons/<topic-slug>/lesson.md`

Structure the lesson following the Bain-inspired principles from `educational_context.MD`:

```markdown
# Lesson: <Topic>

**Target audience:** ...
**Duration:** ...
**Learning objectives (as questions):** ...

---

## 1. Opening — Challenging Problem or Question
<!-- Trigger curiosity. Start from an authentic problem. -->

## 2. Prior Knowledge Check
<!-- Surface misconceptions before instruction. -->

## 3. Core Concepts
<!-- Introduce theory as a thinking tool, not content to cover. -->

## 4. Application
<!-- Students apply theory to a new situation. -->

## 5. Reflection
<!-- Metacognitive closing questions. -->

---

## Sources Used
```

After writing the file, confirm with the user:

> "The lesson plan has been saved to `lessons/<topic-slug>/lesson.md`. Does this look good, or would you like adjustments before I create the exercises and slides?"

Wait for approval before continuing.

---

## Step 4 — Ask for Exercise Context

Ask the user:

> "What context should I keep in mind when creating the exercises?
> For example:
>
> - Should exercises be individual or collaborative?
> - Are they graded or formative (low-stakes)?
> - Any specific formats preferred (case study, multiple choice, open question, group discussion)?
> - Any constraints (time per exercise, tools available, etc.)?"

Wait for the answer before proceeding.

---

## Step 5 — Create Exercises

Create the file: `lessons/<topic-slug>/exercises.md`

Create two sets of exercises:

### During the Lesson (In-class)

- 2–3 exercises that fit within the lesson flow
- Focused on misconceptions, application, and discussion
- Tied to the lesson structure from Step 3

### After the Lesson (Homework / Follow-up)

- 2–3 exercises for deeper processing and transfer
- At least one open-ended question requiring reflection or argumentation

Each exercise should include:

- A clear instruction
- The Bain principle it targets (e.g., "targets: deep learning / transfer")
- An optional teacher note

After writing `exercises.md`, create the file: `lessons/<topic-slug>/answers.md`

This is a teacher-facing document. For each exercise in `exercises.md`, provide:

- The exercise title/number (matching the order in `exercises.md`)
- A model answer or worked-out solution
- For open-ended questions: key elements a strong answer should include, not a single correct answer
- An optional grading note (what distinguishes a weak, adequate, and strong response)

---

## Step 6 — Create MARP Slides

Create the file: `lessons/<topic-slug>/slides.md`

Use MARP format. The slide deck should follow the lesson structure from Step 3.

```markdown
---
marp: true
theme: default
paginate: true
---

# <Topic>
<Subtitle or framing question>

---

<!-- One slide per major lesson section -->
```

Guidelines for slides:

- Keep text minimal — one key point or question per slide
- Use the opening question from the lesson plan as the first content slide
- Include a "Reflection" slide at the end with the metacognitive closing questions
- Do not duplicate exercise content on the slides

After creating the slides, run the MARP CLI to generate a PDF:

```bash
marp lessons/<topic-slug>/slides.md --pdf --output lessons/<topic-slug>/slides.pdf
```

Confirm with the user when all files are ready:

> "All lesson materials are saved in `lessons/<topic-slug>/`:
>
> - `lesson.md` — lesson plan
> - `exercises.md` — in-class and follow-up exercises
> - `answers.md` — model answers and grading notes (teacher-facing)
> - `slides.md` — MARP source
> - `slides.pdf` — rendered slide deck
>
> Let me know if you'd like to adjust anything."

---

## Educational Principles (Reference)

All lesson content should reflect the principles in `educational_context.MD`:

| Principle                 | Application                                        |
| ------------------------- | -------------------------------------------------- |
| Learning = Making Meaning | Start with a big question, not content             |
| Surface Misconceptions    | Prior knowledge check before instruction           |
| Deep Learning             | Questions requiring connection, transfer, argument |
| Intrinsic Motivation      | Authentic problems, learner autonomy               |
| Productive Mistakes       | Normalize uncertainty, discuss errors              |
| Metacognition             | Reflection at the end of every lesson              |
| High Expectations         | Communicate challenge + belief in students         |
