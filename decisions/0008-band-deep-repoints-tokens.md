# 0008 · `.band--deep` re-points tokens instead of getting a dark variant

**Status** Settled — known wart, see *What breaks*
**Date** 2026-09-09 (recorded)
**Touches** `.band--deep` and everything that renders inside one

## What we decided

The deep navy band does not carry dark variants of its children. It redeclares
the semantic tokens on itself, and every child flips for free:

```css
.band--deep {
  --heading: #ffffff;
  --text: rgba(226, 238, 252, .82);
  --muted: rgba(226, 238, 252, .70);
  --border: rgba(255, 255, 255, .16);
  --navy: #ffffff;
}
```

## Why

Otherwise every component needs a `.band--deep .thing` override, and a new
component is not finished until someone remembers to write one. Re-pointing
means a component dropped into the band works the first time.

It is also how the system stays small: one block of five declarations replaces
what would be forty overrides scattered through the file.

## What we gave up

Clarity, at one specific point. `--navy: #ffffff` means the token named *navy*
is white inside this band. It works, it is commented, and it is still the line
that stops a new reader.

The clean version is a real semantic layer — `--color-heading: var(--navy)` at
the root, and `.band--deep { --color-heading: #fff; }` — where nothing is ever
renamed to its opposite.

## What breaks if this changes

Introducing that layer is low-risk if the existing names are kept as aliases,
but it has to be carried to all nine pages in one pass to preserve the
byte-identical shared half ([0005](0005-fix-upstream.md)). Deferred, not
rejected.
