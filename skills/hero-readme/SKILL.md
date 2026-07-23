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

**Bespoke, never templated.** The background effect, palette, and animation must be
invented for THIS project and *depict what it does* — a diffing tool shows a diff
resolving; a device mirror shows a screen appearing; an HTTP client shows a request
leave and a response return. The background-effects catalog and the concept-lab
motifs are *starting points to riff on*, never fill-in-the-blank templates. If two
different projects would get interchangeable heroes, you haven't looked closely
enough at either — vary the background, the colors, and the motion every time.

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

5. **Review with fresh eyes, then revise — loop until it passes (MANDATORY).**
   You cannot trust a hero you have not watched. Get an INDEPENDENT review and
   iterate. See "Review-and-revise loop" below.

6. **Wire it into the README** at the very top, centered, with a real
   `alt="<name> — <tagline>"`, and keep the surrounding copy honest (no invented
   badges or features). → `references/readme-structure.md`.

## Review-and-revise loop (do NOT skip — this is where quality is won)

Draft SVGs almost always have defects — misalignment, overlap, a generic look, an
animation that doesn't read — that are invisible in the code and obvious once
watched. Kill them with an *independent* review that iterates.

**Separate the author from the reviewer.** The reviewer must come at it fresh — a
different agent (dispatch a subagent), or at minimum a fresh-context pass that
judges the *rendered result*, not the code. Whoever wrote the SVG will rubber-stamp
their own work; do not let the author be the sole reviewer.

**The loop:**
1. **Author** produces the SVG.
2. **Reviewer renders it as an `<img>` at SEVERAL timestamps across the animation
   loop** (≈5–6 frames), on a light AND a dark page. One screenshot cannot judge
   motion — you must see the animation *progress* to catch a sweep that leaks, a
   reveal that never completes, or a static frame that looks unfinished.
3. **Reviewer critiques against the rubric** and returns a verdict: `pass`, or
   `revise` with a specific, numbered list of issues.
4. On `revise`, the **author fixes the named issues** and produces a new SVG.
5. **Repeat** until the reviewer returns `pass` (or a sane iteration cap ~3–4),
   then ship.

**Review rubric** — the reviewer checks every item against the actual frames:
- **Bespoke?** Do the background, palette, and animation clearly belong to THIS
  project, or could they be swapped onto any repo? Interchangeable = fail.
- **Depicts the concept?** Does the motion actually *show what the project does*?
- **Motion reads** across the frames — purposeful, loops cleanly, static frame
  already finished, nothing invisible-until-it-moves, no strobing.
- **Alignment / overlap / clipping** — shared edges line up; nothing touches the
  frame edge or collides; nothing cut off; labels fit their box.
- **Legibility** — every word crisp over the effect in both themes; scrim works.
- **GitHub-safe** — no `<script>`/`:hover`; motion gated; a11y present; well-formed.

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

1. **Completed the review-and-revise loop above** — an *independent* reviewer
   rendered several animation frames on both a light and a dark page and returned
   `pass` (bespoke, depicts the concept, motion reads, aligned, legible).
2. Confirmed the background effect **animates** and the static frame looks
   finished.
3. **Run the pre-commit checklist** in `references/github-svg-constraints.md`
   (no script, no interactivity deps, motion gated, a11y present, well-formed).
4. Confirmed the README shows the hero at the top with honest copy.

If a check fails, fix it before committing. Evidence before assertions.

## Common mistakes

- **Template sameness** — the same background effect, layout, and motion recolored
  across every repo. The catalog entries are riff-starters, not templates; invent
  a fresh animation that depicts each project. Interchangeable heroes = failure.
- **Shipping without looking** — Misaligned bars, text touching the frame, an
  element off by 20px, a sweep that leaks. Run the review-and-revise loop.
- **Author reviews own work** — self-review rubber-stamps. Get an independent pass.
- **Judging motion from one screenshot** — render several frames across the loop.
- **No background effect** — a flat wordmark reads as a placeholder. The effect
  is required (`references/background-effects.md`).
- **Effect drowns the text** — turn its opacity down and strengthen the scrim.
  Legibility beats spectacle.
- **Assuming `<script>`/`:hover` work** — they don't on GitHub. Cause of "great
  locally, static/broken on GitHub."
- **Generic art** — a pretty blob that fits any repo. Re-run the authenticity
  gate in `references/hero-design.md`.
- **Overselling** — fake badges or unshipped features under a slick banner.
