# Accessibility

_Part of the ImageWorks Creative design system. Index: [../STYLE-GUIDE.md](../STYLE-GUIDE.md) · Rules: [../CLAUDE.md](../CLAUDE.md) · Code: [../iwc-system.css](../iwc-system.css)_


- `:focus-visible` everywhere, using `--ring`. Never `outline: none` without a
  replacement.
- A `.skip-to-content` link, and `.visually-hidden` for text the screen reader
  needs and the eye does not.
- Every `<section>` takes `aria-labelledby` pointing at its own heading id.
- Decoration is `aria-hidden="true"` — the wash layer, the symbol sheet, every
  icon inside a labelled control, step numbers, mockups.
- `html { scroll-padding-top: calc(var(--nav-h) + 16px); }` so an anchor does
  not land under the bar. If the host site adds a fixed header, this and the
  script's anchor offset are the same measurement — move both.
- Green that carries text is `--green-ink`. Check any new pair; the system
  documents its ratios where they are close (`--grey-soft` / `--grey-ink`,
  5.3:1).
- Prefer the element that already does the work: `<details>` over an accordion
  script, a real tablist with arrow keys over `<div>`s with click handlers.


