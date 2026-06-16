# All India Milli Council — Website

A single-file, responsive landing page for the **All India Milli Council (AIMC)**, built as a holding/placeholder site while the full website is under construction. It includes an auto-sliding hero carousel, a bilingual (English/Urdu) Aims & Objectives section, an auto-sliding Current Affairs news carousel with detailed read-more modals, and a complete contact footer.

## Live Structure

The entire site lives in **one HTML file** (`index.html`) with embedded CSS and JavaScript — no build step, no framework, no bundler. Open it directly in a browser or deploy it to any static host.

```
project-root/
├── index.html
└── images/
    ├── smallLogo.svg
    ├── logoFull.jpeg
    ├── foundation_day.jpeg
    ├── foundation_day_2.jpeg
    ├── constitution_rights.jpeg
    ├── alam_memorial_collage.jpeg
    ├── dr_alam_sonia.jpeg
    ├── hero1.jpeg
    ├── hero2.jpeg
    ├── photo.jpeg
    ├── alam_memorial_1.jpeg
    ├── alam_memorial_2.jpeg
    ├── aims_objective_eng.jpeg
    └── aims_objective_urdu.jpeg
```

> **Important:** All image paths in `index.html` are relative (`images/...`). Place every file above inside an `images/` folder sitting next to `index.html`, or the page will render with broken images.

## Features

### 1. Sticky Navigation
A frosted-glass nav bar with the AIMC logo (`smallLogo.svg`), organisation name, and quick links to News, About, and Contact sections. Stays pinned to the top while scrolling.

### 2. "Under Construction" Banner
A gold-toned notice bar directly beneath the nav, communicating that the full site is still in development, with a pulsing "Launching Soon — InshaAllah" badge.

### 3. Hero Section — Auto-Sliding Image Carousel
A full-bleed carousel cycling through seven photos:

| # | Image | Caption |
|---|---|---|
| 1 | `foundation_day.jpeg` | 33rd Foundation Day Celebrations |
| 2 | `foundation_day_2.jpeg` | 33rd Foundation Day Celebrations |
| 3 | `constitution_rights.jpeg` | Constitution Rights of Minorities |
| 4 | `alam_memorial_collage.jpeg` | Memorial of Dr. Mohammad Manzoor Alam |
| 5 | `dr_alam_sonia.jpeg` | Dr. Alam with Sonia Gandhi |
| 6 | `hero1.jpeg` | AIMC Annual General Body Meeting |
| 7 | `hero2.jpeg` | National Convention – Save the Constitution |

**Mixed aspect ratios (portrait + landscape) are handled automatically.** Each slide renders the photo in full via `object-fit: contain`, while a blurred, darkened copy of the same image fills the surrounding space as a backdrop — so no image is ever cropped or stretched, regardless of orientation.

- Auto-advances every **4 seconds**
- Pauses on mouse hover, resumes on mouse leave
- Clickable dot indicators for direct navigation
- An "Est. 1992" stat pill overlays the carousel

### 4. Current Affairs — Auto-Sliding News Carousel
Three stories, each in a distinct format, navigable via round prev/next buttons, dot indicators, or auto-advance:

1. **Condolence notice** (English) — AIMC mourns Maulana Hakim Mohammad Abdullah Mughesi. Includes a "Read Full Story" button opening a detailed modal with the complete report (tributes, AIMPLB message, named speakers, the Urdu slogan blockquote, vote of thanks).
2. **Press release** (Urdu, RTL) — Memorial programme for Dr. Manzoor Alam. Two-image header layout (main event photo + attendees photo placed inline), full right-to-left Urdu body copy, and a formatted two-column grid of attendee names/designations. Opens via "پوری خبر پڑھیں" into a dedicated Urdu modal.
3. **IOS report** (English, with external link) — A second angle on the Dr. Manzoor Alam memorial, opening with a Hadith quote (Sahih Muslim) and two calls to action: "Read Full Report" (in-page modal) and "View on IOS Website" (external link to `iosworld.org`).

**Carousel behaviour:**
- Auto-advances every **6 seconds**
- Pauses correctly on hover (fixed to use `relatedTarget` so it doesn't restart repeatedly while the cursor moves between child elements inside the card)
- Pauses while any "Read Full Story" modal is open; resumes on close
- Manual navigation (prev/next, dots) resets the auto-advance timer

### 5. Aims & Objectives — Bilingual Toggle
A single image swaps between English and Urdu versions via a toggle switch (EN / اردو). The selected language preference is saved to `localStorage` (wrapped in try/catch for environments where storage is blocked).

### 6. Article Modals
Three full-screen modals (`modal1`, `modal2`, `modal3`) corresponding to the three news stories. Each supports:
- Click outside to close
- `Escape` key to close
- A dedicated close (×) button
- Independent scroll within the modal body

### 7. Footer
Three-column layout:
- **Brand** — full logo (`logoFull.jpeg`) and a short organisational description
- **Quick Links** — in-page anchor links
- **Contact** — address, two email addresses, website, phone (`tel:` link), and WhatsApp (`wa.me` link)

Bottom bar includes copyright and social icons (Facebook, X/Twitter, YouTube, Email).

## Design System

All visual styling is driven by CSS custom properties defined in `:root`, making the theme easy to adjust from one place:

```css
:root {
  --bg: #050d1a;              /* page background */
  --surface: rgba(255,255,255,0.045);
  --border: rgba(255,255,255,0.08);
  --accent: #0fbc83;          /* primary green/teal */
  --accent2: #0891b2;         /* secondary blue */
  --gold: #d4a843;            /* construction banner */
  --text: #f0f4f8;
  --muted: rgba(240,244,248,0.62);
  --radius: 20px;
  --max: 1060px;               /* content max-width */
}
```

**Typography:** `Playfair Display` (serif, headings) + `DM Sans` (body), loaded from Google Fonts.
**Icons:** Font Awesome 6.5.0, loaded non-blocking via `preload` + `onload` swap, with a `<noscript>` fallback.

## Performance & Accessibility Notes

- All below-the-fold images use `loading="lazy"`.
- Font Awesome CSS loads asynchronously so it never blocks first paint.
- `IntersectionObserver` powers scroll-reveal animations and unobserves elements once animated (no wasted work after the first reveal).
- `prefers-reduced-motion: reduce` disables all animations/transitions for users who request it.
- All external links use `rel="noopener"`.
- `localStorage` access is wrapped in `try/catch` to avoid breaking in private/incognito modes where storage may be blocked.
- The Urdu sections use `direction: rtl` and increased `line-height` for comfortable Nastaliq-style reading.

## How to Deploy

Because this is a static, single-file site with no build tooling, deployment is just a matter of hosting the file and its `images/` folder.

**GitHub Pages**
1. Push `index.html` and the `images/` folder to a repository.
2. In repo settings, enable GitHub Pages on the `main` branch (root).
3. The site will be live at `https://<username>.github.io/<repo-name>/`.

**Netlify / Vercel**
Drag and drop the project folder (containing `index.html` and `images/`) into the dashboard, or connect the GitHub repo for automatic deploys.

**Any static web host**
Upload `index.html` and `images/` to the web root via FTP/SFTP — no server-side processing required.

## Customisation Guide

| To change... | Edit... |
|---|---|
| Brand colour | `--accent` / `--accent2` in `:root` |
| Hero slides / captions | The `.hero-slide` blocks inside `#heroSlider` |
| Hero auto-advance speed | `setInterval(..., 4000)` in the hero slider script |
| News auto-advance speed | `setInterval(..., 6000)` in the news carousel script |
| News stories | The `.news-slide` blocks inside `.news-carousel-wrap`, plus the matching `modal1` / `modal2` / `modal3` |
| Aims & Objectives images | `data-en` / `data-ur` attributes on `#aimsImg` |
| Footer contact details | The `.footer-col` block inside `<footer>` |
| Construction banner text | `.banner-title` / `.banner-desc` content |

## Browser Support

Built with modern, broadly-supported CSS (`backdrop-filter`, CSS custom properties, `clamp()`, CSS Grid). Works in all current versions of Chrome, Firefox, Safari, and Edge. `backdrop-filter` has reduced support in older Firefox versions but degrades gracefully (the blur effect is simply absent; layout remains intact).

## License

© 2026 All India Milli Council. All Rights Reserved. This codebase was custom-built for AIMC and is not licensed for reuse without permission.
