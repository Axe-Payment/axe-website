# axe. — Marketing Site (v2)

Marketing site for **axe.** — the API for regulated money movement. Built to the v1.0 brand guidelines.

This is **version 2**, a complete rebrand from the original `axe-website/` folder. v2 swaps to:

- The `axe.` wordmark (period in Voltage Lime).
- Ink / Plasma / Voltage / Slate / Fog colour system (60 / 30 / 7 / 3 split).
- Space Grotesk display sans (PP Neue Machina fallback), Inter body (ABC Diatype fallback), JetBrains Mono code.
- Compliance signals above the fold per brand spec.

## Stack

Pure static. No build step.

- **HTML5** — single `index.html`.
- **CSS** — embedded, organised by component, themed via custom properties.
- **Vanilla JS** — word rotator (crypto / money / banking), scroll-reveals, count-up stats, live-transaction simulator, scroll-progress bar, infra tabs.
- **Fonts** — Google Fonts (Space Grotesk · Inter · JetBrains Mono).
- **Hosting** — Vercel.

## Repo layout

```
axe-website-v2/
├── index.html        # the entire site
├── vercel.json       # security headers + clean URLs
├── robots.txt        # allow indexing
├── .gitignore
├── DEPLOY.md         # ↪ same as v1 (CLI / Git / drag-drop)
├── GITHUB.md         # GitHub + Vercel hand-off
└── README.md         # this file
```

## Local preview

```bash
python3 -m http.server 5173
# then open http://localhost:5173
```

## Brand tokens

```css
:root {
  --ink:      #0B0F1A;   /* primary surface, ~60% */
  --plasma:   #FAFAF7;   /* text on dark */
  --voltage:  #C8FF00;   /* live · CTA · status (rationed: ≤3 per surface) */
  --slate:    #1A1F2E;   /* code panels, raised cards */
  --fog:      #9CA3AF;   /* secondary text, dividers */

  --display:  'Space Grotesk', system-ui, sans-serif;
  --body:     'Inter', system-ui, sans-serif;
  --mono:     'JetBrains Mono', ui-monospace, monospace;
}
```

**Voltage budget per surface:** the period in `axe.`, one CTA, one live-status dot. The brand guide caps Voltage at three appearances per layout.

## Voice

- Plainspoken, technical, specific. Numbers always carry units. No "revolutionize", no "lightning fast".
- See `axe-payments-brand-guidelines.md` (in the design folder) for the full voice spec.

## Deploy

Same as v1. See `DEPLOY.md` and `GITHUB.md`.

## Difference from v1

| Aspect | v1 | v2 |
|---|---|---|
| Brand mark | `A · axe payments` | `axe.` (lime period) |
| Accent colour | Red `#E2371A` | Voltage Lime `#C8FF00` |
| Surface | Light dominant | **Ink dominant** (60% dark) |
| Display font | Instrument Serif | **Space Grotesk** (heavy display sans) |
| Body font | Inter / Satoshi | Inter (ABC Diatype fallback) |
| Hero headline | Static | **Cycling word**: crypto / money / banking |
| Compliance row | Footer badges | **Above-the-fold strip** + scrolling logo marquee |
| Comparison table | 8-row dark table | **Removed** |
| Offices section | 3-card grid | **Removed** |
| CTA | "Bring your Head of Digital…" | **"Sound interesting? Connect with us."** |

---

© 2026 Axe Payments Limited.
