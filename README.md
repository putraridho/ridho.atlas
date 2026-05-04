# ridho.atlas

Personal portfolio for [Muhammad Ridho Putra](https://github.com/putraridho), Senior Frontend Engineer.

A mech-OS career atlas — past positions are planets orbiting in 3D, the operator is the central sun, the whole interface is dressed as a Gundam-style cockpit display. Single self-contained HTML file. Three.js + GSAP via ES modules, no build step.

Live: <https://putraridho.github.io/ridho.atlas/>

## Features

- Six orbiting position planets + central about-sun (the active position glows hottest)
- Radar mini-map (top-down orbit view) with click-to-navigate and bearing markers
- Drag to rotate camera, scroll to zoom, click planets to engage
- Career timeline strip inside each panel for cross-navigation between positions
- Soft-lock targeting reticle that tracks the cursor, fires an acquisition flash when in range, and reads the locked target's ID
- Mech-OS chrome: warm-red palette, scan-lines, CRT scan-band drift, hex-cut panel corners, dense HUD readouts, glitch-flicker on alert indicators
- Boot sequence: full intro splash → ~10s ceremonial wake-up choreography (sun stepped ignition → orbit rings → planets chronological → active climax → HUD assembly)
- Smart routing: full intro on first visit, ~4s fast wake-up on return, instant for `prefers-reduced-motion`
- Side panel arrives via mech glitch reveal (chromatic aberration + opacity flicker), exits the same way
- Auto-aging tenure (the `9+ yrs` count recomputes from a single constant)
- Custom warm triangle cursor (mech-OS palette, amber on engageable elements)
- Mobile responsive (HUD compresses, brand mark stacks, side panel goes full-width)
- SEO: meta tags, Open Graph, Twitter Card, JSON-LD Person schema, crawler-readable semantic HTML block

## Customize

All content lives inline. Three things to edit:

**`projects[]`** — past positions. Each entry:

```js
{
  id: 'pos-001',
  title: 'jitera',
  period: '2025–PRESENT',
  start: 2025, end: null,        // null = current
  tag: 'SENIOR FRONT-END SPECIALIST · ACTIVE',
  color: 0xff5a3a,               // hex literal (active position should be warm)
  size: 0.62, orbit: 3.2, angle: 0.4,
  active: true,
  desc: '...',
  meta: [['stack', '...'], ['since', '...']],
  links: [{ label: 'company', url: '...' }]
}
```

The active position should be warm-coloured (`0xff5a3a`-ish) — the ceremonial intro climaxes on it specifically. Inactive positions can be cooler tones; they all get HDR-bright cores and bloom regardless.

**`aboutData`** — bio + contact info shown when the central sun is engaged. Same shape as a position, plus `isAbout: true`.

**`CAREER_START`** — start year. Drives the auto-aged `9+ yrs` count in the about-card, HUD-bl mech-OS readout, ticker, and intro corner. The seven SEO meta strings are still hardcoded and need a manual bump each year — they're read before any JS runs.

Theme tokens are CSS variables in `:root` (top of the `<style>` block):

- `--warm` / `--warm-2` — primary system color (mech-OS scarlet)
- `--amber` — highest-alert highlight (active counters, lock-acquired readouts)
- `--cyan` — secondary status only (demoted from earlier "calm cockpit" version)
- `--ink` / `--ink-soft` / `--ink-dim` — text hierarchy

## Accessibility

- `prefers-reduced-motion` skips the intro and stops idle animations (planet rotation, wireframe spin, scan-band drift)
- Keyboard nav: Tab/Shift-Tab cycles positions, Enter/Space engages, Esc disengages, Arrow keys rotate camera
- Semantic content block (`<div class="visually-hidden">`) holds `h1`, `h2`, role list, and contact links in real text — readable by crawlers and screen readers, invisible to sighted users
- Mech-OS readout text uses hard 1px outline shadows for legibility against bright bloom

## Architecture notes

- Single HTML file (~2800 lines) — easier to deploy and harder to fork than a build-system project, deliberately
- ES modules via importmap so post-processing (UnrealBloomPass, custom chromatic aberration ShaderPass) can be properly imported
- The wake-up choreography is one giant `gsap.timeline` with explicit phase labels — see `runIntro()` for the canonical sequence; `runFastIntro()` is its compressed mirror; `skipIntroDirect()` is the reduce-motion path
- Sun ignition decomposes the sun group into `sunCore` / `sunWire` / `sunHalo` so each part can be driven independently for the slow-burn effect
- All planet HDR brightness is multiplied via `MeshBasicMaterial.color.multiplyScalar(...)` with `toneMapped: false` so bloom catches them at intensities greater than 1.0

## Built with

[Three.js](https://threejs.org) · [GSAP](https://gsap.com) · Major Mono Display · Share Tech Mono · Chakra Petch
