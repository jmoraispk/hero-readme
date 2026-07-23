# README structure around the hero

The hero earns attention; the body has to keep it and stay honest. Follow the
project's existing README voice — improve structure, don't flatten personality.

## Skeleton (top to bottom)

```markdown
<div align="center">

<!-- Single adaptive SVG: -->
<img src="assets/hero.svg" alt="<name> — <one-line tagline>" width="100%">

<!-- …or, for structurally different dark/light art: -->
<!--
<picture>
  <source media="(prefers-color-scheme: dark)"  srcset="assets/hero-dark.svg">
  <img alt="<name> — <one-line tagline>" src="assets/hero-light.svg" width="100%">
</picture>
-->

# <name>

**<one honest sentence about what it is and who it's for>**

<!-- badges: ONLY real ones (see honesty rules) -->

</div>

## Quickstart

<smallest thing that gets someone to "it works">

## Usage / Examples

<the 2–3 real things it does, with runnable snippets>

## Features

<honest bullets — only what's shipped>

## Installation / Configuration    <!-- if non-trivial -->

## Contributing / License          <!-- if applicable -->
```

Add a Table of Contents only if the README is long enough to need one. Omit any
section a project doesn't warrant — an empty "Roadmap" is worse than no section.

## Placement rules

- Hero is the **first thing** in the file, centered via `<div align="center">`.
- Immediately restate name + tagline as real text (indexing, screen readers,
  people who block images).
- The `alt` text is `"<name> — <tagline>"`, not "hero image".

## Honesty rules (non-negotiable)

The hero must not oversell and the copy must not lie.

- **Badges only if real.** A CI badge requires real CI. Version/downloads badges
  require a real published package. Never paste a "build: passing" badge you
  can't back. When in doubt, leave it out.
- **Features only if shipped.** No aspirational or roadmap items dressed as
  current capabilities.
- **Claims must be checkable.** "Fast", "secure", "zero-config" need to be true
  and, ideally, evidenced. Delete adjectives you can't defend.
- **Don't invent** license, author, or links. Read them from the repo.

A gorgeous hero on top of dishonest copy makes the whole project look worse, not
better. Authenticity is the through-line from image to text.
