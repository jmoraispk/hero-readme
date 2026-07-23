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

**House style:** a self-contained **dark banner** (background ~`#0d1117`) with a
subtle **animated background effect** (required) and a scrim for legibility — it
reads well on both GitHub light and dark READMEs. Not a flat wordmark on a solid
fill.

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

3. **Compose a dark banner with a required background effect.** Every hero MUST
   include a subtle animated background effect (flow-field streaks, twinkling
   particles, aurora blobs, or plasma) behind the content, with a **scrim** over
   the text so it stays legible. Pull effect colors from the project palette.
   **You MUST follow** `references/background-effects.md`.

4. **Build the SVG to GitHub's real constraints.** This is where naive attempts
   fail. **You MUST follow** `references/github-svg-constraints.md`:
   no `<script>`, no `:hover`/interactivity (GitHub loads it as an `<img>`);
   animate with SMIL and/or inline CSS `@keyframes`; embed fonts as paths or use
   a safe stack; gate motion behind `prefers-reduced-motion`; add
   `role="img"`/`aria-label`/`<title>`/`<desc>`. Save to `assets/hero.svg`.

5. **Render and self-review — iterate until clean (MANDATORY).** SVG coordinates
   are easy to get subtly wrong; you cannot trust a hero you have not looked at.
   Loop below until zero defects.

6. **Wire it into the README** at the very top, centered, with a real
   `alt="<name> — <tagline>"`, and keep the surrounding copy honest (no invented
   badges or features). → `references/readme-structure.md`.

## Self-review loop (do NOT skip — this is where quality is won)

Draft SVGs almost always have alignment and spacing defects that are invisible in
the code and obvious once rendered. So:

1. **Render** the SVG to an image (headless browser embedding it as an `<img>`,
   caught mid-animation) — on both a light and a dark page background.
2. **Look at it and criticize it out loud**, checking specifically:
   - **Alignment** — do elements that should share an edge/baseline actually line
     up? Are related bars left-aligned to the same x? Is the wordmark underline
     under the right glyphs?
   - **Overlap / clipping** — is any text touching or colliding with another
     element or the frame edge? Anything cut off?
   - **Spacing & balance** — even margins and gaps? A clear focal point, not
     centered mush?
   - **Legibility** — is every word crisp over the background effect in *both*
     themes? Does the scrim do its job?
   - **Motion** — does the effect actually animate, and is the static frame
     already finished (nothing invisible until it moves)?
3. **Fix** the coordinates/values for every defect found.
4. **Re-render and repeat** until a pass finds nothing. One render is not enough.

## Quick reference — GitHub SVG do / don't

| Do | Don't |
|----|-------|
| SMIL `<animate>` / inline `@keyframes` | `<script>` (stripped) |
| Autonomous looping motion | `:hover` / click triggers (dead in `<img>`) |
| Embed everything | external fonts/images/`@import` |
| Dark banner + scrim over the effect | flat wordmark on a solid fill |
| Gate motion on `prefers-reduced-motion` | rapid flashing |

## Verification gate (required)

Do not report the hero as done until you have:

1. **Completed the self-review loop above** — rendered as an `<img>` on both a
   light and a dark page, and a final pass found zero alignment / overlap /
   spacing / legibility defects.
2. Confirmed the background effect **animates** and the static frame looks
   finished.
3. **Run the pre-commit checklist** in `references/github-svg-constraints.md`
   (no script, no interactivity deps, motion gated, a11y present, well-formed).
4. Confirmed the README shows the hero at the top with honest copy.

If a check fails, fix it before committing. Evidence before assertions.

## Common mistakes

- **Shipping without looking** — the #1 quality killer. Misaligned bars, text
  touching the frame, an element off by 20px. Run the self-review loop.
- **No background effect** — a flat wordmark reads as a placeholder. The effect
  is required (`references/background-effects.md`).
- **Effect drowns the text** — turn its opacity down and strengthen the scrim.
  Legibility beats spectacle.
- **Assuming `<script>`/`:hover` work** — they don't on GitHub. Cause of "great
  locally, static/broken on GitHub."
- **Generic art** — a pretty blob that fits any repo. Re-run the authenticity
  gate in `references/hero-design.md`.
- **Overselling** — fake badges or unshipped features under a slick banner.
