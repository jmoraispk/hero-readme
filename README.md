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
  <a href="https://github.com/jmoraispk/codeaway">
    <img src="assets/examples/codeaway.svg" alt="codeaway — keep your AI coding agent running" width="100%">
  </a>
</p>

…and **20 more in the wild** — check the **[wild gallery](assets/wild/wild.md)**.

|   |   |
|:--:|:--:|
| <a href="https://github.com/Genymobile/scrcpy"><img src="assets/wild/Genymobile__scrcpy.svg" width="100%" alt="scrcpy"></a><br>**scrcpy** · ⭐ 146k | <a href="https://github.com/d3/d3"><img src="assets/wild/d3__d3.svg" width="100%" alt="d3"></a><br>**d3** · ⭐ 110k |
| <a href="https://github.com/axios/axios"><img src="assets/wild/axios__axios.svg" width="100%" alt="axios"></a><br>**axios** · ⭐ 107k | <a href="https://github.com/mrdoob/three.js"><img src="assets/wild/mrdoob__three.js.svg" width="100%" alt="three.js"></a><br>**three.js** · ⭐ 103k |
| <a href="https://github.com/excalidraw/excalidraw"><img src="assets/wild/excalidraw__excalidraw.svg" width="100%" alt="excalidraw"></a><br>**excalidraw** · ⭐ 90k | <a href="https://github.com/jesseduffield/lazygit"><img src="assets/wild/jesseduffield__lazygit.svg" width="100%" alt="lazygit"></a><br>**lazygit** · ⭐ 80k |
| <a href="https://github.com/mermaid-js/mermaid"><img src="assets/wild/mermaid-js__mermaid.svg" width="100%" alt="mermaid"></a><br>**mermaid** · ⭐ 79k | <a href="https://github.com/chartjs/Chart.js"><img src="assets/wild/chartjs__Chart.js.svg" width="100%" alt="Chart.js"></a><br>**Chart.js** · ⭐ 65k |
| <a href="https://github.com/tesseract-ocr/tesseract"><img src="assets/wild/tesseract-ocr__tesseract.svg" width="100%" alt="tesseract"></a><br>**tesseract** · ⭐ 63k | <a href="https://github.com/socketio/socket.io"><img src="assets/wild/socketio__socket.io.svg" width="100%" alt="socket.io"></a><br>**socket.io** · ⭐ 61k |
| <a href="https://github.com/Leaflet/Leaflet"><img src="assets/wild/Leaflet__Leaflet.svg" width="100%" alt="Leaflet"></a><br>**Leaflet** · ⭐ 42k | <a href="https://github.com/date-fns/date-fns"><img src="assets/wild/date-fns__date-fns.svg" width="100%" alt="date-fns"></a><br>**date-fns** · ⭐ 34k |
| <a href="https://github.com/lovell/sharp"><img src="assets/wild/lovell__sharp.svg" width="100%" alt="sharp"></a><br>**sharp** · ⭐ 30k | <a href="https://github.com/sharkdp/hyperfine"><img src="assets/wild/sharkdp__hyperfine.svg" width="100%" alt="hyperfine"></a><br>**hyperfine** · ⭐ 28k |
| <a href="https://github.com/liabru/matter-js"><img src="assets/wild/liabru__matter-js.svg" width="100%" alt="matter-js"></a><br>**matter-js** · ⭐ 17k | <a href="https://github.com/catppuccin/catppuccin"><img src="assets/wild/catppuccin__catppuccin.svg" width="100%" alt="catppuccin"></a><br>**catppuccin** · ⭐ 15k |
| <a href="https://github.com/asciinema/asciinema"><img src="assets/wild/asciinema__asciinema.svg" width="100%" alt="asciinema"></a><br>**asciinema** · ⭐ 15k | <a href="https://github.com/katspaugh/wavesurfer.js"><img src="assets/wild/katspaugh__wavesurfer.js.svg" width="100%" alt="wavesurfer.js"></a><br>**wavesurfer.js** · ⭐ 9.0k |
| <a href="https://github.com/ImageOptim/gifski"><img src="assets/wild/ImageOptim__gifski.svg" width="100%" alt="gifski"></a><br>**gifski** · ⭐ 7.0k | <a href="https://github.com/nayuki/QR-Code-generator"><img src="assets/wild/nayuki__QR-Code-generator.svg" width="100%" alt="QR-Code-generator"></a><br>**QR-Code-generator** · ⭐ 5.0k |

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
