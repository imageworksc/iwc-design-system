# 0010 · Disclosure is native `<details>`, not a script

**Status** Settled
**Date** 2026-09-09 (recorded)
**Touches** the FAQ on every page, the service rows on `marketing-plans`

## What we decided

Anything that opens and closes is a native `<details>` / `<summary>`. No
accordion routine, no `aria-expanded` bookkeeping, no height animation in JS.

Opening is CSS: `::details-content` interpolated `0 → auto` under
`interpolate-size: allow-keywords`, with the copy sliding in over it.

## Why

The browser toggles it, announces the state, keeps closed copy out of the
accessibility tree, and makes it findable by in-page search — all without being
asked, and all things a hand-rolled accordion gets wrong at least one of.

It also deleted a routine. The branding page's script was seven functions; six
of them, the accordion included, had nothing left to act on once the sections
they were written for used the right element.

## What we gave up

Exclusivity comes free with a script and has to be chosen with `name` here —
which turned out to be the right default anyway. `marketing-plans`'s service
rows are deliberately **not** exclusive: two can be open at once, which is what
you want when comparing them.

Browsers without `interpolate-size` get a clean snap instead of a slide. They
keep the slide on the copy.

## What breaks if this changes

The free accessibility. Any replacement has to reproduce state announcement,
the accessibility-tree behaviour and find-in-page, and the first two are
usually where a custom accordion fails an audit.
