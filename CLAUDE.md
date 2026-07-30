# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page marketing site for ReLuminate, a youth-led project building AI-powered, sound-first games for visually impaired players. The entire site is one file: [index.html](index.html) (~1400 lines) plus three files in `assets/`.

There is no build step, no package manager, no dependency, and no test suite. Editing `index.html` and committing is the whole workflow.

## Commands

Preview locally (any static server works; port 8899 is already allowlisted in `.claude/settings.local.json`):

```bash
python3 -m http.server 8899
```

Deployment is GitHub Pages from `main` — pushing to `main` publishes. `CNAME` pins the custom domain `reluminate-global.org`, so it must stay at the repo root.

## Architecture

**All styling is inline `style="..."` attributes.** The markup was translated from a visual design tool, which is why nearly every element carries a long inline style. The `<style>` block in `<head>` is reserved for the three things inline styles cannot express:

1. `:hover` states — these need `!important` to beat the inline styles (`.nav-link`, `.btn-primary`, `.btn-outline`, `.btn-nav`, `.btn-survey`).
2. `@media (max-width: 640px)` mobile overrides, which target elements via `data-*` hooks (`[data-nav]`, `[data-nav-links]`, `[data-tl]`) and section ids.
3. The `rl-float` keyframe used by the decorative hero blobs.

So: a new hover or responsive behavior goes in the `<style>` block keyed off a class or `data-` attribute; everything else goes inline next to the element.

**Scroll reveal** is the only JavaScript — an IIFE at the bottom of `<body>`. Any element tagged `data-reveal` is faded/translated in by an `IntersectionObserver`; `data-reveal-delay="120"` staggers siblings (used on the "What we do" cards). Two behaviors to preserve when touching it: it bails out entirely under `prefers-reduced-motion: reduce`, and it leaves elements already in view at load untouched so the hero never flashes.

**Section layout.** Sections in order: `#top` (hero), `#mission`, `#what`, `#journey`, `#founder`, `#contact` (also the footer). The nav is `position: fixed`, so every anchor-targeted section carries `scroll-margin-top: 60px` — keep that on any new section, and add its id to the mobile padding rule in the `<style>` block. Content sections cap at `max-width: 1120px` with `margin: 0 auto`.

The `#journey` timeline is five repeated `data-tl` grid rows (`92px 28px 1fr`: year / dot-and-rail / copy). The mobile media query narrows that grid, so new entries must keep both the `data-tl` attribute and the same column template.

## Design constraints

Accessibility is the product, not a nicety — this is a site about visually impaired players, and the copy explicitly calls out its own typeface choice.

- Body text is **Atkinson Hyperlegible** (chosen for low-vision readers); headings, labels, and buttons are **Sora**. Both load from Google Fonts. In inline styles the family is written with escaped quotes: `font-family: &quot;Sora&quot;, sans-serif`.
- Palette: ink `#1f2a33`, blue `#1e4e9c` (hover `#163c7a`), green `#8fc77e` (deep `#5a9647`), cream page `#fbf9f5`, warm section `#f2efe8`, body copy `#4a5661`. Reuse these rather than introducing new hues.
- Decorative elements (hero gradient blobs, timeline dots) carry `aria-hidden="true"` where they are purely visual.

The call-to-action is an external Google Form (`https://forms.gle/...`) in `#contact`, duplicated as the "Survey" pill in the nav.
