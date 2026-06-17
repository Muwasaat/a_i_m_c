# All India Milli Council — Website

Single-file landing page for AIMC (placeholder while the full site is built). No build step required — open `index.html` directly or deploy as static files.

## File Structure

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

All image paths are relative — the `images/` folder must sit next to `index.html`.

## Features

- **Hero carousel** — 7 auto-sliding images (4s interval), handles mixed portrait/landscape via a blurred backdrop fill so nothing gets cropped.
- **Current Affairs carousel** — 3 stories (English condolence notice, Urdu press release, English IOS report with external link), auto-slides every 6s, pauses on hover/modal-open, round prev/next buttons + dots.
- **Aims & Objectives** — EN/Urdu image toggle, saved via `localStorage`.
- **Article modals** — full story text for each news item, closes via ×, backdrop click, or `Escape`.
- **Footer** — address, two emails, phone, WhatsApp, website, social links.

## Design Tokens

Theme colors/spacing are controlled via CSS variables in `:root` (`--accent`, `--accent2`, `--bg`, `--gold`, etc.) — change once, applies everywhere.

## Deploy

Upload `index.html` + `images/` to any static host (GitHub Pages, Netlify, Vercel, or plain FTP). No server-side processing needed.

## Quick Customisation

| Change | Where |
|---|---|
| Brand colour | `--accent` / `--accent2` in `:root` |
| Hero slides | `.hero-slide` blocks in `#heroSlider` |
| Slide timing | `setInterval(..., 4000)` (hero) / `6000` (news) |
| News stories | `.news-slide` blocks + matching `modal1`/`modal2`/`modal3` |
| Footer contact | `.footer-col` inside `<footer>` |

## License

© 2026 All India Milli Council. All Rights Reserved.

