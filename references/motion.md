# Motion

_Part of the ImageWorks Creative design system. Index: [../STYLE-GUIDE.md](../STYLE-GUIDE.md) · Rules: [../CLAUDE.md](../CLAUDE.md) · Code: [../iwc-system.css](../iwc-system.css)_


| | |
| --- | --- |
| **Easing** | `--ease: cubic-bezier(.16, .84, .44, 1)` — everything |
| **Durations** | `.25s` interaction · `.3–.4s` colour and disclosure · `.55–.8s` entrance · 47–127s ambient |
| **Hover** | a button lifts 3px; a card lifts inside its own border so it gains no height; a row changes colour rather than moving |

### Reveal

The one thing that needs a script, because it has to know when a section comes
into view.

```css
[data-anim="on"] .reveal {
  opacity: 0;
  transform: translateY(16px);
  transition: opacity .7s var(--ease), transform .7s var(--ease);
  transition-delay: var(--reveal-delay, 0ms);
}
[data-anim="on"] .reveal.is-revealed { opacity: 1; transform: none; }
```

`script.js` sets `data-anim="on"` on `<html>`, then observes every `.reveal`
with `rootMargin: '0px 0px -12% 0px'`, `threshold: 0.12`, unobserving each one
as it fires. Two guards matter:

1. If the visitor asked for reduced motion, or `IntersectionObserver` is
   missing, **everything is revealed immediately** — the flag still goes on, so
   the stylesheet only hides a `.reveal` while the page is in a position to
   bring it back.
2. The negative `rootMargin` means anything in the last slice of a
   fully-scrolled page would never trigger, so a scroll/load handler reveals
   the remainder once the visitor reaches the bottom.

Items inside a revealed block stagger off an index set in the markup:

```css
.is-revealed .signals li {
  animation: signal-in .55s var(--ease) backwards;
  animation-delay: calc(var(--i) * .09s + .22s);
}
```

### Reduced motion

Every page ends with the blanket, then the exceptions the blanket gets wrong:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: .01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: .01ms !important;
    scroll-behavior: auto !important;
  }
  [data-anim="on"] .reveal { opacity: 1; transform: none; }
}
```

The exceptions are anything the blanket would snap to a wrong end frame — a
marquee becomes a scrollable strip (`animation: none !important` plus
`overflow-x: auto`, mask removed); a rail that draws itself is given its final
length outright; a node parked at the end of a static rail is hidden, because
it would read as a stray dot. **Colour and tint changes stay. Only the travel
goes.**

### Print

```css
@media print {
  .band { padding-block: 24px; }
  [data-anim="on"] .reveal { opacity: 1; transform: none; }
}
```


