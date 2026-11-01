---
name: create-lesson
description: Start the full lesson creation workflow (9 steps)
disable-model-invocation: true
argument-hint: "[topic or input folder slug] (optional)"
---

Start the lesson creation workflow defined in CLAUDE.md. Follow all steps in order:

0. Check `input/` for a matching `input/<topic-slug>/` folder (use $ARGUMENTS as topic or slug if provided), read its `brief.md` and list its `sources/` and `input/_shared/`
1. Ask for the topic — or confirm what `brief.md` / $ARGUMENTS already says
2. Ask for sources — read the input files first, then ask only for anything else
3. Create the lesson plan (`lesson.md`), reading `.claude/context/persona.md` and `.claude/context/educational_context.md` first
4. Ask for exercise context — or confirm what `brief.md` already says
5. Create exercises (`exercises.md`) and model answers (`answers.md`)
6. Create quiz questions (`quiz.md`), persona-aware
7. Create MARP slides (`slides.md`) with the HZ theme (`themes/README.md`) and render to PDF and interactive HTML
8. Create student notes template (`notes-template.md`)
9. Create the lesson infographic following `.claude/skills/infographic/SKILL.md`

Wait for user approval after Step 3 before continuing. Confirm completion after Step 9.
