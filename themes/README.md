# HZ Themes

Two MARP themes in the HZ University of Applied Sciences look and feel (palette from hz.nl):

| File | Theme name | Used for |
| --- | --- | --- |
| `hz.css` | `hz` | Lesson slides (16:9) |
| `hz-infographic.css` | `hz-infographic` | One-page infographics (A4 portrait), via the `/infographic` skill |

`.marprc.yml` in the repo root registers this folder and enables HTML, so from the repo root you only need:

```bash
npx marp lessons/<slug>/slides.md --pdf -o lessons/<slug>/slides.pdf   # PDF for printing/sharing
npx marp lessons/<slug>/slides.md -o lessons/<slug>/slides.html        # interactive version for class
```

Run `npm install` once first. `examples/showcase.md` shows every layout (`npm run showcase` renders it).

**Fonts:** HZ uses Silka (headings) and DIN (body). Those are licensed, so the theme uses them only when installed on your machine and otherwise falls back to Plus Jakarta Sans and Barlow from Google Fonts. Rendering offline falls back to system fonts.

## Slide layouts

Set per slide with `<!-- _class: name -->` directly after the `---`.

| Class | Looks like | Use for (lesson section) |
| --- | --- | --- |
| *(none)* | White, orange accent bar above title | Default content |
| `title` | Navy gradient, big white title | First slide |
| `agenda` | Numbered cards from an `1.` list | Lesson structure (UDL: visible lesson flow) |
| `question` | Full blue, one big question | Opening problem, "think" moments |
| `poll` | Light background, white QR card | Predict-first / prior-knowledge polls |
| `concept` | Light blue-grey background | Core concepts |
| `activity` | Warm cream, orange title | In-class exercises (with `.chips`) |
| `reflection` | White, green accents | Metacognitive closing questions |
| `closing` | Navy, centred | Last slide / next steps |

## Components (HTML)

```html
<div class="columns">          <!-- also: columns wide-left / wide-right -->
<div>

Left column markdown

</div>
<div>

Right column markdown

</div>
</div>

<div class="myth">Common idea…</div>   <!-- labelled "Common idea", orange -->
<div class="fact">Closer look…</div>   <!-- labelled "Closer look", green -->

<div class="callout">Highlighted note</div>

<div class="chips"><span class="chip">⏱ 10 min</span><span class="chip">👥 pairs</span></div>

<details class="reveal">
<summary>Show answer</summary>

Hidden until clicked (HTML version). In the PDF only the button is shown.

</details>
```

Always leave a blank line between an HTML tag and the markdown inside it.

## Interaction (HTML version)

- **Step-by-step bullets:** write bullets with `*` instead of `-`. They then appear one per click in `slides.html`; the PDF shows them all.
- **Click to reveal:** `<details class="reveal">` for answers, hints, "why?" follow-ups.
- **Polls:** generate a QR code locally and put it on a `poll` slide:
  ```bash
  npx qrcode -w 600 -o lessons/<slug>/poll-qr.png "https://www.menti.com/..."
  ```
  ```markdown
  ![qr w:300](poll-qr.png)
  ```
  The `qr` in the alt text gives it the white card style.
- **Presenter view:** open `slides.html`, press `p` to see speaker notes (`<!-- ... -->` comments) and the next slide. Press `o` for an overview of all slides, `f` for full screen.

## Infographic components

See `.claude/skills/infographic/templates/` for complete examples: `.hero`, `.label`, `.row` (+`cols-2`/`cols-4`) with `.card` (+`orange`/`green`/`sky`), `.band` with `.myth`/`.fact`, `.flow` with `.step`, `.compare`, `.hub` with `.core`/`.node`, `.takeaway`, `.footer`.
