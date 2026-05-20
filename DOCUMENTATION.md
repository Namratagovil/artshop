# Namrata Agarwal — Art Portfolio: Build Documentation

## Overview

A single-page illustration and photography portfolio for Namrata Agarwal, built with vanilla HTML, CSS, and JavaScript — no frameworks, no build tools, no backend. The site is fully self-contained in `index.html` and a two-folder asset structure.

---

## Technology Stack

| Concern | Solution |
|---|---|
| Markup | Semantic HTML5 |
| Styling | Vanilla CSS (custom properties, CSS Grid, Flexbox) |
| Scripting | Vanilla ES2020 JavaScript (no libraries) |
| Fonts | Google Fonts — Inter (300, 400, 500, 600) |
| Form delivery | [Formspree](https://formspree.io) (no backend required) |
| Hosting | GitHub Pages (static) |

---

## Project Structure

```
artshop/
├── index.html           # Entire site (HTML + CSS + JS in one file)
├── README.md            # Repository readme
├── DOCUMENTATION.md     # This file
├── assets.json          # Asset manifest with titles, prices, and metadata
├── assets_art/          # Original artwork images (37 files, .JPG / .jpg)
└── assets_photographs/  # Photography images (26 files, .JPG)
```

---

## Build History — Step by Step

### Step 1 — Initial single-page portfolio (`8908fd5`)
- Created `index.html` from scratch with a responsive 4-column gallery grid.
- Implemented sticky header with desktop nav links and a hamburger menu for mobile.
- Added hero section with artist intro, about section, and a contact section.
- Used CSS custom properties for a consistent design token system (`--black`, `--mid`, `--light`, etc.).
- Built a JavaScript lightbox (`<dialog>`-style overlay) for full-size image viewing, with keyboard navigation (Escape closes, Tab traps focus).
- Added a contact form with inline validation (required fields, email format check).
- Made fully accessible: skip-link, ARIA labels, `focus-visible` outlines, `role="dialog"`, `aria-modal`.

### Step 2 — Real artwork and photograph assets (`a8186a0`)
- Added 37 original artwork files to `assets_art/`.
- Added 26 photography files to `assets_photographs/`.
- Replaced placeholder `<img>` sources with real asset paths throughout the gallery grids.

### Step 3 — Art / Photographs tabs (`6d4847f`)
- Split the single gallery into two tabbed panels: **Art** and **Photographs**.
- Added `.gallery-panel` / `.gallery-panel.active` CSS toggle.
- Wired tab links with a `showPanel()` JavaScript function.
- URL hash (`#art`, `#photographs`) is honoured on page load and updated on tab change via `history.replaceState`.
- Mobile nav also wired to the tab system.

### Step 4 — Contact form: mailto fallback (`c55c665`)
- Switched the contact form submit handler from a broken Formspree placeholder to a `mailto:` link that opens the user's mail client with pre-filled subject and body.

### Step 5 — Photograph naming from image content (`d2b874f`)
- Reviewed each photograph file and assigned descriptive captions based on image content (e.g. `100_0589.JPG` → "Fishing Boat", `DSC00046.JPG` → "Fatehpur Sikri").

### Step 6 — Order Flow with Formspree modal (`current`)
- **Order button**: Added an `"Order Painting"` button to every Art gallery card. The button appears on hover (top-right corner), styled as a small pill against the image. Photographs do not have order buttons (they are not for sale).
- **Pricing data**: Each art card now carries `data-title` and `data-price` HTML attributes. Prices are placeholder values in GBP — update them directly in `index.html` or in `assets.json` and re-sync.
- **Order modal**: A sleek slide-up modal (`role="dialog"`, `aria-modal="true"`) with a dark blurred backdrop. When opened it auto-fills the painting title and price from the card's data attributes.
- **Form fields** (inside the modal):
  - Hidden: `painting_title`, `painting_price` (pre-filled, sent with every submission)
  - Visible required: Name, Email, Shipping Address
  - Visible optional: Message
- **Formspree delivery**: The modal form posts via `fetch()` to `https://formspree.io/f/xoqpkyor`. On success the form is hidden and a confirmation message is shown inline — no page reload or redirect. On network error a fallback `alert()` prompts direct email contact.
- **No checkout / no payment**: The order note at the bottom of the modal makes clear that no payment is collected here — it is purely an inquiry that the artist confirms manually.
- **Accessibility**: Focus is trapped inside the modal, Escape closes it, focus returns to the triggering button on close.
- **Documentation & assets manifest**: Created `DOCUMENTATION.md` (this file) and `assets.json`.

---

## How to Update Prices

Prices live in two places. Update both to stay in sync:

1. **`index.html`** — find the art `<div class="gallery-card">` for the painting and change `data-price="£XXX"`.
2. **`assets.json`** — find the matching entry in `"art"` array and change `"price"`.

---

## How to Swap the Formspree Endpoint

1. Create a free account at [formspree.io](https://formspree.io) and create a new form.
2. Copy the form ID (the part after `/f/` in the endpoint URL).
3. In `index.html`, find:
   ```html
   <form class="order-form" id="orderForm" action="https://formspree.io/f/xoqpkyor"
   ```
   Replace `xoqpkyor` with your real form ID.

---

## Responsive Breakpoints

| Breakpoint | Gallery columns | Notes |
|---|---|---|
| > 1024 px | 4 | Desktop default |
| 769 – 1024 px | 3 | Tablet landscape |
| 481 – 768 px | 2 | Tablet portrait / large mobile |
| ≤ 480 px | 1 | Mobile |

---

## Accessibility Checklist

- [x] Skip-to-content link
- [x] All images have descriptive `alt` text
- [x] Interactive elements meet 44 × 44 px touch target minimum
- [x] Focus styles visible on all interactive elements (`focus-visible`)
- [x] Lightbox: `role="dialog"`, `aria-modal`, focus trapped, Escape closes
- [x] Order modal: `role="dialog"`, `aria-modal`, focus trapped, Escape closes
- [x] Form fields have associated `<label>` elements
- [x] Required fields marked with `aria-required="true"`
- [x] Error messages linked via `aria-describedby`
- [x] Mobile nav toggle updates `aria-expanded` and `aria-label`
