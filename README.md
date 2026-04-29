# ridho.atlas

Personal portfolio for [Muhammad Ridho Putra](https://github.com/putraridho), Senior Frontend Engineer.

A cockpit-themed "career atlas" — each past role is a planet orbiting in 3D, the operator is the central sun. Single self-contained HTML file. Three.js + GSAP, no build step.

## Features

- Six orbiting position planets + central about-sun
- Radar mini-map with click-to-navigate
- Drag to rotate camera, scroll wheel to zoom
- Career timeline inside each panel for cross-navigation between positions
- Smart intro: full ~5s on first visit, fast ~1.5s on return, instant for `prefers-reduced-motion`
- Soft-lock targeting reticle tracks the cursor and shows the nearest position ID
- Auto-aging tenure (the `9+ yrs` count recomputes from a single constant)
- Mobile responsive (HUD compresses, brand mark stacks to two lines)
- SEO: meta tags, Open Graph, Twitter Card, JSON-LD Person schema, crawler-readable semantic content

## Customize

All content lives in the inline `<script>` block. Three things to edit:

**`projects[]`** — past positions. Each entry:

```js
{
  id: 'pos-001',
  title: 'jitera',
  period: '2025–PRESENT',
  start: 2025, end: null,        // null = current
  tag: 'SENIOR FRONT-END SPECIALIST · ACTIVE',
  color: 0xff5a3a,               // hex, no quotes
  size: 0.62, orbit: 3.2, angle: 0.4,
  active: true,
  desc: '...',
  meta: [['stack', '...'], ['since', '...']],
  links: [{ label: 'company', url: '...' }]
}
```

**`aboutData`** — bio and contact info shown when the central sun is engaged. Same shape as a position, plus `isAbout: true`.

**`CAREER_START`** — start year. Drives the auto-aged `9+ yrs` count in the about-card, ticker, and intro corner.

Theme colors are CSS variables in `:root` at the top of the `<style>` block.

## Accessibility

- `prefers-reduced-motion` skips the intro and stops planet/wireframe rotation
- Keyboard navigation: Tab/Shift-Tab cycles positions, Enter/Space engages, Esc disengages, Arrow keys rotate the camera
- Semantic content (h1, h2, role list, contact links) lives in a `.visually-hidden` block — readable by crawlers and screen readers, invisible to sighted users

## Built with

[Three.js](https://threejs.org) · [GSAP](https://gsap.com) · Major Mono Display · Share Tech Mono · Chakra Petch