# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Static website for **Connivance**, a Rock/Pop/Funk band from Île-de-France. No build step, no dependencies — just a single HTML file served directly.

## Development

Open `index.html` in a browser. Any HTTP server works for local testing:

```bash
python3 -m http.server 8000
```

There are no build, lint, or test commands.

## Architecture

Everything lives in `index.html` (~1530 lines): HTML structure, all CSS (inline `<style>`), and all JavaScript (inline `<script>` at the bottom). There are no separate JS or CSS files.

**Key JS systems (all in the `<script>` block ~line 1250+):**

- **i18n**: The `T` object (line 1256) holds translations for 6 languages (FR, EN, IT, ES, JA, ZH). Any element with a `data-i18n="key"` attribute gets its `innerHTML` swapped by `setLang()`. The default is French. Browser language is auto-detected on first visit; preference is saved to `localStorage`.
- **Scroll effects**: Navbar hides on scroll-down / shows on scroll-up. `.reveal` elements animate in via `IntersectionObserver`.
- **Hero particles**: Procedurally generated floating dots via `#heroParticles`.

**Content structure** (page sections in order): Hero → Next Gig → About → Members → Concerts → Discography → Videos → Listen → Contact.

**Concert pages**: Each concert gets its own directory, e.g. `concert/20260314/index.html`, with a setlist and audio click tracks in a local `clicks/` subdirectory. The top-level `clicks/` holds the master set of MP3 files.

## Adding/updating content

- **Text content**: Update both the HTML fallback text (French) and all language keys in the `T` object.
- **New i18n string**: Add a `data-i18n="key"` attribute to the HTML element, then add the `key` to every language in `T`.
- **New concert page**: Create `concert/YYYYMMDD/index.html` following the existing concert page pattern.

## Styling notes

CSS custom properties are defined at the top of the `<style>` block:
- Primary accent: `#e8922a` (orange)
- Background: `#0e0e14` (near-black)
- Breakpoint for mobile nav (hamburger): `700px`
