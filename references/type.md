# Type

_Part of the ImageWorks Creative design system. Index: [../STYLE-GUIDE.md](../STYLE-GUIDE.md) · Rules: [../CLAUDE.md](../CLAUDE.md) · Code: [../iwc-system.css](../iwc-system.css)_


```css
body {
  font-family: 'Plus Jakarta Sans', system-ui, -apple-system, 'Segoe UI',
               Roboto, Helvetica, Arial, sans-serif;
  font-size: var(--step-0);
  font-weight: 400;
  line-height: 1.65;
  color: var(--ink);
}

h1, h2, h3, h4 {
  margin: 0;
  color: var(--navy);
  font-weight: 800;
  line-height: 1.15;
  letter-spacing: -.018em;
  text-wrap: balance;
}

p { margin: 0; text-wrap: pretty; }
```

- **Loaded as base64** in a `@font-face` at the top of the stylesheet, weight
  range `300 800`, `font-display: swap`. Never a Google Fonts `<link>` — that
  is a network request and a flash.
- **Headings are 800.** Body 400, emphasis 700, quiet button labels 600.
- **Negative tracking** on headings: `-.018em` normally, `-.035em` on the hero
  `h1`, which also runs a tighter `line-height: 1.08`.
- **`text-wrap: balance`** on headings, **`pretty`** on paragraphs.
- **Measure**: `--measure: 66ch` on any run of prose. A heading caps at `21ch`
  (`.sec-title`) or `27ch` (`.sec-title--wide`); the hero `h1` at `16ch`,
  because a ragged left column reads faster than a wide centred block.

### The sizes

Every step is a `clamp()`, so a size is a range rather than a number: the floor
is what a 320px phone gets, the cap what the 1180px design width gets. The
right-hand columns are the ranges in the **Global UX + Design Rules**, which
these are held inside.

| Step | Used by | 320px | 1180px | Rules, desktop | Rules, mobile |
| --- | --- | --- | --- | --- | --- |
| `--step-4` | H1, where a hero sets none | 30px | 56px | 42–56 | 30–36 |
| *(hero)* | `.hero h1` — sets its own | 28.8px ⚠ | 57.6px | 42–56 | 30–36 |
| `--step-3` | H2 · `.sec-title` | 28px | 44px ⚠ | 32–42 | 26–32 |
| `--step-2` | H3 | 22px | 28px | 22–28 | — |
| `--step-1` | `.lead` · `.note` · `.signals` | 16.5px | 18px | 17–18 | 16–17 |
| `--step-0` | body · `.quote-rail` | 16px | 17px | 17–18, never <16 | 16–17 |
| `--step--1` | `.skip-to-content` | 12.5px | 13.5px | chrome, not body copy | — |

Line heights: body `1.65`, headings `1.15`, the hero `h1` `1.08`. The rules ask
for roughly `1.6` on body and `1.1–1.25` on headlines, so all three sit inside
them.

**The two ⚠ are deliberate**, and both are commented where they are set:

- **The hero `h1` floor.** `min(9vw, 36px)` gives 28.8px at 320px, against a
  mobile minimum of 30px. The largest size that still holds that headline to
  three lines at 320px measured 29.5px — the two cannot both be had, and a
  headline broken across five lines is the worse failure. From 334px up the
  ramp is inside the range.
- **The 44px H2 cap**, against a 42px maximum. The `--one` variants hold their
  run on a single line at measurements taken at 44px, and the home's own h2 is
  44px. Every width from 538px to the design width is inside the range; only
  the cap is over, by 2px.

Everything else in the scale lands inside the ranges as written.

### Type components

| Class | What it is |
| --- | --- |
| `.eyebrow` | 12px / 800 / `.16em` uppercase in `--green-ink`, with an 8px green dot before it. On `.band--cta` it flips to `--green`. |
| `.sec-title` | Section `h2`. `--step-3`, `max-width: 21ch`. `em` inside it is not italic — it is the green accent phrase. `--wide` takes it to 27ch. |
| `.lead` | `--step-1`, `line-height: 1.7`, `--muted`, capped at `--measure`. `strong` goes navy/700. |
| `.note` | `--step-1` / 700 / navy — a one-line claim that should not read as body copy. |
| `.hero-sub` | The hero's paragraph. Same idea, hero sizing. |
| `--one` / `--two` | `.sec-title--one`, `.lead--one`, `.note--one` drop the cap and take `white-space: nowrap` **above 1024px only**, for runs measured to fit. `.lead--two` widens to 1000px and balances into two lines above 1024px. Only use them on copy you have actually measured. |


