# Lesson Creation Workflow

This file defines a step-by-step workflow Claude should follow when asked to create a lesson.
Always follow these steps in order. Create a dedicated folder for each new lesson under `lessons/<topic-slug>/`.

---

## Workflow Overview

```text
Step 0 → Check the input folder
Step 1 → Ask for topic
Step 2 → Ask for sources
Step 3 → Create lesson plan (markdown, persona-aware)
Step 4 → Ask for exercise context
Step 5 → Create exercises + answer key
Step 6 → Create quiz questions (persona-aware)
Step 7 → Create MARP slides (HZ theme, PDF + interactive HTML)
Step 8 → Create student notes template (Guided Learning Log)
Step 9 → Create infographic (lesson summary)
```

---

## Step 0 — Check the Input Folder

Before asking anything, look in `input/` (see `input/README.md`):

- If a topic slug or name was given, look for a matching `input/<topic-slug>/` folder. If none was given but exactly one lesson folder exists in `input/` without a matching `lessons/` folder, propose that one.
- Read `input/<topic-slug>/brief.md` if it exists. Every filled-in field answers the matching question in Steps 1, 2 and 4.
- List the files in `input/_shared/` and `input/<topic-slug>/sources/` (ignore `.gitkeep`).

Use the same `<topic-slug>` for the `lessons/` folder.

---

## Step 1 — Ask for the Topic

If `brief.md` already answers this, summarise topic, audience and duration in two or three lines and ask the user to confirm or correct it, instead of asking the question below.

Otherwise ask the user:

> "What is the topic of the lesson? Please describe it briefly, including the target audience (e.g., age group, prior knowledge level) and the intended duration of the lesson."

Wait for the answer before proceeding.

---

## Step 2 — Ask for Sources

Read all files found in Step 0 (`input/_shared/` and `input/<topic-slug>/sources/`) and any URLs listed in `brief.md`. Then list what you found in one line per source and ask: "Anything else I should use?" — instead of the full question below.

If there are no input files, ask the user:

> "What sources should I use for this lesson? You can provide:
>
> - URLs to online articles, videos, or documentation
> - File paths to documents in this project folder
> - General references (books, papers) I should be aware of
>
> Leave blank to rely only on the `.claude/context/educational_context.md` and my general knowledge."

Fetch or read all provided sources before proceeding.

---

## Step 3 — Create the Lesson Plan

Create a folder: `lessons/<topic-slug>/`

Create the file: `lessons/<topic-slug>/lesson.md`

Structure the lesson following the Bain-inspired principles from `.claude/context/educational_context.md`.

**Persona-aware design:** Read `.claude/context/persona.md` before writing the lesson plan. For each major section, consider how the three student archetypes (Lars / HAVO, Fatima / MBO, Daan / non-traditional) will experience it. Specifically:

- **Opening:** Choose a problem that feels relevant to Fatima's practical experience AND intriguing enough to engage Daan's curiosity. Add a brief note on how to make it land for Lars too (e.g., a concrete anchor or worked example).
- **Prior Knowledge Check:** Anticipate that Lars may lack practical reference points, Fatima may have misconceptions from applied shortcuts, and Daan may have gaps in foundational theory.
- **Core Concepts:** Provide at least one concrete example (for Lars and Fatima) and one conceptual extension or "why does this work?" angle (for Daan).
- **Application:** Design the task so it has a low floor (accessible to Lars) and a high ceiling (stretching enough for Daan). Note optional depth layers in a teacher note.
- **Reflection:** Include at least one question that invites students to connect the lesson to their own background — making space for Fatima's experience and Daan's self-directed learning history.

```markdown
# Lesson: <Topic>

**Target audience:** ...
**Duration:** ...
**Learning objectives (as questions):** ...

---

## 1. Opening — Challenging Problem or Question
<!-- Trigger curiosity. Start from an authentic problem. -->
<!-- Persona note: ... -->

## 2. Prior Knowledge Check
<!-- Surface misconceptions before instruction. -->
<!-- Persona note: ... -->

## 3. Core Concepts
<!-- Introduce theory as a thinking tool, not content to cover. -->
<!-- Persona note: ... -->

## 4. Application
<!-- Students apply theory to a new situation. -->
<!-- Persona note: low floor / high ceiling task design -->

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

If `brief.md` already answers this, summarise the exercise context in one or two lines and ask the user to confirm or correct it, instead of asking the question below.

Otherwise ask the user:

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

## Step 6 — Create Quiz Questions

Create the file: `lessons/<topic-slug>/quiz.md`

Write exactly **4 quiz questions** students can use to self-assess whether they understood the lesson. The questions are low-stakes and formative — meant to help students identify gaps, not to grade them.

**Persona-aware design:** The 4 questions should collectively serve all three archetypes from `.claude/context/persona.md`:

- **Q1 — Recall (Lars-focused):** A straightforward question that confirms whether the student grasped the central concept. Clear, unambiguous, no tricks. Gives Lars a confidence anchor.
- **Q2 — Application (Fatima-focused):** A short scenario or practical case where the student must apply the concept. Rewards Fatima's practical intuition and gives Lars a concrete reference point.
- **Q3 — Conceptual / "Why?" (Daan-focused):** A question that probes understanding of the underlying mechanism or rationale — not just what, but why. Rewards Daan's depth and stretches Fatima and Lars.
- **Q4 — Transfer / Open (all):** A broader question asking students to connect the concept to a different context, their own experience, or a related field. Has no single right answer. Rewards Daan's curiosity, Fatima's experience, and pushes Lars beyond the familiar.

Each question must include:

- The question text
- The persona it primarily targets (Q1–Q3) or "all" (Q4)
- The type of thinking it requires (e.g., recall, application, analysis, transfer)
- A brief model answer or key elements of a strong answer (for student self-check)

```markdown
# Quiz — <Topic>

*Use these questions to check your understanding. There are no grades — just honest self-reflection.*

---

## Q1 — <Short title>
**Type:** Recall
**Question:** ...
**Self-check:** ...

## Q2 — <Short title>
**Type:** Application
**Question:** ...
**Self-check:** ...

## Q3 — <Short title>
**Type:** Conceptual
**Question:** ...
**Self-check:** ...

## Q4 — <Short title>
**Type:** Transfer
**Question:** ...
**Self-check:** ...
```

---

## Step 7 — Create MARP Slides

Create the file: `lessons/<topic-slug>/slides.md`

Use MARP format with the HZ theme. The slide deck should follow the lesson structure from Step 3.
Before writing, read `themes/README.md` (layouts, components, interaction) and use `themes/examples/showcase.md` as a reference.

```markdown
---
marp: true
theme: hz
paginate: true
footer: 'HZ University of Applied Sciences · <Course> · <Week>'
---

<!-- _class: title -->
<!-- _paginate: false -->

# <Topic or framing question>

<Course · week>

---

<!-- _class: agenda -->

## Today

1. ...
```

Map lesson sections to slide layouts (`<!-- _class: ... -->`):

| Lesson section | Layout |
| --- | --- |
| Title | `title` |
| Lesson structure (UDL: visible agenda) | `agenda` — one numbered card per lesson section |
| 1. Opening question | `question` |
| 2. Prior knowledge check | `poll` (with QR code if a poll link is known) and/or `.myth` / `.fact` columns |
| 3. Core concepts | `concept`, with `.callout` for the "why does this work?" angle |
| 4. Application | `activity`, with `.chips` for time / grouping / output |
| Concept checks | default layout with `<details class="reveal">` for the answer |
| 5. Reflection | `reflection` |
| Close / next steps | `closing` |

Guidelines for slides:

- Keep text minimal — one key point or question per slide
- Use the opening question from the lesson plan as the first content slide after the agenda
- Include a "Reflection" slide at the end with the metacognitive closing questions
- Do not duplicate exercise content on the slides — refer to the exercise number instead
- Put persona notes and teacher prompts in speaker notes (`<!-- ... -->`), never on the slide
- **Interaction:** use `*` bullets (appear one by one in the HTML version) where students should think before seeing the next point, and `<details class="reveal">` for answers and hints. Leave a blank line between HTML tags and the markdown inside them.
- **Poll QR code:** if `brief.md` has a poll link, generate a QR code (command below) and place it on the `poll` slide as `![qr w:300](poll-qr.png)`

```bash
npx qrcode -w 600 -o lessons/<topic-slug>/poll-qr.png "<poll-url>"
```

After creating the slides, render both versions from the repo root (`.marprc.yml` registers the theme and enables HTML; run `npm install` first if `node_modules/` is missing):

```bash
npx marp lessons/<topic-slug>/slides.md --pdf -o lessons/<topic-slug>/slides.pdf
npx marp lessons/<topic-slug>/slides.md -o lessons/<topic-slug>/slides.html
```

Render a PNG of any slide you are unsure about (`npx marp lessons/<topic-slug>/slides.md --images png -o <scratch-dir>/slide.png`) and look at it; fix overflowing text by shortening it or splitting the slide.

After creating the slides, proceed to Step 8 without confirmation.

---

## Step 8 — Create Student Notes Template (Guided Learning Log)

Create the file: `lessons/<topic-slug>/notes-template.md`

This is a student-facing document — a structured template they fill in before, during, and after the lesson. Its purpose is to deepen processing and make learning visible to the student themselves.

The template has three phases:

### Before the Lesson

A single prompt that activates prior knowledge and sets a personal learning intention:

- "What do I already think I know about this topic?"
- "What am I curious or uncertain about going in?"

### During the Lesson

Structured space for active note-taking with four prompts:

- **Key ideas** — The most important concepts or insights (in their own words, not copied verbatim)
- **Questions that arose** — Things they didn't understand or want to explore further
- **Connections** — Links to things they already know, from class, work, or daily life
- **Something that surprised me** — An unexpected idea, contradiction, or moment of confusion

### After the Lesson

A synthesis section to consolidate and reflect:

- "Summarise the core idea of this lesson in 2–3 sentences, as if explaining it to someone who wasn't there."
- "What question do you still have — or what would you want to learn next?"
- "How does this connect to your own experience, field, or interests?"

**Persona-aware framing:** The template prompts should feel low-threshold and open — not a test. Use inviting, informal language. The "Connections" and "After" prompts especially give space for Fatima's practical experience and Daan's self-directed depth, while the "Key ideas" structure gives Lars the scaffolding to anchor their notes.

Use this template structure:

```markdown
# Learning Log — <Topic>

*This is your personal thinking space — not a test. Use it to make the lesson yours.*

---

## Before the Lesson

**What do I already think I know about this topic?**


**What am I curious or uncertain about going in?**


---

## During the Lesson

**Key ideas** *(in your own words — don't just copy)*


**Questions that came up**


**Connections** *(to things you already know, from class, work, or life)*


**Something that surprised me**


---

## After the Lesson

**Summarise the core idea in 2–3 sentences, as if explaining it to someone who wasn't there.**


**What question do you still have, or what would you want to explore next?**


**How does this connect to your own experience, field, or interests?**

```

After creating the notes template, proceed to Step 9 without confirmation.

---

## Step 9 — Create Infographic

Follow `.claude/skills/infographic/SKILL.md` to create a one-page summary of the whole lesson:

- Use the layout from `brief.md` if given, otherwise `one-pager`
- Output: `lessons/<topic-slug>/infographic.md`, `infographic.pdf` and `infographic.png`
- Check the PNG visually before finishing

Confirm with the user when all files are ready:

> "All lesson materials are saved in `lessons/<topic-slug>/`:
>
> - `lesson.md` — lesson plan
> - `exercises.md` — in-class and follow-up exercises
> - `answers.md` — model answers and grading notes (teacher-facing)
> - `quiz.md` — 4 self-assessment quiz questions (student-facing)
> - `slides.md` — MARP source
> - `slides.pdf` — rendered slide deck
> - `slides.html` — interactive slide deck (press `p` for presenter view)
> - `notes-template.md` — Guided Learning Log for students
> - `infographic.pdf` / `.png` — one-page lesson summary
>
> Let me know if you'd like to adjust anything, or run `/infographic` for an extra infographic of a single topic."

---

## Educational Principles (Reference)

All lesson content should reflect the principles in `.claude/context/educational_context.md`:

| Principle                 | Application                                        |
| ------------------------- | -------------------------------------------------- |
| Learning = Making Meaning | Start with a big question, not content             |
| Surface Misconceptions    | Prior knowledge check before instruction           |
| Deep Learning             | Questions requiring connection, transfer, argument |
| Intrinsic Motivation      | Authentic problems, learner autonomy               |
| Productive Mistakes       | Normalize uncertainty, discuss errors              |
| Metacognition             | Reflection at the end of every lesson              |
| High Expectations         | Communicate challenge + belief in students         |
