# CLAUDE.md

Personal portfolio site for Tenzin Lhakpa (AI/ML Engineer), hosted on GitHub Pages at
https://tenlhak.github.io (repo: `tenlhak/tenlhak.github.io`, branch: `main`).

## Architecture

- **Single-file static site.** Everything — HTML, CSS, and JS — lives in `index.html`.
  No build step, no framework, no external JS libraries. Keep it that way unless the
  owner asks otherwise.
- `images/` holds all assets (webp preferred). `resume.pdf` at the root is the hosted
  résumé — both "Résumé" buttons link to it. To update the résumé, overwrite the file;
  never change the filename/URL.
- Fonts are loaded from Google Fonts: **Inter** (display/body) and **IBM Plex Mono**
  (annotations). Analytics via **GoatCounter** (script tag near the bottom).

## Run / test locally

```
python -m http.server 8000
```

Then open http://localhost:8000. Don't open `index.html` via `file://` — fetch calls
(page-view counter) are blocked by CORS. GoatCounter ignores localhost visits.

## Design system — "technical document" concept

The design is deliberate Swiss/technical style. When editing, preserve these conventions:

- **Numbered everything:** nav and sections are `01 Work … 05 Contact`; projects are
  `№01…№05`; images carry captions `Fig. 01 …`; essays are `E·01 …`. **If you add or
  remove an item, renumber everything downstream** and update the count in the section
  head (e.g. `(05)` next to "Selected Work").
- **Colors** are CSS variables in `:root`. Single accent color `--accent: #ff4400`
  (signal orange) — do not introduce new colors.
- **Type rules:** headings in Inter (uppercase, tight tracking), all micro-labels/
  annotations in IBM Plex Mono via the `.mono` class. Hairline borders (`--line`)
  frame every section.
- Project images render grayscale and colorize on row hover (CSS filter).

## JS behaviors (all vanilla, inside the one `<script>` block)

- Scramble-decode animation on the `<h1>` spans (uses `data-text`; respects
  `prefers-reduced-motion`).
- Fixed HUD (bottom-left): local time, scroll %, current section. Section labels are
  hardcoded in `sectionLabels` — update if sections change.
- Scroll progress bar (top edge), scroll-reveal via IntersectionObserver (`.reveal`).
- Page-view counter fetches `https://tenzinlhakpa.goatcounter.com/counter//.json`.
  Shows `n/a` if it fails. Requires "Allow adding visitor counts on your website"
  enabled in the owner's GoatCounter settings (was returning 403 as of Jul 2026 —
  owner needs to flip the setting). The old CountAPI service is dead; don't revert
  to it.

## Content gotchas

- Owner's current positioning: **AI/ML Engineer focused on agentic systems** that
  automate manual organizational work. Keep hero/spec/about copy consistent with this.
- Essays section: E·01 links to a published Medium article; the rest are
  "Coming soon" placeholders the owner intends to write.
- Favicon is `images/fav_icon.webp`; `apple-touch-icon.png` is still the old logo
  (needs a 180×180 replacement eventually).
- The original full-quality `endo_assist.png` lives outside the repo at
  `..\endo_assist.png` (repo copy is compressed webp).

## Owner preferences (learned the hard way)

- **Discuss design direction before rebuilding.** A previous multi-page "minimalist"
  redesign was rejected outright; the current Swiss/technical single-page design was
  chosen from presented options and approved.
- Prefers being taught how to do things (commands, reasoning) over having them done
  silently.
- Site must stay GitHub Pages compatible: static frontend only, no backend.
