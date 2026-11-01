---
name: infographic
description: Create an HZ-styled one-page infographic (A4, PDF + PNG) that summarises a whole lesson or one topic from it. Use when the user asks for an infographic, visual summary, poster, cheat sheet or one-pager of a lesson.
argument-hint: "[topic-slug] [whole lesson | section name] [layout] (all optional)"
---

# Infographic

Turn a lesson (or one concept from it) into a single A4 page students can keep, print or revisit.
It is the "second format" for the core concept required by the UDL checklist in `.claude/context/persona.md`.

## 1. Gather input

Parse `$ARGUMENTS` for: the lesson folder (`lessons/<topic-slug>/`), the scope (whole lesson or one section/concept) and an optional layout.
Ask only for what is missing. If there is exactly one lesson folder, use it.

Read `lessons/<topic-slug>/lesson.md`, and `quiz.md` if present (its Q1 is a good check of what the central idea is).

## 2. Pick a layout

Templates live in `.claude/skills/infographic/templates/`. Each is a filled example; copy it and replace all content.

| Layout | Use when | Template |
| --- | --- | --- |
| `one-pager` | Summary of the whole lesson (default) | `one-pager.md` |
| `process` | A procedure, algorithm, cycle or method in 3–6 steps | `process.md` |
| `compare` | Two concepts, tools or approaches side by side | `compare.md` |
| `concept-map` | One central concept with 4–8 related ideas | `concept-map.md` |

If the user did not choose, pick the one that fits the content and say which one you chose and why in one line.

## 3. Write the content

Output file: `lessons/<topic-slug>/infographic.md`, or `infographic-<section-slug>.md` for a single section.

Content rules — an infographic is not a compressed lesson plan:

- **Hero:** the lesson's opening question as the title, and a one-line answer underneath. Kicker = course · week.
- **Max ~150 words on the whole page.** Card text ≤ 25 words, step text ≤ 20 words.
- **Students' language,** not textbook language. Concrete over abstract (Lars), practical anchors (Fatima), one "why" (Daan).
- Include the **misconception** from the lesson's Prior Knowledge Check when the layout has room (`.myth` / `.fact`).
- End with a **takeaway** in "Now you can…" or one-sentence form, matching the learning objectives.
- Accessibility: left-aligned text, no italics for emphasis (use `*text*`, which the theme renders bold orange), don't use colour as the only signal, and no text in images.
- Keep the template's structure and class names. Markdown inside `<div>` blocks needs a blank line before and after it.
- The `concept-map` hub expects exactly 8 `.node` items with the `.core` as the 5th child; use fewer nodes only by switching to `one-pager`.

## 4. Render and check

Run from the repo root (`.marprc.yml` registers the themes and enables HTML):

```bash
npx marp lessons/<topic-slug>/infographic.md --pdf -o lessons/<topic-slug>/infographic.pdf
npx marp lessons/<topic-slug>/infographic.md --image png -o lessons/<topic-slug>/infographic.png
```

Then **open the PNG with the Read tool and look at it**. Fix and re-render if:

- text overflows a card or the page, or anything overlaps the footer → shorten text first, then remove a card
- there is a large empty gap (> ~¼ page) → add one card (e.g. "Where you see this", "Try this", "Why does this work?")
- a heading wraps awkwardly → rephrase it shorter

## 5. Report

Tell the user the file paths (`.md`, `.pdf`, `.png`), the layout used, and offer one alternative layout that would also fit.
