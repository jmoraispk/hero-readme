---
name: hero-readme
description: Use when creating or upgrading a README and it needs a top-of-file hero image, banner, or wordmark — "make my README beautiful", "add a hero/banner", "generate a project banner/logo image". For producing an animated SVG hero that represents the actual project (not generic AI art) and renders correctly on GitHub.
---

# hero-readme

## Overview

Produce a hand-crafted, animated **SVG hero** for the top of a README that
authentically represents **this** project — its real name, purpose, tech, or
architecture — and that actually renders and animates on GitHub.

**Core principle: authenticity.** Every visual element must trace back to a real
signal from the repo. If you can't name where a shape, word, or color came from,
it doesn't belong. Generic-but-pretty art is exactly the failure this skill
prevents.

## When to use

- A README needs a hero/banner/wordmark at the top.
- "Make my README look professional / beautiful."
- An existing hero is generic AI art or a lifeless shields.io strip.

Not for: full screenshot/GIF capture pipelines, or writing README *prose* with no
visual (do that directly).

## Workflow

Do these in order. Don't skip to drawing.

1. **Gather real signals.** Read the repo — name, one-line purpose/tagline,
   project type, primary language/framework, core features, existing brand/tone.
   Write them down. → details in `references/hero-design.md` (Step 1).

2. **Choose ONE authentic archetype** based on project type: **wordmark**
   (safe default), **concept-motif** (only if the project literally does the
   depicted thing), or **architecture/flow** (libs/services). → `references/hero-design.md`.

3. **Build the SVG to GitHub's real constraints.** This is where naive attempts
   fail. **You MUST follow** `references/github-svg-constraints.md`:
   no `<script>`, no `:hover`/interactivity (GitHub loads it as an `<img>`);
   animate with SMIL and/or inline CSS `@keyframes`; adapt to dark mode; embed
   fonts as paths or use a safe stack; gate motion behind
   `prefers-reduced-motion`; add `role="img"`/`aria-label`/`<title>`/`<desc>`.
   Save to `assets/` (e.g. `assets/hero.svg`).

4. **Wire it into the README** at the very top, centered, with a real
   `alt="<name> — <tagline>"`, and keep the surrounding copy honest (no invented
   badges or features). → `references/readme-structure.md`.

5. **Verify before claiming done** — see gate below.

## Quick reference — GitHub SVG do / don't

| Do | Don't |
|----|-------|
| SMIL `<animate>` / inline `@keyframes` | `<script>` (stripped) |
| Autonomous looping motion | `:hover` / click triggers (dead in `<img>`) |
| Embed everything | external fonts/images/`@import` |
| `prefers-color-scheme` for dark mode | dark text on transparent bg |
| Gate motion on `prefers-reduced-motion` | rapid flashing |

## Verification gate (required)

Do not report the hero as done until you have:

1. **Rendered it in both light and dark** (a headless browser / preview) and
   confirmed it is visible, legible, and actually animates in each.
2. **Run the pre-commit checklist** in `references/github-svg-constraints.md`
   (no script, no interactivity deps, motion gated, a11y present, well-formed).
3. Confirmed the README shows the hero at the top with honest copy.

If a check fails, fix it before committing. Evidence before assertions.

## Common mistakes

- **Assuming `<script>`/`:hover` work** — they don't on GitHub. #1 cause of
  "looks great locally, static/broken on GitHub."
- **Generic art** — a pretty gradient blob that fits any repo. Re-run the
  authenticity gate in `references/hero-design.md`.
- **Invisible in dark mode** — dark ink on a transparent background vanishes.
- **Overselling** — fake badges or unshipped features under a slick banner.
