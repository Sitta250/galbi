# Restaurant Website Design Concept

A reference for building future restaurant websites with the same aesthetic principles.

---

## Core Philosophy

The design should feel like the restaurant itself — restrained, intentional, and confident. Nothing decorative for decoration's sake. Every element earns its place. The goal is to make the food and the space feel elevated, not the website.

---

## Typography

- **Body font:** DM Sans, weight 300 (light). Clean, modern, neutral.
- **No display or decorative serif fonts for headings.** Avoid fonts like DM Serif Display, Playfair Display, or anything with heavy contrast strokes — they feel generic and dated for this aesthetic.
- **Headings** use the same body font (DM Sans), differentiated only by size and letter-spacing, not by font family.
- **Korean text** uses Noto Serif KR. Keep it minimal — only where the Korean name appears (nav, footer brand).
- **No Google Fonts with personality.** No Pacifico, Lobster, or hand-lettered fonts. No fonts that try too hard.
- **Letter-spacing** is your friend. Use generous letter-spacing (`0.1em`–`0.25em`) with uppercase and small sizes instead of bold weight to create hierarchy.
- **Font sizes** should be modest. Section titles around `clamp(1.6rem, 4vw, 2.8rem)`, not huge.

---

## Color Palette

- **Dark base:** near-black ink (`#1a1714`) for the nav and footer.
- **Light base:** warm parchment (`#f2ead8`) or clean white (`#ffffff`) for content sections.
- **Stone/neutral accents:** muted warm grays (`#8a8278`, `#b0a898`) for secondary text and labels.
- **No strong accent colors.** No red, orange, or vibrant hues. If you need an accent, use a slightly warmer or cooler shade of the existing palette.
- **Avoid pure black (`#000000`) and pure white (`#ffffff`) for text** — use near-black and warm white so it feels softer.

---

## Emoji & Icons

- **No emoji anywhere in the UI.** Not in menus, not in section labels, not in CTAs. Emoji reads as casual and undermines the refined aesthetic.
- **Social media icons must be real SVG icons**, not emoji substitutes (no ▣ for Instagram, no Unicode workarounds).
  - Instagram: use the official icon shape — rounded rectangle + circle + dot (`<rect rx="5">` + `<path>` + `<line>`).
  - Use `stroke="currentColor"` so the icon inherits the link's color on hover.
- **Map/location icons:** use a clean SVG pin, not an emoji pin.
- **No star emoji for reviews** — use `★` character or an SVG star if needed, consistently sized.

---

## Layout & Spacing

- **Fixed nav bar** at top, `60px` height, dark background. Contains: logo + restaurant name (left), nav links (right).
- **Nav name:** place the Korean name and English name directly next to the logo as a flex group — do not center them separately in the bar.
- **Section padding:** generous vertical padding (`4rem`–`6rem`) so sections breathe. Never cramped.
- **Max content width:** around `900px`–`1100px`, centered. Don't let text or grids stretch full-width on large screens.
- **Menu grid:** two columns on desktop, single column on mobile. Use a simple CSS grid, no fancy layouts.
- **Consistent gap rhythm:** use `1rem`, `1.5rem`, `2rem`, `2.5rem` — don't introduce arbitrary spacing values.

---

## Navigation

- **Desktop:** logo + name on the left, text links on the right. Links in small uppercase with generous letter-spacing.
- **Mobile:** hide name text and nav links. Show a 3-bar hamburger icon on the right. Tapping opens a slide-in sidebar from the right.
- **Sidebar:** dark background matching nav, links stacked vertically, closes on link tap or overlay tap. Lock body scroll while open.
- **No dropdown menus.** Keep nav flat — if the site is simple enough to be a single page, use anchor links.

---

## Sections & Content

- **Section eyebrow labels** (small uppercase text above headings): use sparingly. If it adds no information, remove it. "What guests say" above "Reviews" is redundant — cut it.
- **Section headings:** can combine two languages inline, e.g. `Speisekarte / Menu`. Feels authentic.
- **Menu items:** use a consistent row pattern — name on the left, price right-aligned. Description in smaller, muted text below the name.
- **Category labels:** small, uppercase, muted, with an em dash prefix (e.g. `— Mittagessen · 점심`). Include Korean alongside German/English where appropriate.
- **Numbered items** (like a lunch set menu M1–M5): include the number as part of the item name, not as a separate column.

---

## Photography & Media

- **Photo frames:** use `aspect-ratio` to enforce consistent proportions (portrait `4/5` for food/interior shots).
- **Auto-cycling photo gallery:** 3 frames, staggered timers (e.g. 4.2s / 5.1s / 3.7s), 1s CSS fade transition. Frames should never all switch at the same time.
- **Section transitions:** avoid heavy gradient blends between sections unless the background color shift is dramatic. When sections share the same background color, no blend is needed.
- **Gallery illustration or brand art:** if the restaurant has a signature illustration or hand-drawn logo, give it its own full-width section.

---

## Tone & Copy

- **Short and direct.** Descriptions in the menu should be one line. No paragraph-length item descriptions.
- **Bilingual where it matters:** German + Korean for a Korean restaurant in Germany. English tab as an option, not the default.
- **No marketing language.** No "experience the flavors of Korea" type copy. Let the food names speak.
- **Phone numbers:** display in a readable format (e.g. `030 5173 1828`) even if the `href` uses the raw format (`tel:+4930051731828`).

---

## What to Avoid

- No emoji in any UI text
- No placeholder icons (▣, ♦, Unicode shapes as icons)
- No heavy/decorative serif display fonts for headings
- No rainbow accent colors or gradients that don't serve a purpose
- No glassmorphism, drop shadows on text, or neon glows
- No large hero text that screams — keep headings calm
- No auto-playing video backgrounds
- No cookie banners or pop-ups unless legally required
- No animations that aren't subtle (fade/reveal on scroll is fine; bouncing or spinning elements are not)
- No sticky elements other than the nav bar
- No unnecessary eyebrow labels — if the heading already says what it is, remove the label above it

---

## Reusable Patterns

```
Nav:        [Logo + Name (flex left)] .............. [Links (right)] [Hamburger mobile]
Hero:       Full-viewport, centered logo/wordmark, no text overlay
Section:    Section heading (centered) → content grid
Menu row:   [Item name + description] .... [Price]
Photo grid: 3 equal frames, cycling, staggered intervals
Footer:     Dark bg · Brand name + tagline + Instagram (left) · Location (center) · Hours + Contact (right)
```

---

## Technical Notes

- Single HTML file is fine for a restaurant site of this scale. No framework needed.
- Use CSS custom properties (`--ink`, `--parchment`, etc.) for all colors from the start.
- `clamp()` for font sizes and container widths — avoids breakpoint clutter.
- Use `IntersectionObserver` for scroll-reveal animations. Threshold `0.1`, stagger with `setTimeout`.
- Photo cycling: vanilla JS with `setInterval`, preload images with `new Image()`, toggle `.active` class with CSS `opacity` transition.
- Mobile breakpoint: `680px` covers phones. A single breakpoint is usually enough for a site like this.
- Sidebar: toggle `.open` class, lock scroll with `document.body.style.overflow = 'hidden'`.
