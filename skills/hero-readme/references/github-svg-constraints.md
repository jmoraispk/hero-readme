# GitHub-rendered SVG: what actually works

READMEs render on GitHub, which serves every image through its Camo proxy and
sanitizes SVGs loaded as images (`![](x.svg)` or `<img src="x.svg">`). Most
"SVG generator" tools produce SVGs that look animated in a browser but render
**static or broken** on GitHub because they assume `<script>` runs. It does not.

This file is the ground truth. Build to it.

## The one rule that trips everyone up

**An SVG embedded as an image cannot run JavaScript and cannot respond to the
mouse.** GitHub loads your hero as an `<img>`, so:

- `<script>` — **stripped.** Never rely on it.
- `:hover`, `:active`, click handlers, `<a>` navigation inside the SVG — **dead.**
  The image is not interactive. Animation must be autonomous (loops), not
  triggered by the user.
- `<foreignObject>` and embedded HTML — **not rendered.** Stay in pure SVG.
- External references — `@import`, `<image href="https://...">`,
  `@font-face { src: url(https://...) }` — **blocked.** Everything must be
  embedded in the file.

## What DOES animate (use these)

| Technique | Works on GitHub? | Use for |
|-----------|:---------------:|---------|
| SMIL: `<animate>`, `<animateTransform>`, `<animateMotion>` | ✅ | movement, transforms, path motion |
| CSS `@keyframes` in an inline `<style>` | ✅ | fades, sweeps, staggered reveals |
| CSS transitions on `:hover` | ❌ | never — no pointer in `<img>` |
| `<set>` on interaction events | ❌ | never — no events fire |

Both SMIL and inline-CSS `@keyframes` run in the image's own rendering context
without script, so both play on GitHub. Prefer whichever is clearer for the
effect; you can mix them.

```svg
<!-- CSS keyframes: a gradient sweep that loops forever, no script -->
<style>
  @keyframes sweep { to { transform: translateX(100%); } }
  .shimmer { animation: sweep 4s ease-in-out infinite; }
</style>
<rect class="shimmer" .../>
```

```svg
<!-- SMIL: same idea, declarative -->
<rect ...>
  <animateTransform attributeName="transform" type="translate"
    from="-400 0" to="400 0" dur="4s" repeatCount="indefinite"/>
</rect>
```

## Dark mode

GitHub has light and dark themes. Two robust approaches — pick one:

**A. Single adaptive SVG (elegant, one file).** Put a `prefers-color-scheme`
media query inside the SVG's `<style>`. The query reflects the viewer's theme.

```svg
<style>
  .bg { fill: #ffffff; }
  .fg { fill: #0b1020; }
  @media (prefers-color-scheme: dark) {
    .bg { fill: #0d1117; }
    .fg { fill: #f0f6fc; }
  }
</style>
```

**B. Two files via `<picture>` (most robust for genuinely different art).**

```html
<picture>
  <source media="(prefers-color-scheme: dark)"  srcset="assets/hero-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/hero-light.svg">
  <img alt="Project name — one-line tagline" src="assets/hero-light.svg" width="100%">
</picture>
```

Default to A for a single wordmark/motif hero. Use B only when light and dark
need structurally different graphics. Never leave a hero that's invisible on one
theme (e.g. dark text with a transparent background disappears in dark mode).

## Accessibility & motion safety (required, not optional)

- Give the root `role="img"` and a real `aria-label`, plus `<title>` and
  `<desc>` as the first children. The `alt` on the `<img>`/`<picture>` matters
  too — screen readers use it.
- Gate motion behind reduced-motion so it only plays when the viewer allows it:

```svg
<style>
  .shimmer { /* static styles only */ }
  @media (prefers-reduced-motion: no-preference) {
    .shimmer { animation: sweep 4s ease-in-out infinite; }
  }
</style>
```

- No rapid flashing (seizure risk). Keep loops slow (≥2s) and easing gentle.

## Fonts (the other silent failure)

The SVG renders with fonts on the **viewer's** machine, not yours. Web fonts
won't load. Two options:

- **System font stack** — editable, tiny, "good enough" for most heroes.
  `font-family="'Segoe UI', system-ui, -apple-system, Helvetica, Arial, sans-serif"`.
  Accept that exact glyph shapes vary by platform.
- **Text converted to `<path>`** — pixel-identical everywhere, guarantees a
  display typeface, but no longer editable as text and larger. Use for a
  wordmark where the exact letterforms are the brand.

Never rely on a font you can't embed as paths and can't expect on the viewer's OS.

## Layout & size

- Use a `viewBox` (e.g. `viewBox="0 0 1200 360"`) so it scales; a banner aspect
  around 2.5:1–4:1 reads well at the top of a README.
- Control display width from the README: `<img ... width="100%">` or a fixed max.
- Center with `<div align="center">…</div>` (GitHub honors `align`).
- Keep it lean — well under ~200 KB. No embedded raster unless essential.

## Pre-commit validation checklist

Before wiring a hero in, confirm:

- [ ] No `<script>` anywhere in the file.
- [ ] No `:hover`/click/`<foreignObject>`/external `href` dependencies.
- [ ] Animation uses SMIL and/or inline `@keyframes` only.
- [ ] Visible and legible in BOTH light and dark (test both).
- [ ] Motion gated behind `prefers-reduced-motion: no-preference`.
- [ ] `role="img"`, `aria-label`, `<title>`, `<desc>` present; `alt` on the img.
- [ ] Well-formed XML, fonts embedded-as-paths or safe stack, size sane.
