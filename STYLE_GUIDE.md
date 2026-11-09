# Social Shields style guide

One look for socialshields.org and every `*.socialshields.org` site. The quickest way to adopt it is to link the shared
stylesheet and use its tokens; the rules below explain the choices so a site can also follow them with its own CSS.

```html
<link rel="stylesheet" href="https://socialshields.org/brand.css">
<body class="ss">
```

`brand.css` sets the tokens on `:root`, loads the fonts, and styles base elements inside `.ss`. It sets no layout.
Any site that already has a design system (a framework theme, Tailwind config, etc.) can instead copy the token
values into its own config.

## 1. Color

| Token | Value | Use |
| --- | --- | --- |
| `--ss-green` | `#2f7a4f` | Primary: buttons, links on hover, brand marks |
| `--ss-green-dark` | `#1f5c3a` | Headings, brand name |
| `--ss-green-soft` | `#4caf8f` | Mascot body, illustrations |
| `--ss-gold` | `#e8c268` | Accent: focus rings, highlights, icon accents |
| `--ss-gold-dark` | `#b7891f` | Small uppercase labels (eyebrows, group titles) |
| `--ss-bg` | `#fdfaf0` | Page background (warm cream) |
| `--ss-hero-bg` | `#eaf4ed` | Hero or header band (pale green) |
| `--ss-bg-soft` | `#eef4ef` | Hover fills, chips, selected states |
| `--ss-card` | `#ffffff` | Cards, floating bars |
| `--ss-fg` | `#2a332e` | Body text |
| `--ss-muted` | `#6f7d76` | Secondary text, footers |
| `--ss-line` | `#e6e1d1` | Borders, dividers |

Rules:
- Light theme only, by choice. Do not add a dark mode; set `color-scheme: light`.
- Green carries, gold accents. Gold is never a large fill; it appears in labels, focus rings and icon details.
- Text on `--ss-green` is white. Text on cream or pale green is `--ss-fg` or `--ss-green-dark`.
- Data visualizations start from the greens and golds above, then add neutrals. Avoid red/blue defaults.

## 2. Typography

Two families, loaded from Google Fonts:

- **Fraunces** (variable, weights 600–700) for headings and the brand name. Set
  `font-variation-settings: "opsz" 144, "SOFT" 60` and `letter-spacing: -0.02em`. Headings are `--ss-green-dark`.
- **Plus Jakarta Sans** (500–800) for everything else: body, UI, buttons, labels.

Fallbacks: `"Iowan Old Style", Georgia, serif` and `"Helvetica Neue", Arial, sans-serif`.

| Role | Font | Size | Weight | Notes |
| --- | --- | --- | --- | --- |
| H1 | Fraunces | `clamp(42px, 6.2vw, 68px)` | 700 | line-height 1.02 |
| H2 | Fraunces | 28px | 700 | line-height 1.15 |
| H3 | Fraunces | 20px | 700 | |
| Body | Plus Jakarta Sans | 16px | 500 | line-height 1.55 |
| Lede | Plus Jakarta Sans | 17px | 500 | color `--ss-muted`, max 48ch |
| Label / eyebrow | Plus Jakarta Sans | 13px | 700 | uppercase, letter-spacing .16em, `--ss-gold-dark` |
| Button | Plus Jakarta Sans | 14px | 700 | |
| Footer | Plus Jakarta Sans | 13px | 700 | uppercase, letter-spacing .12em, `--ss-muted` |

Serif headings over a sans body is the signature; do not swap them or add a third family.

## 3. Shape, depth, motion

- Radii: 14px for buttons and tiles (`--ss-radius`), 22px for cards and bars (`--ss-radius-lg`), 999px for pills.
- One shadow: `0 8px 28px rgba(60, 80, 60, .08)` (`--ss-shadow`), only on white cards over cream.
- Borders are 1px `--ss-line`. No heavy outlines.
- Easing: `cubic-bezier(.2, .8, .2, 1)` (`--ss-ease`), 200–300ms. Hover lifts by 2px. Respect `prefers-reduced-motion`.

## 4. Layout

- Content width 1040px (`--ss-measure`), 16px side gutters, safe-area aware.
- Page background is cream; a hero or header band may use pale green. Sections separate with a 1px `--ss-line` rule.
- Breakpoint 820px: stack grids to one column, center text.
- Phone first: no horizontal scroll, 44px minimum tap targets.

## 5. Icons

Every icon comes from the Icons API so all sites share one drawing style. Use the "color" style with the brand colors:

```
https://icons.socialshields.org/api/icons/<name>.svg?style=color&color=%232f7a4f&accent=%23e8c268&ink=%233b4a41&bg=%23ffffff&theme=light&size=96
```

Display at 30–36px in bars and 64–96px in feature tiles. Do not mix in other icon sets.

Current assignments: shield (brand), lightbulb (Research, Lab), heart (MHDash), castle (SIEGE), chat-bubbles (Network),
graduation-cap (Teaching), book-stack (KB), terminal (Pyram), package (Products), megaphone (News Hub), weather (Weather), documents (News),
paint-palette (Icons).

## 6. Mascot

The sheep is the shared mascot. It is an open-bot-avatar definition (MIT) with body color `--ss-green-soft` (#4caf8f)
and eye color `--ss-fg`. Use the definition from `index.html` on socialshields.org. On subsites it is optional; when used,
keep it small (about 100px) near the footer or a contact block, and keep the static SVG fallback.

## 7. Shared elements every subsite has

1. **Home link** at the top-left: the shield icon plus "Social Shields" in Fraunces, linking to `https://socialshields.org/`.
   Class `.ss-home` in `brand.css`.
2. **Footer** reading only `Farmingdale State College` (class `.ss-footer`). No personal names in the footer.
3. **Contact** address `contact@socialshields.org` where a contact is needed.
4. `<title>` is `<Project> · Social Shields`.

## 8. Voice

Short sentences. Plain words. Sentence case for headings. Labels and footers are the only uppercase text.
