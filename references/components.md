# Components

_Part of the ImageWorks Creative design system. Index: [../STYLE-GUIDE.md](../STYLE-GUIDE.md) · Rules: [../CLAUDE.md](../CLAUDE.md) · Code: [../iwc-system.css](../iwc-system.css)_


### Buttons

```css
.btn {                       /* 54px tall, 26px inset, 16px/700, 2px corner */
  display: inline-flex; align-items: center; justify-content: center;
  gap: 11px;
  height: 54px; padding-inline: 26px;
  border-radius: var(--r); border: 1.5px solid transparent;
  font-size: 16px; font-weight: 700; line-height: 1;
  white-space: nowrap;
}
.btn:hover  { transform: translateY(-3px); box-shadow: var(--shadow-lift); }
.btn:active { transform: translateY(-1px); }
```

- `.btn--solid` — green fill, white label, `brightness(1.04)` on hover. **One
  per view.**
- `.btn--quiet` — transparent, `--border` hairline, navy label at 600. Hover
  moves the border to `#c3d6ea`, not to navy: a jump to navy read louder than
  the green button beside it.
- Inside `.band--cta` both grow to **58px / 17px**, and the quiet one takes a
  white border at `.34`.
- `.btn-row` is `display: flex; flex-wrap: wrap; gap: 14px`. Below 640px the
  buttons go full width.
- A button carries its icon as `<svg class="icon" width="15" height="15">` with
  a `<use href="#i-arrow">`.

### Links

| Class | Behaviour |
| --- | --- |
| `.iw-link` | the home's underline: a 1.5px rule in `currentColor` growing `scaleX(0 → 1)` from the left over `.3s` |
| `.arrow-link` | 15px/700 blue, arrow slides `translateX(5px)` on hover. `--green` variant for green-ink. |
| `.skip-link` | 13.5px/700 `--faint` with a bottom hairline, going navy on hover — a quiet jump to a section |
| `.quote-rail` | a ruled full-width row for a call that repeats through the copy, so the repetition reads as rhythm rather than clutter |

### Chips and icons

`.chip` is the home's 22px tinted circle — green by default, with `--blue`,
`--navy` and `--danger` variants — holding a 12px icon. It is the only place a
circle appears in a 2px-corner system, and it always holds an icon, never text.

Icons are an **SVG symbol sheet** at the top of `<body>`:

```html
<svg width="0" height="0" aria-hidden="true" focusable="false" class="icon-defs">
  <defs>
    <symbol id="i-check" viewBox="0 0 16 16">…</symbol>
    <symbol id="i-arrow" viewBox="0 0 24 24">…</symbol>
  </defs>
</svg>
```

Strokes are `currentColor`, `stroke-width: 1.8`, round caps and joins. Used as
`<svg class="icon" aria-hidden="true"><use href="#i-check"/></svg>`.

### The hero

Three parts, in this order:

1. **The ground** — `.hero-wash` with three `<span>` washes and a sheen.
2. **The column** — `.wrap.hero-inner > .hero-main`, ranged left, `gap: 24px`.
3. **The entrance** — a staged animation, CSS only.

```html
<section class="hero" aria-labelledby="hero-title">
  <div class="hero-wash" aria-hidden="true">
    <span class="hero-wash__g"></span>
    <span class="hero-wash__b"></span>
    <span class="hero-wash__s"></span>
  </div>
  <div class="wrap hero-inner">
    <div class="hero-main">
      <h1 id="hero-title">…<span class="accent">…</span></h1>
      <p class="hero-sub">…<strong>…</strong></p>
      <div class="btn-row">…</div>
    </div>
  </div>
</section>
```

The hero is `min-height: min(76vh, 620px)` and ends on a gradient running
white → white 56% → `--band-tint`, so it hands off to a tinted band with no
seam and no rule.

**The washes.** Green opens top-left, brand blue top-right, sky low and
widest — each a `closest-side` radial at `.21–.24` alpha, each on its own
element with its own keyframes and its own period (71s / 97s / 127s, sharing
no useful factor) so they drift apart and back together instead of sliding as
one sheet. They move on **Y only**: X held at zero keeps each wash in its own
place. Four waypoints, `linear` — two on an ease decelerates, stops and
reverses, which reads as an animation looping.

The layer is `block-size: 100%` with a **percentage** mask
(`linear-gradient(180deg, #000 0, #000 52%, transparent 88%)`), not a fixed
pixel box. A fixed box against a hero of a different height gets cut off square
at the bottom, and that cut is the line that shows between the hero and the
section under it. The sheen (`heroSheen`, 47s) rides **inside** the wash layer
so it fades under the same mask.

**The entrance** is declared outright under
`@media (prefers-reduced-motion: no-preference)`, not gated on a script flag:
`hero-in .8s var(--ease) backwards`, delays `.06 / .26 / .40 / .54`, with the
green accent phrase landing at `.34` and only above 640px, where it can take
`display: inline-block` without being pushed off the measure. `backwards` drops
the fill afterwards so hover states still win.

### Cards and rows

There is no `.card` class — there is a **recipe**, applied wherever a surface
is needed:

```css
border-radius: var(--r);
background: linear-gradient(180deg, var(--card-top), var(--card-bottom));
box-shadow: var(--shadow-card);
```

A list of rows (`.cms-list` / `.cms-row`) is one card with `overflow: hidden`,
rows divided by `--border-soft`, hovering to `--tint-blue`, and a rule that
**wipes in from the left** — the same mechanic the links use, rather than a
decorative bar that is always there.

A ruled list without the card (`.signals`) is rows at `padding-block: 16px`
between `--border` hairlines, each with a chip. Hover is a whisper —
`rgba(128, 195, 74, .07)` — not a move: five rows shifting under the cursor is
busier than the content deserves.

### Disclosure (FAQ and service rows)

Native `<details>`. No accordion script: the browser toggles it, announces the
state, and keeps closed copy out of the accessibility tree without being asked.

- Ruled like `.signals`, `summary` at 17–18px/700 navy, hover to `--blue`.
- `summary::-webkit-details-marker { display: none; }`, replaced by `.faq-sign`
  — a plus built from two `::before`/`::after` bars that rotates 90° and goes
  green when open.
- Opening: `::details-content` interpolated `0 → auto` under
  `interpolate-size: allow-keywords`, with the copy sliding in over it.
  Browsers without it get a clean snap and keep the slide.
- FAQ rows are exclusive by name; service rows are **not** — two can be open at
  once, which is what you want when comparing them.

### Forms

From `contact-form-iwc`. Fields are 2px-cornered, 52px tall, on a
barely-off-white ground:

```css
.iwc-input, .iwc-textarea {
  width: 100%;
  font-family: inherit; font-size: 16px; color: #1f2b3e;
  background: #fbfcfe;
  border: 1px solid #dbe4ef; border-radius: 2px;
}
.iwc-input    { height: 52px; padding: 0 14px; }
.iwc-textarea { padding: 14px; min-height: 150px; resize: vertical; }
.iwc-input:focus, .iwc-textarea:focus {
  outline: 0; background: #fff;
  border-color: #1266b5;
  box-shadow: 0 0 0 3px rgba(18, 102, 181, .14);
  transform: translateY(-1px);
}
```

- **`:user-invalid`, never `:invalid`** — a required field must not turn red
  before it has been touched.
- `.iwc-field:focus-within > label` picks up the focus blue, so the eye has
  somewhere to land.
- Required is marked with a green `*` (`.iwc-req`); optional with a quiet
  uppercase tag (`.iwc-opt`).
- 16px minimum on inputs — anything smaller makes iOS zoom the page.
- The captcha keeps its own dashed well, so the block that lands there is
  visibly part of the form and not floating loose.

### Navigation

The nav is its own repo (`menu-iwc`) and its own vocabulary, on the same
tokens: `.utility` (the strip that scrolls away) over `.nav` (88px, `--nav-h`,
sticky) with `.menu` / `.dropdown` panels, `.hamburger`, and a drawer below
1000px.

Its own tokens: `--logo-h: 40px`, `--drawer-w: min(380px, 88vw)`,
`--border-hover: #c3d6ea`, `--scrim: rgba(10, 44, 77, .42)`, `--shadow-nav`,
`--shadow-nav-stuck`, `--shadow-drawer`.

Accessibility is the point of that repo: `aria-expanded` on every trigger,
arrow keys along the bar and down a panel, `Home`/`End`, `Escape` to close and
return focus, a focus trap while the drawer is open, and `body.is-locked` so
the page behind it cannot scroll.


