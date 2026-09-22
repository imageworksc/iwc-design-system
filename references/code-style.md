# Code style

_Part of the ImageWorks Creative design system. Index: [../STYLE-GUIDE.md](../STYLE-GUIDE.md) · Rules: [../CLAUDE.md](../CLAUDE.md) · Code: [../iwc-system.css](../iwc-system.css)_

Not opinions — these are the conventions already in force across the whole
system. Match them and a new page's CSS is indistinguishable from the rest.

## CSS

**No leading zeros — anywhere.** `.16em`, `.25vw`, `rgba(20, 40, 80, .08)`.
Never `0.16em`. The system holds 80 fractional values and not one of them
carries a leading zero.

The rule is not only about CSS. Anything we number is written the same way:
decision records are `1-`, `9-`, `10-`, never `0001-`. The zero-padded form
buys lexical sorting in a directory listing and costs readability in every
heading, link and reference that mentions the thing; we take the readability.

```css
letter-spacing: .16em;          /* yes */
letter-spacing: 0.16em;         /* no  */
transition: opacity .7s var(--ease);
box-shadow: 0 1px 3px rgba(20, 40, 80, .08);
```

**No unit on zero.** `padding: 0`, `top: 0`, `border: 0`. Never `0px`.

**Hex lowercase, shortened where it shortens.** `#fff`, `#143c66`. Never
`#FFF`, never `#ffffff` in a rule — though the token declaration itself keeps
the long form (`--white: #ffffff`) so the block reads as a column.

**Single quotes** on font names: `font-family: 'Plus Jakarta Sans', system-ui, …`.

**Logical properties** where there is one: `padding-block`, `padding-inline`,
`margin-inline`, `inline-size`, `block-size`, `border-top` stays `border-top`.

**Tokens over values.** If you are typing a hex or a bare pixel size into a
page block, check first whether a token already says it. Every size a page
block uses is declared once at the head of that block, prefixed.

**One space after the colon, one declaration per line** — except a short rule
that fits on one, which is written on one:

```css
.btn-row { display: flex; flex-wrap: wrap; gap: 14px; }
.chip--blue { background: var(--chip-blue); color: var(--navy); }
```

**Section banners** divide the stylesheet:

```css
/* --------------------------------------------------------------------------
   BUTTONS AND LINKS
   -------------------------------------------------------------------------- */
```

and the file itself opens with a `==========` banner naming the page.

**No `!important`** outside the reduced-motion blanket.

## Comments

Comments explain **why**, not what. The rejected alternative, the measurement
behind a number, the bug the rule fixes. This is the single most valuable habit
in the codebase — it is why these pages are still editable a year later.

```css
/* Was a jump straight to navy, which read louder than the green button next
   to it. #c3d6ea is the ring the reached process step already uses. */
.btn--quiet:hover { border-color: #c3d6ea; }
```

```css
/* clip, not hidden: hidden would make body a scroll container and break
   the sticky nav */
overflow-x: clip;
```

A comment that only restates the property is noise — delete it. A comment
carrying a measurement (`the heading is 791px at 44px, against 944px of room`)
is the most valuable kind, because it is the thing nobody can recover later.

When a decision is bigger than the rule it sits on — it shapes several rules,
or someone will want to overturn it — write it up in [`decisions/`](../decisions/)
and point the comment there.

## HTML

- Attribute order: `class`, then `id`, then `aria-*`, then the rest.
- Double quotes on attributes.
- Section comments number the sections as they appear:

```html
<!-- 1 · HERO ---------------------------------------------------------- -->
```

- Decoration carries `aria-hidden="true"`; nothing decorative gets an id.
- No `style=`. Ever.

## JavaScript

- `'use strict'` at the top, loaded with `defer`.
- `const` / `let`, arrow functions, `for…of`, spread, `??`. No `var`.
- Functions named `setupThing()`, called at the foot of the file.
- Same comment discipline as the CSS — the file header says what the script is
  for and, just as usefully, what it no longer does:

```js
/* The file it came from carried six more routines — the sticky header, the
   dropdown menu, the process rail, the FAQ accordion, the counting stats and
   the anchor scrolling. None of them has anything left to act on. */
```

## Prose, in the docs and the READMEs

- Sentence case in headings, not Title Case.
- An em dash with spaces around it — like this — not an en dash.
- British-leaning spelling is already in the files (`colour`, `centred`,
  `honoured`). Keep it consistent within a file rather than converting.
- Numbers that were measured are written with their measurement, not rounded
  away: `29.5px at 320`, not `about 30px`.
