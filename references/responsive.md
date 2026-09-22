# Responsive

_Part of the ImageWorks Creative design system. Index: [../STYLE-GUIDE.md](../STYLE-GUIDE.md) · Rules: [../CLAUDE.md](../CLAUDE.md) · Code: [../iwc-system.css](../iwc-system.css)_


Built and measured **320px → 5120px**, with no horizontal overflow at any width
in that range, with every disclosure open.

### Down

| Breakpoint | What happens |
| --- | --- |
| `≤900px` | two-column grids become one; a sticky aside goes static |
| `≤767px` | carousel cards go to `84vw`, the marquee speeds up |
| `≤700px` | dense rows tighten, round marks come down, an open detail gives up its indent |
| `≤640px` | stat grids stack; a `.btn-row` goes full width; a tab pair stops being a pair |
| `≤560px` | headlines that were held on one line are allowed to wrap |

`.hero h1` is `clamp(min(9vw, 36px), 4.2vw + 8px, 64px)`. The floor scales
below 400px instead of sitting flat at 36px — pinned there, a three-word
headline broke to four and five lines on a 320–360px phone. `min()` leaves
every width from 400px up exactly as it was.

### Up

**Nothing below 1800px is touched** — on a 1440 or 1920 display the shell caps
are the intended measure. Past that they stop being a measure and start being a
stripe: on a 4K panel reporting 3840 CSS pixels, an 1180px shell covers under a
third of the screen at a body size physically half what the same value gives on
a 1080p monitor.

| | `--shell` | `--gutter` | `--band-y` | `--step-0` | `h1` | `.btn` |
| --- | --- | --- | --- | --- | --- | --- |
| base | 1180 | 22–40 | 64–108 | 15.5–17 | 36–64 | 54px |
| `≥1800px` | 1320 | 48 | 120 | 18 | 54 | 60px |
| `≥2400px` | 1560 | 64 | 148 | 20 | 62 | 68px |
| `≥3200px` | 1840 | 80 | 180 | 23 | 72 | 78px |

The shell stops at 1840px **on purpose**. Past that, more width would only
lengthen the line: the shell and the type grow together, so an open detail
measures 75 characters at the design width and still only 85 at 4K. A 5120px
viewport gets generous margins rather than a wider column.

**This is what page tokens are for.** Declare every size the page block uses
once, prefixed, at the head of that block — no bare pixel size anywhere else:

```css
/* marketing-plans */
--mp-h1: clamp(32px, 4.2vw, 48px);
--mp-name: 20px;
--mp-icon: 48px;
```

Then the four steps of the range move the whole page from one place instead of
restating forty rules apiece. Anything derived stays derived —
`calc(var(--mp-icon) * 22 / 48)` sizes a mark's icon off the mark itself.


