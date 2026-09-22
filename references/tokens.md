# Tokens

_Part of the ImageWorks Creative design system. Index: [../STYLE-GUIDE.md](../STYLE-GUIDE.md) · Rules: [../CLAUDE.md](../CLAUDE.md) · Code: [../iwc-system.css](../iwc-system.css)_


Declared once on `:root`, verbatim across every page. Copy this block; do not
retype values.

```css
:root {
  color-scheme: light;

  /* ---- brand ---- */
  --navy: #143c66;
  --navy-deep: #0a2c4d;
  --blue: #1266b5;
  --blue-bright: #1e6bb0;
  --green: #80c34a;
  --green-ink: #5c9a2e;          /* the green for text and links */
  --ink: #1f2b3e;                /* body copy */
  --muted: #5a6b82;
  --faint: #7d8ea1;
  --nav-ink: #3d464d;

  /* ---- surfaces ---- */
  --white: #ffffff;
  --band-tint: #f2f5f9;
  --band-tint-warm: #f1f3f6;
  --card-top: #ffffff;
  --card-bottom: #fcfdff;
  --border: #e3eaf3;
  --border-soft: #eef2f7;
  --chip-blue: #c1daff;
  --chip-green: #eaf6dd;
  --chip-navy: rgba(24, 73, 125, .14);
  --tint-green: #eef6e6;
  --tint-blue: #e5edf7;
  --danger-soft: #fbe9e9;
  --danger-ink: #b23b3b;
  --grey-soft: #e8edf4;          /* 5.3:1 with --grey-ink, so a 10px */
  --grey-ink: #4f5f77;           /* uppercase tag still clears AA */

  /* ---- the closing band ---- */
  --cta-band: linear-gradient(135deg, #1266b5, #0a2c4d);

  /* ---- shape ---- */
  --r: 2px;

  /* ---- depth ---- */
  --shadow-card: 0 1px 3px rgba(20, 40, 80, .08), 0 14px 34px rgba(20, 40, 80, .1);
  --shadow-flat: 0 1px 3px rgba(20, 40, 80, .07);
  --shadow-lift: 0 4px 12px rgba(20, 40, 80, .18);
  --ring: 0 0 0 3px rgba(128, 195, 74, .5), 0 0 0 1px rgba(20, 60, 102, .55);

  /* ---- rhythm ---- */
  --shell: 1180px;
  --gutter: clamp(22px, 4vw, 40px);
  --band-y: clamp(64px, 8vw, 108px);
  --nav-h: 88px;
  --measure: 66ch;

  /* ---- type scale — §4 says what each step is and the range it holds ---- */
  --step--1: clamp(12.5px, .18vw + 12px, 13.5px);   /* chrome, not body copy */
  --step-0:  clamp(16px, .25vw + 15.2px, 17px);     /* body */
  --step-1:  clamp(16.5px, .4vw + 15.5px, 18px);    /* lead, note, signals */
  --step-2:  clamp(22px, 1.1vw + 18px, 28px);       /* H3 */
  --step-3:  clamp(28px, 2.6vw + 18px, 44px);       /* H2 / .sec-title */
  --step-4:  clamp(30px, 3vw + 20px, 56px);         /* H1, where the hero sets none */

  /* ---- motion ---- */
  --ease: cubic-bezier(.16, .84, .44, 1);
}
```

### How the colours are used

- **Navy** carries every heading. Headings are `--navy`, never `--ink`.
- **Green** is the action colour: the solid button, the eyebrow dot, the check
  chip, the accent phrase in a headline. `--green` on a surface, `--green-ink`
  (`#5c9a2e`) whenever it carries text or a link — `#80c34a` on white does not
  clear AA.
- **Blue** is the secondary/interactive colour: arrow links, hovered rows,
  focus on a form field, the CTA gradient's light end.
- **`--muted`** is body copy in a lead; **`--faint`** is metadata and quiet rails.
- **Red exists only as feedback** — `--danger-soft` / `--danger-ink` for a
  counterpoint chip or an invalid field. It is never decoration.

### The focus ring

`--ring` is green over a navy hairline, applied on `:focus-visible` with the
2px corner:

```css
:where(a, button, summary, details):focus-visible {
  outline: none;
  box-shadow: var(--ring);
  border-radius: var(--r);
}
```


