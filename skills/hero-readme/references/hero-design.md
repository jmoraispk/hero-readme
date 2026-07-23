# Designing an authentic hero

The hero fails the moment it could belong to a different project. Every element
must trace back to something true about **this** repo. If you can't name the
signal a shape/word/color came from, cut it.

## Step 1 — Harvest real signals

Read the repo, don't guess. Pull:

- **Name** and **one-line purpose/tagline** — from README H1, the `description`
  in `package.json` / `pyproject.toml` / `Cargo.toml` / `composer.json`, or the
  GitHub repo description.
- **Project type** — CLI, library, web/interactive app, service/API. Decides the
  archetype below.
- **Primary language / framework** — informs palette and any iconography.
- **Core concepts / features** — top-level README headings, exported public API,
  subcommands, the 2–3 things it actually does.
- **Existing brand** — a logo, existing screenshots, colors already in the docs
  or app. Reuse these; don't reinvent.
- **Tone** — playful vs. precise vs. enterprise, inferred from how the docs read.

Write these down before drawing anything. The hero is a visual restatement of
this list.

## Step 2 — Pick ONE archetype

| Archetype | Best for | The move |
|-----------|----------|----------|
| **Wordmark** | anything; the safe, always-valid default | Animated typographic treatment of the real name + tagline. Motion carries the polish. |
| **Concept-motif** | tools with a vivid, literal action | A subtle animation that *depicts what it does* — a diff tool's two columns resolving, a particle gallery's drifting particles. Only if the project genuinely does that. |
| **Architecture/flow** | libraries, services, pipelines | A small animated diagram of the real data/request flow, labeled with real component names. |

When unsure, do a **wordmark** — a beautifully-set real name never lies about the
project. Never invent a mascot or motif the project doesn't earn.

## Step 3 — Choose a restrained palette

In priority order:

1. **Existing brand colors** (logo/app/docs) — always win.
2. **A single accent + neutrals** — one confident accent (or a two-stop gradient)
   over near-black/near-white. This is the tasteful default.
3. **Ecosystem hint, lightly** — a language's known color as *an* accent, never
   the whole design (don't make every Go project teal).

Two to three colors total. Ensure contrast holds in light and dark (see
`github-svg-constraints.md` dark-mode section). Gradients read as "premium" when
they're subtle and 2–3 stops; garish when rainbow.

## Step 4 — Typography

- Name large and unmistakable; tagline ~40–55% of its size, lighter weight.
- Establish clear hierarchy: name → tagline → (optional) small metadata.
- Also render the name/tagline as real README text near the hero — the image
  alone isn't indexable or screen-reader-ideal.
- Font portability: safe stack for editability, or text-to-path for an exact
  display face (see constraints file).

## Step 4b — Background effect (required)

Every hero gets a subtle animated background effect behind the content — this is
what separates a crafted hero from a placeholder. Default to a **self-contained
dark banner** (`~#0d1117`) so the effect's colors pop and the banner reads on
both GitHub themes. Pick ONE effect (flow-field streaks, twinkling particles,
aurora blobs, or plasma), color it from the project palette, keep it low-opacity,
and put a scrim over the text. Full techniques and code: `background-effects.md`.

## Step 5 — Motion with taste

Motion should feel intentional and calm, never a demo reel.

- **Purposeful:** the motion should reinforce the concept (a sweep of light
  across a wordmark; content lines settling into place; data flowing along an
  arrow). Decoration for its own sake reads as noise.
- **Subtle & slow:** loops ≥2s, gentle easing (`ease-in-out`), low amplitude. One
  or two coordinated motions beat five competing ones.
- **Looping & autonomous:** no hover/click triggers (they don't fire on GitHub).
- **Accessible:** gate every animation behind
  `@media (prefers-reduced-motion: no-preference)`; the static frame must already
  look finished.

## Composition checklist

- [ ] Banner aspect ~2.5:1–4:1, generous margins, nothing clipped at the edges.
- [ ] Has a background effect behind the content (required), under a scrim.
- [ ] Legible when scaled down (README width on a phone).
- [ ] Real name present and correctly spelled; tagline is honest.
- [ ] Balanced — clear focal point, not centered-everything mush.

Then render it and run the **self-review loop** in `SKILL.md` before wiring it in.

## Authenticity gate (the whole point)

Before you commit, for **each** visual element answer: *what real signal from
Step 1 does this come from?* If any element's answer is "it looked cool," delete
it. Generic-but-pretty is the failure mode this skill exists to prevent.
