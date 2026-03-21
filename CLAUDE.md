# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for **Alien Moon** (psychedelic rock/dance band, Netherlands) with a companion **Crazy Cow** (Neil Young tribute) sub-site. No build system — pure HTML/CSS/vanilla JS, deployed automatically to GitHub Pages on every push to `main`.

## Development

Open files directly in a browser or use any static file server:
```bash
python3 -m http.server 8080
```

No build, compile, lint, or test steps.

## Architecture

### Dual-Brand Structure

Two parallel sites sharing the same layout pattern:
- `/` — Alien Moon (neon cyberpunk aesthetic)
- `/crazycow/` — Crazy Cow (warm vintage/sepia aesthetic)

Each site has:
- `index.html` — main page
- `gallery.html` — photo gallery
- `data.json` — all dynamic content (events, socials, about, video, photos, members, contact)

### Data-Driven Rendering

Pages fetch their local `data.json` on load and call a `render()` function that populates the HTML. All content changes (events, photos, social links, member info) should be made in `data.json`, not in HTML.

`data.json` event object fields: `date`, `time`, `venue`, `address`, `city`, `note`, `poster` (image URL for poster, optional).

### Layout

Fixed split-panel layout:
- **Left panel** (380px): sticky band branding, nav, social links
- **Right panel**: scrollable content area (scroll target is `.right-panel`, not `window`)

Navigation uses `data-scroll` attributes on `<a>` elements; click handlers smooth-scroll within `.right-panel`.

Responsive breakpoint at 768px — switches to single-column vertical layout.

### Key Differences Between Sites

- **Alien Moon**: Shows only the first event with a poster; includes a YouTube embed (video ID from `data.json`) and a mailing list signup form.
- **Crazy Cow**: Shows all events that have posters; includes a band members grid.

### Fonts & Colors

- **Alien Moon**: Bebas Neue + Space Mono; cyan `#00f5c4`, purple `#7b2fff`, pink `#ff3c6e`
- **Crazy Cow**: Rye + Playfair Display; amber `#c8920a`, warm browns
