# Copilot Instructions – Investor Deck Generator

## Product Context

This project is a static HTML/CSS investor presentation deck for **Dugout Howe Complex**, a youth sports facility in Howe, TX operated by **Pine Tar Sports** (contact: Tim Truman, 491 Morrison Rd, Howe, TX 75459).

The deck is a self-contained, browser-based slide show used to pitch the investment opportunity to prospective investors. Each slide is a standalone HTML file. The presentation covers the business overview, market opportunity, revenue model, financial projections, investment tiers, and a call to action.

**All financial language must comply with SEC/regulatory standards.** Use "target" or "projected" instead of "guaranteed" when describing investment returns.

## Tech Constraints

- **Pure static HTML/CSS** – no JavaScript frameworks, no build tools, no package managers.
- **No server-side code** – all files are served directly from the filesystem or a static host.
- **External CDN dependencies only:**
  - Font Awesome 6.0.0-beta3 (icons): `https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css`
  - Google Fonts (Montserrat + Open Sans): loaded via `@import` in `manus.css`
- **Images** are stored in the `images/` directory and referenced with relative paths.
- Target display resolution is **1280×720px** (16:9 slide format). Slides must also be responsive down to 480px via media queries in `manus.css`.

## Architecture Rules

- **One HTML file per slide.** Slides are named: `index.html`, `slide-01.html`, `slide-01a.html`, `slide-02.html` … `slide-09.html`, `slide-09-1.html`, `slide-10.html`.
- **Linear navigation only.** Each slide links to the previous and next slide using `.nav-btn` anchor elements inside `.nav-buttons`. The first slide hides its prev button; the last slide hides its next button.
- **Shared stylesheet.** All slides link to `manus.css` for base styles. Slide-specific overrides are written in a `<style>` block within the individual HTML file.
- **CSS variables are the source of truth for all colors and shadows.** Never use hardcoded hex or rgba values in slide files or `manus.css` when a variable already exists. Defined in `:root` inside `manus.css`:
  - Brand: `--color-primary` (#002D62 Navy), `--color-accent` (#C41E3A Red), `--color-secondary` (#89CFF0 Light Blue)
  - Semi-transparent backgrounds: `--color-accent-bg`, `--color-primary-bg`, `--color-category-1-bg`, `--color-category-2-bg`, `--color-category-3-bg`
  - Shadows: `--shadow-soft`, `--shadow-medium`
- **Slide container dimensions are fixed at 1280×720px** via `.slide-container` in `manus.css`. Do not override width/height on individual slides.
- When adding a new slide, follow the existing file naming convention and insert the slide into the navigation sequence by updating the prev/next links on the adjacent slides.

## Coding Style

- **HTML** – use semantic elements where possible; keep indentation at 4 spaces.
- **CSS** – use CSS variables from `manus.css` for all brand colors and backgrounds; keep slide-specific `<style>` blocks scoped to that file; do not modify `manus.css` for one-off overrides.
- **No inline styles** for colors or layout unless strictly necessary for dynamic/computed values (e.g., `display: none` on the hidden nav button).
- Keep slide markup clean and readable; avoid deeply nested wrappers.
- Maintain consistent class naming already in use: `.slide-container`, `.header-section`, `.content-section`, `.nav-buttons`, `.nav-btn`, etc.
- Investment figures and percentages should match across all slides for consistency.

## Output Expectations from Copilot

- Produce complete, ready-to-use HTML/CSS that follows all rules above without requiring follow-up edits.
- When creating or editing a slide, output the **full file content** so it can be saved directly.
- **Include helpful inline comments only where behavior is non-obvious** (e.g., a clip-path value, a z-index stacking rationale, or a workaround for a browser quirk). Do not comment self-explanatory markup.
- Never introduce new external dependencies (CDNs, fonts, libraries) without explicit approval.
- Always use "target" or "projected" (never "guaranteed") for investment return language.
- **Take a screenshot (or verify visually in a browser) when done implementing a change and when reviewing code**, so the visual result can be confirmed before the work is considered complete.
- When updating navigation links, verify the full slide sequence is unbroken.
