# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static company website for **swint.ai** — an AI software and consulting company. HTML and JavaScript live in `index.html`; CSS is fully extracted into the `css/` folder tree.

## Development

No build tools or dependencies. Open `index.html` directly in a browser, or serve it locally:

```bash
# Python
python -m http.server 8080

# Node (if installed)
npx serve .
```

## Architecture

### File structure

HTML and JavaScript live in `index.html`. CSS is split across `css/utils/`, `css/components/`, and `css/pages/`. The `js/`, `pages/`, and `components/` folders are scaffolded for future use.

### Page sections (in order)

`nav` → `hero` → `.ticker` → `.value-section` → `.services-section` → `.why-section` → `.serve-section` → `.cta-section` → `footer`

### Two canvas animations

- `#heroCanvas` — ambient particle network across the full hero background. Particles connect via lines when within `CONN_DIST = 85px`.
- `#markCanvas` — the animated hexagon logo mark on the hero right. Nodes defined in `mAll[]`, edges in `mEdges[]`, particles travel along edges via `MPart` class with easing. `MRipple` pulses originate from the center node.

Both run their own `requestAnimationFrame` loops (`heroLoop`, `markLoop`) independently.

### Design tokens

All colors live in `:root` CSS custom properties in `css/utils/variables.css`. The primary palette:

- `--navy` / `--navy2` / `--navy3` — dark backgrounds (light → darkest)
- `--cyan: #00C2FF` — primary accent
- `--sky: #4DA8DA` — secondary accent

### Font stack

- `Plus Jakarta Sans` — headings, logo, buttons, tab labels
- `Outfit` — body copy
- `Rajdhani` — eyebrows, nav links, labels, footer — always uppercase + letter-spacing

### Responsive strategy

Breakpoints in `css/pages/home.css` and `css/components/navbar.css`:

- `1024px` — hero collapses to single column; value grid stacks
- `768px` — nav links hidden, hamburger shown; service tabs stretch full width
- `480px` — hero buttons stack vertically; canvas shrinks
- `360px` — service tabs go vertical

### Service tabs

JS function `switchTab(name, btn)` toggles `.active` on `.svc-panel` elements (`#panel-build`, `#panel-automate`, `#panel-optimize`) and `.stab` buttons.

## Scaffolded folders (not yet used)

| Path | Intended use |
| --- | --- |
| `pages/` | Additional HTML pages (about.html, services.html, etc.) |
| `components/` | Shared HTML partials loaded via `fetch()` (navbar, footer) |
| `data/` | JSON content files (team, services, case studies) |
| `js/vendor/` | Third-party libraries (e.g. GSAP, Alpine.js) if added |
| `assets/images/{logo,team,clients,icons}/` | Categorised image assets |
