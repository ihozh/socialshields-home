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

The look combines three sources. The neutral surfaces and the single bright gold follow
[impeccable.style](https://impeccable.style/). The green is Farmingdale State College's, from
[farmingdale.edu](https://www.farmingdale.edu/). The type roles follow [meedan.org](https://meedan.org/): a heavy
grotesque for display, a sturdy serif for navigation, a plain sans for text. Meedan's own display and navigation
faces are commercial, so the same roles are filled with open fonts.

## 1. Color

| Token | Value | Use |
| --- | --- | --- |
| `--ss-green-dark` | `#006456` | Headings, brand name, buttons, footer band |
| `--ss-green` | `#006f71` | Hover on green, focus rings |
| `--ss-gold` | `#ffba00` | Mascot body, footer rule, text selection, icon accents |
| `--ss-gold-dark` | `#856514` | Gold as text, in the rare case a gold word is needed |
| `--ss-bg` | `#f8f8f8` | Page background |
| `--ss-hero-bg` | `#eeeeee` | Hero or header band |
| `--ss-bg-soft` | `#e4e4e4` | Hover fills, selected states |
| `--ss-card` | `#fdfdfd` | Floating bars, chips |
| `--ss-ink` | `#070707` | Strongest text: chip text, hovered links |
| `--ss-fg` | `#1b1b1b` | Body text |
| `--ss-muted` | `#585858` | Secondary text, labels |
| `--ss-line` | `rgba(7, 7, 7, .1)` | Borders, dividers |

`--ss-green-soft` is the old name for the mascot color. It now points to `--ss-gold` and stays only so existing
sites do not break; use `--ss-gold` in new code.

Rules:
- Light theme only, by choice. Do not add a dark mode; set `color-scheme: light`.
- Surfaces are neutral gray, with no warm or green tint. Green carries the words that matter; gold is the one
  bright spot.
- Gold is never a text color on light surfaces (it fails contrast) and never a large fill apart from the mascot.
- Text on green is white. Text meets WCAG AA (4.5:1) on every surface; do not lighten `--ss-muted`.
- Data visualizations start from the green and gold above, then add neutrals. Avoid red/blue defaults.

## 2. Typography

Four families, loaded from Google Fonts:

- **Bricolage Grotesque** (weights 700–800) for headings and the brand name. Heavy and tight; it is the loudest
  thing on the page after the mascot.
- **IBM Plex Serif** (500–600) for navigation and short emphasized lines: section names, H3.
- **IBM Plex Sans** (400–600) for everything else: body, UI, buttons, labels.
- **IBM Plex Mono** (500) only for code and literal strings such as an email address.

Tokens: `--ss-head`, `--ss-nav`, `--ss-body`, `--ss-mono`.

| Role | Font | Size | Weight | Notes |
| --- | --- | --- | --- | --- |
| H1 | Bricolage Grotesque | `clamp(2.9rem, 6.4vw, 4.75rem)` | 800 | line-height 1, letter-spacing -0.02em, `--ss-green-dark` |
| H2 | Bricolage Grotesque | 2rem | 800 | line-height 1.1, `--ss-green-dark` |
| H3 | IBM Plex Serif | 19px | 600 | line-height 1.35, `--ss-ink` |
| Brand name | Bricolage Grotesque | 24px | 800 | letter-spacing -0.02em, mixed case |
| Navigation | IBM Plex Serif | 19px | 600 | section names in a bar |
| Body | IBM Plex Sans | 16px | 400 | line-height 1.6 |
| Lede | IBM Plex Sans | 18px | 400 | max 48ch |
| Label | IBM Plex Sans | 11px | 600 | uppercase, letter-spacing .14em, `--ss-muted` |
| Button | IBM Plex Sans | 14px | 600 | |
| Code / address | IBM Plex Mono | 13px | 500 | |
| Footer | IBM Plex Sans | 12px | 600 | uppercase, letter-spacing .14em, white on green |

Keep Bricolage Grotesque for headings and the brand name only; it is too heavy for running text. Do not put a
small uppercase label directly above a heading.

## 3. Shape, depth, motion

- Radii: 14px for buttons and tiles (`--ss-radius`), 22px for cards and bars (`--ss-radius-lg`), 999px for pills.
- One shadow, soft and neutral (`--ss-shadow`), only on floating bars and cards.
- Borders are 1px `--ss-line`. No heavy outlines.
- Focus ring: 2px `--ss-green`, offset 2px.
- Easing: `cubic-bezier(.2, .8, .2, 1)` (`--ss-ease`), 200–300ms. Hover lifts by 2px. Respect `prefers-reduced-motion`.

## 4. Layout

- Content width 1040px (`--ss-measure`), 16px side gutters, safe-area aware.
- Page background is `--ss-bg`; a hero or header band may use `--ss-hero-bg`. Sections separate with a 1px
  `--ss-line` rule.
- Section cards (homepage): Research, Education and Products are three cards in a row. A card is barely
  there: `--ss-card` on the page gray, a 1px `--ss-line` border, the 22px radius, 32px padding. Inside: the section
  name as a green heading, then one line per project (16px, ink), each closed by a 1px rule and ending in a small
  green arrow; the whole line is the link. No color fills, no icons, no carousel or timed rotation, and project
  names are not shown as headings.
- Breakpoint 820px: stack grids to one column, center text.
- Phone first: no horizontal scroll, 44px minimum tap targets.
- No rubber-band overscroll: the page stops at its top and bottom edges (`overscroll-behavior: none`, set by
  `brand.css` on any page that uses `.ss`).

## 5. Icons

Every icon comes from the Icons API so all sites share one drawing style. Use the "stroke" style: green lines with
gold details, which sits well next to the thin headings.

```
https://icons.socialshields.org/api/icons/<name>.svg?style=stroke&weight=1.4&color=%23006456&accent=%23ffba00&bg=%23fdfdfd&theme=light&size=96
```

Set `bg` to the surface the icon sits on (`%23fdfdfd` for bars and cards, `%23f8f8f8` for the page); the stroke
style paints hidden faces with it. Do not use the filled styles: they turn into dark blobs at bar size.

Display at 30–36px in bars and 64–96px in feature tiles. Do not mix in other icon sets.

Current assignments: shield (brand), microscope (Research), lightbulb (Lab), heart (MHDash), castle (SIEGE), chat-bubbles (Network),
graduation-cap (Education), book-stack (KB), terminal (Pyram), package (Products), megaphone (News Hub), weather (Weather), documents (News),
paint-palette (Icons).

## 6. Mascot

The sheep is the shared mascot. It is an open-bot-avatar definition (MIT) with body color `--ss-gold` (#ffba00)
and eye color `--ss-fg` (#1b1b1b). Use the definition from `index.html` on socialshields.org. On subsites it is
optional; when used, keep it small (about 100px) near the footer or a contact block, and keep the static SVG fallback.

On the homepage the sheep has a speech bubble with no heading: one sentence that opens with a greeting for the
time of day and points to one thing to read: a Knowledge Base entry, or one of the three sections of the page. The entry changes every 8 seconds, pausing while the pointer or keyboard focus is on the bubble; a click on the sheep
moves on at once. With `prefers-reduced-motion` there is no timer. The lines are a short
list in `index.html`; add to it when the Knowledge Base or the project list grows.

## 7. Shared elements every subsite has

1. **Home link** at the top-left: the shield icon plus "Social Shields" in Bricolage Grotesque, linking to
   `https://socialshields.org/`. Class `.ss-home` in `brand.css`.
2. **Footer**: a green band with a gold rule on top, reading only `Farmingdale State College` (class `.ss-footer`).
   On the homepage the Contact block sits inside the same green, so the gold rule moves up to the top of Contact.
   No personal names in the footer.
3. **Contact** address `contact@socialshields.org` where a contact is needed.
4. `<title>` is `<Project> · Social Shields`.

## 8. Voice

Short sentences. Plain words. Sentence case for headings. Labels and footers are the only uppercase text.
