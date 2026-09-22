# Layout

_Part of the ImageWorks Creative design system. Index: [../STYLE-GUIDE.md](../STYLE-GUIDE.md) · Rules: [../CLAUDE.md](../CLAUDE.md) · Code: [../iwc-system.css](../iwc-system.css)_


```css
.wrap {                       /* every band's inner column */
  width: 100%;
  max-width: var(--shell);    /* 1180px */
  margin-inline: auto;
  padding-inline: var(--gutter);
}

.band { padding-block: var(--band-y); background: var(--white); }

.stack {                      /* the default section rhythm */
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 18px;
}
```

A section is always:
`<section class="band …">` → `<div class="wrap stack reveal">` → eyebrow,
sec-title, lead, content.

### Band variants

| Variant | Ground | Use |
| --- | --- | --- |
| `.band` | white | the default |
| `.band--tint` | `#f2f5f9` | alternate with white so the page reads in slabs |
| `.band--tint-b` | `#f1f3f6` | the warmer tint, when two tinted bands sit near each other |
| `.band--snug` | — | `clamp(44px, 4.6vw, 64px)` for a section whose content already carries air |
| `.band--lift` | — | adds only top padding, for a band that follows the hero |
| `.band--cta` | `--cta-band` + dot field | **the closing call.** `clamp(72px, 8vw, 112px)` tall, headings and quiet buttons go white, the eyebrow goes `--green` |
| `.band--deep` | 6-stop navy gradient + dot field | the credibility / pricing band |

The two dark bands lay a dot field over the gradient — a 1px white radial at
`.07`, on a 24px grid (`--cta`) or 26px (`--deep`) — and put their children on
`position: relative` above it.

`.band--deep` **re-points the semantic tokens instead of writing a dark
variant**, which is why nothing inside it needs one:

```css
.band--deep {
  --heading: #ffffff;
  --text: rgba(226, 238, 252, .82);
  --muted: rgba(226, 238, 252, .70);
  --border: rgba(255, 255, 255, .16);
  --navy: #ffffff;
}
```


