<div align="center">

<img src="assets/hero.svg" alt="hero-readme — animated hero images for your README, a Claude skill" width="100%">

</div>

## Why

Most README tools give you text and shields.io badges, or generic AI banner art that could belong to any project — never a real hero. The gap is a **top-of-README hero that shows what your project _is_**, built from its real name, purpose, and tech, and that actually renders and animates on GitHub. That's the whole job of this skill.

## Examples

<p align="center">
  <a href="https://github.com/jmoraispk/odysseus-fx">
    <img src="assets/examples/odysseus-fx.svg" alt="Odysseus FX — 25 live canvas & shader effects" width="100%">
  </a>
</p>

<p align="center">
  <a href="https://github.com/jmoraispk/delta-review">
    <img src="assets/examples/delta-review.svg" alt="Delta — GitLab MR reviews, minus the wait" width="100%">
  </a>
</p>

<p align="center">
  <a href="https://github.com/chartjs/Chart.js">
    <img src="assets/wild/chartjs__Chart.js.svg" alt="Chart.js — animated charting" width="100%">
  </a>
</p>

<p align="center">
  <a href="https://github.com/liabru/matter-js">
    <img src="assets/wild/liabru__matter-js.svg" alt="matter-js — a 2D physics engine for the web" width="100%">
  </a>
</p>

<div align="center">

### 👉 &nbsp; For 20 more examples, visit the [**Gallery**](assets/wild/wild.md) &nbsp; 👈

</div>

## How to use

**1. Install it.** As a Claude Code plugin (recommended):

```bash
/plugin marketplace add jmoraispk/hero-readme
/plugin install hero-readme@hero-readme
```

For any other agent, copy [`skills/hero-readme/`](skills/hero-readme) into its skills directory (commonly `.agents/skills/`).

**2. Ask for a hero** — point your agent at a repo:

> **You:** *"make an image for the top of the README"*

It also triggers on *"add a hero/banner to my README"* or *"make my README look better."*

**3. It reads your project and sketches a direction.** Because every hero is built from your real name, tagline, and tech, the skill can take it different ways — here, the same project as a wordmark, an aurora, and a terminal:

<p align="center">
  <img src="assets/variants/variant-wordmark.svg" width="32%">
  <img src="assets/variants/variant-aurora.svg" width="32%">
  <img src="assets/variants/variant-terminal.svg" width="32%">
</p>

It then **renders and independently reviews** the result — watching several animation frames for alignment, motion, and legibility — revises until it passes, commits the SVG to `assets/`, and wires it into your README. For fun, more animated marketing motifs live in the **[concept lab](assets/concept-lab.md)**.

<details>
<summary><b>How it works</b> — the pipeline, for the curious</summary>

<br>

1. **Gather real signals** — name, tagline, project type, language, core features, existing brand.
2. **Pick an authentic motif** — a background, palette, and animation that depict what the project does; never a shared template.
3. **Compose a dark banner with a required background effect** — flow-field, particles, aurora, plasma, and more, colored from the project palette, under a scrim so text stays legible.
4. **Build the SVG to GitHub's real constraints** — no `<script>` or `:hover` (GitHub loads it as an `<img>`), animate with SMIL / CSS `@keyframes`, gate motion behind `prefers-reduced-motion`, add accessibility metadata.
5. **Review and revise, independently** — a separate reviewer renders several animation frames and critiques them; the author revises until it passes. SVG defects are invisible in the code and obvious once watched, so a hero is never shipped unlooked-at.
6. **Wire it into the README** with honest copy — no invented badges or features.

The differentiators: naive SVG generators assume `<script>` runs (so their "animated" heroes are static or broken on GitHub — see [`github-svg-constraints.md`](skills/hero-readme/references/github-svg-constraints.md)), and they never watch what they produced (so it's misaligned or generic — hence the review loop).

</details>
