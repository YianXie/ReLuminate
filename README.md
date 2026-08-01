# ReLuminate

The website for **ReLuminate** — a youth-led project building AI-powered, sound-first games so visually impaired young people can play, connect, and belong.

**Live site:** [reluminate-global.org](https://reluminate-global.org)

## Mission

Gaming is where young people make friends, build confidence, and unwind. But most games assume perfect vision, locking millions of visually impaired youth out of the spaces where their peers gather.

ReLuminate flips that assumption and designs games around **sound, story, and AI**:

- **Sound-first design** — spatial audio, voice, and rich soundscapes carry the story and the gameplay. The screen is optional.
- **AI that adapts to you** — AI personalizes each story to the player and adapts controls and difficulty in real time.
- **Community & wellness** — multiplayer spaces connect differently abled youth with peers worldwide.

The work maps to **SDG 9** (inclusive innovation and accessible digital infrastructure) and **SDG 11** (inclusive, safe communities — physical and digital).

Founded by **Yian Xie**, a 16-year-old developer and advocate for differently abled youth at the Singapore American School.

## Journey & events

| When | What |
| --- | --- |
| 2024 | ReLuminate is born — the idea takes shape, backed by global youth leadership communities. |
| 2025 | Game prototyping, the first logo and project video, and presentations to global youth networks including LearningPlanet. |
| 2025 | Visit to the **Enabling Village**, Singapore, to study assistive technologies and the everyday challenges visually impaired people face. |
| May 2026 | **UN STI Forum 2026** — joining the Forum's session on science, technology and innovation for sustainable development. |
| July 2026 | **UN HLPF 2026, New York** — a day at the High-Level Political Forum on Sustainable Development (10 July), during the 7–16 July session reviewing SDGs 6, 7, 9, 11 and 17. |

At the HLPF, ReLuminate attended the official session on strengthening alliances for SDG implementation, the *Act, Allocate, Accelerate* side event on eye health convened by the UN Friends of Vision with the IAPB, and the voluntary national reviews. The site's `#hlpf` section covers the day in full.

## Technical overview

Deliberately minimal: **no build step, no package manager, no dependencies, no framework.** The entire site is one file — [`index.html`](index.html) — plus images in `assets/`. Editing the HTML and committing is the whole workflow.

**Structure.** Sections in order: `#top` (hero), `#mission`, `#what`, `#journey`, `#hlpf`, `#founder` (which also carries the footer). A fixed header navigates between them, so every anchor-targeted section carries `scroll-margin-top: 60px`. Content caps at `max-width: 1120px`.

**Styling.** Almost all styling lives in inline `style="..."` attributes — the markup was translated from a visual design tool. The `<style>` block in `<head>` is reserved for the three things inline styles cannot express:

1. `:hover` states, which need `!important` to beat the inline styles.
2. `@media (max-width: 640px)` mobile overrides, targeting elements via `data-*` hooks (`[data-nav]`, `[data-nav-links]`, `[data-tl]`) and section ids.
3. The `rl-float` keyframe used by the decorative hero blobs.

**JavaScript.** One IIFE at the bottom of `<body>`. An `IntersectionObserver` fades and translates in any element tagged `data-reveal`; `data-reveal-delay="120"` staggers siblings. It bails out entirely under `prefers-reduced-motion: reduce`, and leaves elements already in view at load untouched so the hero never flashes.

**Accessibility** is the product, not a nicety. Body text is set in **Atkinson Hyperlegible**, a typeface designed for low-vision readers; headings and buttons use **Sora**. Both load from Google Fonts. Photographs carry descriptive `alt` text, and purely decorative elements (hero gradient blobs, timeline dots) are `aria-hidden="true"`.

**Palette.** Ink `#1f2a33`, blue `#1e4e9c` (hover `#163c7a`), green `#8fc77e` (deep `#5a9647`), cream page `#fbf9f5`, warm section `#f2efe8`, body copy `#4a5661`.

## Running locally

Any static server works:

```bash
python3 -m http.server 8899
```

Then open <http://localhost:8899>.

## Deployment

GitHub Pages from `main` — pushing to `main` publishes. `CNAME` pins the custom domain `reluminate-global.org` and must stay at the repo root.

## License

[MIT](LICENSE) © 2026 Yian Xie
