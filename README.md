# Flowstate

A single-page corporate website built with [Astro](https://astro.build). Designed for professional services firms — fully static, fast, and easy to customise.

---

## Features

- **Single-page layout** with 8 distinct sections: Hero, About, Purpose, Clients & Sectors, Board & Team, Why Us, Contact, and Footer
- **Scroll-triggered entrance animations** — 8 unique transitions (fade-up, slide-in, blur-in, 3D flip, squeeze reveal, staggered children) powered by a single `IntersectionObserver`
- **Hero word-by-word float-up** — each element on the hero animates in sequence using CSS keyframes with staggered delays
- **Hardware-accelerated only** — all animations use `transform`, `opacity`, and `filter` exclusively; zero layout shift (CLS = 0)
- **Reusable animation system** — `--anim-delay` and `--stagger-offset` CSS custom properties let you tune timing per-element inline
- **Responsive** — mobile-friendly layout with hamburger navigation
- **`prefers-reduced-motion` support** — all animations are disabled for users who prefer reduced motion
- **Google Fonts** — Playfair Display (display) + Inter (body)

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Framework | [Astro](https://astro.build) v7 |
| Styling | Vanilla CSS (design tokens via CSS custom properties) |
| Animations | CSS keyframes + Intersection Observer API |
| Fonts | Google Fonts (Playfair Display, Inter) |
| Node | ≥ 22.12.0 |

---

## Project Structure

```
/
├── public/
│   └── favicon.svg
├── src/
│   ├── assets/
│   ├── components/
│   │   └── Welcome.astro
│   ├── layouts/
│   │   └── Layout.astro
│   └── pages/
│       ├── index.astro
│       └── flowstate-advisor.astro   ← main page
└── package.json
```

All page content (copy, team data, service items) is defined as typed constants in the Astro frontmatter at the top of `flowstate-advisor.astro`. No external CMS or database is required.

---

## Getting Started

```bash
# Install dependencies
npm install

# Start the dev server (runs in background)
npx astro dev --background

# Check dev server status
npx astro dev status

# View logs
npx astro dev logs

# Stop the dev server
npx astro dev stop
```

The site is available at **http://localhost:4321**.

---

## Commands

| Command | Action |
| :--- | :--- |
| `npm install` | Install dependencies |
| `npm run dev` | Start local dev server at `localhost:4321` |
| `npm run build` | Build production site to `./dist/` |
| `npm run preview` | Preview production build locally |
| `npm run astro ...` | Run Astro CLI commands |

---

## Animation System

Animations are controlled by two mechanisms:

### 1. Scroll-triggered (`data-anim`)
Add a `data-anim` attribute to any element. The `IntersectionObserver` adds `.is-visible` when the element reaches 20% in the viewport.

```html
<section data-anim="fade-up" style="--anim-delay: 0.4s;">
```

| Value | Effect |
| :--- | :--- |
| `fade-up` | Fade in + slide up |
| `slide-left` | Slide in from left |
| `slide-right` | Slide in from right |
| `scale-up` | Zoom in from 88% |
| `blur-in` | Defocus → sharp |
| `flip-in` | 3D rotateX flip |
| `squeeze` | Horizontal squeeze reveal |
| `stagger` | Children float up in sequence |

**Custom properties:**

| Property | Default | Description |
| :--- | :--- | :--- |
| `--anim-delay` | `0s` | Delay before transition begins |
| `--stagger-offset` | `0s` | Base delay added to all stagger children |

### 2. Hero on-load (`hw` classes)
The hero section uses pure CSS keyframe animations with staggered `animation-delay` values — no JavaScript required.

```html
<p class="hero-eyebrow hw hw-1">...</p>
<h1>
  <span class="hw hw-2">Title</span>
  <em class="hw hw-3">Subtitle</em>
</h1>
```

Classes `hw-1` through `hw-7` map to delays from `0.15s` to `2.30s`.

---

## Customisation

All content is in the Astro frontmatter of [`src/pages/flowstate-advisor.astro`](src/pages/flowstate-advisor.astro):

- **`firm`** — company name, tagline, contact details
- **`aboutPillars`** — Vision / Mission / Philosophy cards
- **`purposeItems`** — service lines with descriptions and tags
- **`targetColumns`** — Private Sector / Public Sector client lists
- **`industries`** — industry vertical cards with images
- **`board`** / **`team`** — people cards with photos
- **`differentiators`** — "Why Us" bullet points

Design tokens (colours, fonts, spacing) are all in `:root` CSS custom properties at the top of the `<style>` block.

---

## Deployment

```bash
npm run build
```

Output is in `./dist/` — deploy to any static host (Netlify, Vercel, Cloudflare Pages, AWS S3, etc.).

---

## License

Private. All rights reserved.
