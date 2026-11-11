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

The look combines two sources. The neutral surfaces, the single bright gold and the type come from
[impeccable.style](https://impeccable.style/). The green is Farmingdale State College's, from
[farmingdale.edu](https://www.farmingdale.edu/).

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

Three families, loaded from Google Fonts:

- **Alumni Sans** (variable, weights 200–500) for headings and the brand name. It is a condensed face set thin and
  large: that contrast with the body text is the signature.
- **Albert Sans** (400–700) for everything else: body, UI, buttons, labels.
- **JetBrains Mono** (500) only for code and literal strings such as an email address.

Fallbacks: `"Albert Sans", Arial, sans-serif` for headings and
`"Avenir Next", "Helvetica Neue", Arial, system-ui, sans-serif` for body.

| Role | Font | Size | Weight | Notes |
| --- | --- | --- | --- | --- |
| H1 | Alumni Sans | `clamp(3.6rem, 7.4vw, 6rem)` | 200 | line-height 1, `--ss-green-dark` |
| H2 | Alumni Sans | 2.6rem | 300 | line-height 1.04, `--ss-green-dark` |
| H3 | Albert Sans | 18px | 600 | line-height 1.35, `--ss-ink` |
| Brand name | Alumni Sans | 20px | 400 | uppercase, letter-spacing .18em |
| Body | Albert Sans | 16px | 400 | line-height 1.65 |
| Lede | Albert Sans | 18px | 400 | max 48ch |
| Label | Albert Sans | 11px | 600 | uppercase, letter-spacing .14em, `--ss-muted` |
| Button | Albert Sans | 14px | 600 | |
| Code / address | JetBrains Mono | 13px | 500 | |
| Footer | Albert Sans | 12px | 600 | uppercase, letter-spacing .14em, white on green |

Do not set Alumni Sans below about 20px or heavier than 500; at small sizes use Albert Sans. Do not put a small
uppercase label directly above a heading.

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
- Breakpoint 820px: stack grids to one column, center text.
- Phone first: no horizontal scroll, 44px minimum tap targets.

## 5. Icons

Every icon comes from the Icons API so all sites share one drawing style. Use the "color" style with the brand colors:

```
https://icons.socialshields.org/api/icons/<name>.svg?style=color&color=%23006456&accent=%23ffba00&ink=%231b1b1b&bg=%23ffffff&theme=light&size=96
```

Display at 30–36px in bars and 64–96px in feature tiles. Do not mix in other icon sets.

Current assignments: shield (brand), lightbulb (Research, Lab), heart (MHDash), castle (SIEGE), chat-bubbles (Network),
graduation-cap (Teaching), book-stack (KB), terminal (Pyram), package (Products), megaphone (News Hub), weather (Weather), documents (News),
paint-palette (Icons).

## 6. Mascot

The sheep is the shared mascot. It is an open-bot-avatar definition (MIT) with body color `--ss-gold` (#ffba00)
and eye color `--ss-fg` (#1b1b1b). Use the definition from `index.html` on socialshields.org. On subsites it is
optional; when used, keep it small (about 100px) near the footer or a contact block, and keep the static SVG fallback.

## 7. Shared elements every subsite has

1. **Home link** at the top-left: the shield icon plus "Social Shields" in Alumni Sans capitals, linking to
   `https://socialshields.org/`. Class `.ss-home` in `brand.css`.
2. **Footer**: a green band with a gold rule on top, reading only `Farmingdale State College` (class `.ss-footer`).
   No personal names in the footer.
3. **Contact** address `contact@socialshields.org` where a contact is needed.
4. `<title>` is `<Project> · Social Shields`.

## 8. Voice

Short sentences. Plain words. Sentence case for headings. The brand name, labels and footers are the only uppercase text.
