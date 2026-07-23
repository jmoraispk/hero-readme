# Background effects (required)

**Every hero must have a living, animated background effect.** A flat wordmark on
a solid fill looks like a placeholder. The background is what makes a hero feel
crafted — but it must stay *behind* the content and never fight the text.

All techniques below are **pure CSS/SMIL, no `<script>`**, so they animate on
GitHub (see `github-svg-constraints.md`). All must be gated by
`prefers-reduced-motion` and sit under a **scrim** wherever text overlaps them.

## The house pattern: self-contained dark banner

The strongest, most portable hero is a **fixed dark banner** (background around
`#0d1117`) with a colored animated effect and a scrim — *not* a theme-adaptive
one. A dark banner reads well on both GitHub light and dark READMEs, and the
effect colors pop. Reserve light/adaptive designs (`github-svg-constraints.md`,
dark-mode section) for cases where a project's brand demands light.

Layer order, back to front:

1. Solid dark `<rect>` backdrop.
2. A soft accent radial `glow` for depth.
3. The **animated effect** (pick one below), at low opacity.
4. A **scrim** gradient (dark → transparent) over the text side, plus an optional
   vignette. This is what keeps the wordmark legible.
5. Wordmark / tagline / concept-motif on top.

## Effect 1 — flow-field streaks (the signature)

Long curves that follow a noise/flow field, drawn as dashed strokes whose
`stroke-dashoffset` animates → particles appear to stream along the field.

```svg
<style>
  .streak { stroke-dasharray: 8 34; animation: flow linear infinite; }
  @keyframes flow { to { stroke-dashoffset: -42; } }   /* -(dash+gap) = -42 */
  @media (prefers-reduced-motion: reduce) { .streak { animation: none; } }
</style>
<!-- Per-streak duration/delay via INLINE style so each flows independently.
     The class uses the `animation` shorthand with NO duration; the inline
     animation-duration wins (higher specificity). Do NOT put duration in the
     class or a media query — the shorthand would reset it. -->
<path class="streak" d="M-140,80 L-116,78 …" fill="none" stroke="#818cf8"
      stroke-width="1.6" opacity="0.5"
      style="animation-duration:2.6s;animation-delay:-1.2s"/>
```

Generate ~12–18 streaks: each a polyline sampled across the canvas where
`y = baseY + A·sin(f·x + phase)` (layer two sines for organic drift). Spread
`baseY` to fill the height; cycle palette colors; vary width/opacity/duration.
Extend paths past both edges (start `x < 0`, end `x > width`) so ends never show.

## Effect 2 — twinkling particle dots

A scatter of small circles that pulse in scale/opacity, staggered. Pairs well
with (or replaces) streaks; delta-review uses a dot **grid**.

```svg
<style>
  .dot { transform-box: fill-box; transform-origin: center;
         animation: twinkle ease-in-out infinite; }
  @keyframes twinkle { 0%,100% { transform: scale(0.7); } 50% { transform: scale(1.25); } }
  @media (prefers-reduced-motion: reduce) { .dot { animation: none; } }
</style>
<circle class="dot" cx="480" cy="120" r="1.8" fill="#22d3ee" opacity="0.18"
        style="animation-duration:3s;animation-delay:-2.1s"/>
```

The `opacity` attribute is the static/reduced-motion resting value — keep it low
(0.10–0.25) so dots read as texture, not confetti.

## Effect 3 — aurora / mesh blobs

Large blurred radial-gradient blobs drifting slowly. Calm and premium; good when
streaks would be too busy.

```svg
<circle cx="300" cy="180" r="260" fill="url(#blobA)" opacity="0.5"
        style="filter:blur(40px)">
  <animateTransform attributeName="transform" type="translate"
    values="0 0; 60 -30; 0 0" dur="14s" repeatCount="indefinite"/>
</circle>
```

## Effect 4 — plasma via animated `feTurbulence`

Shader-like organic flow, entirely in an SVG filter. Animate `baseFrequency`
with SMIL. Tint by compositing over an accent gradient; keep opacity low.

```svg
<filter id="plasma">
  <feTurbulence type="fractalNoise" baseFrequency="0.012" numOctaves="2" result="n">
    <animate attributeName="baseFrequency" dur="18s"
             values="0.010;0.016;0.010" repeatCount="indefinite"/>
  </feTurbulence>
  <feColorMatrix in="n" type="matrix" values="0 0 0 0 0  0 0 0 0 0  0 0 0 0 0  0.6 0 0 0 0"/>
</filter>
```

## The scrim (do not skip)

Wherever text sits over the effect, put a gradient rect between them:

```svg
<linearGradient id="scrim" x1="0" y1="0" x2="1" y2="0">
  <stop offset="0" stop-color="#0d1117" stop-opacity="0.96"/>
  <stop offset="0.4" stop-color="#0d1117" stop-opacity="0.82"/>
  <stop offset="0.66" stop-color="#0d1117" stop-opacity="0.28"/>
  <stop offset="1" stop-color="#0d1117" stop-opacity="0"/>
</linearGradient>
<rect width="1280" height="360" fill="url(#scrim)"/>   <!-- above effect, below text -->
```

Text on the left → scrim strong on the left, clearing to the right where the
effect breathes (behind/around a concept-motif card). Flip for right-aligned text.

## Vary the effect per project (do not default to the flow-field)

The effect should suit what the repo *does*; reusing one effect everywhere is the
template trap. Beyond the four above, invent from a wide palette of GitHub-safe
motions (pure CSS/SMIL/filters):

- **reaction–diffusion / metaballs** — organic blobs merging (`feTurbulence` +
  `feDisplacementMap`, or blurred circles) — fluid, graphics, generative, AI.
- **boids / particle swarm** — many dots drifting along a field — data, networks.
- **digital rain / scanline** — falling glyph columns or a sweeping scan bar —
  terminals, security, OCR, recorders.
- **starfield / warp** — points streaking from a vanishing point — speed, perf.
- **mesh-gradient drift** — large soft color regions morphing — design, theming.
- **grid / dot-matrix pulse** — a lattice breathing — infra, databases, tables.
- **waveform / equalizer** — bars rising and falling — audio, streaming, metrics.

Pick or combine what echoes the project, then recolor to its brand. Aim so that no
two heroes share a background.

## Taste rules

- **Effect colors come from the project palette** (`hero-design.md`), not a fixed
  rainbow.
- **Low opacity, behind everything.** If the effect competes with the wordmark,
  turn it down. Legibility beats spectacle.
- **One effect, done well.** Don't stack streaks + plasma + blobs.
- **Slow and calm.** Durations ≥2s; no strobing.
- **Always** reduced-motion gated; the static frame must already look finished.
