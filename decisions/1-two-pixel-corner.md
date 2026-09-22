# 1 · The corner is 2px, everywhere

**Status** Settled
**Date** 2026-09-09 (recorded; the decision predates the repos)
**Touches** `--r`, every surface in the system

## What we decided

Every corner in the system is `var(--r)`, which is `2px`. Buttons, cards,
inputs, panels, the chip well, the drawer. There are no exceptions and no
second radius token.

## Why

It comes from the live home page, which squares its corners at 2px. It is the
single most recognisable thing about the brand's surfaces — soft enough not to
read as a hard edge, tight enough that nothing looks like a consumer app.

Holding it to one value is what makes it read as a decision rather than a
default. A system with three radii has none.

## What we gave up

Rounded cards, pill buttons, and the softer look those carry. On a page selling
design services, that softness reads as generic; the square corner reads as
deliberate.

## What breaks if this changes

Nothing mechanically — `--r` is one token and every rule reads it. But it
changes the character of all nine pages at once, so it is a brand decision, not
a CSS one.

The one circle in the system is `.chip`, at `border-radius: 50%`. It is a
22px icon well, never text, and it is deliberate contrast rather than drift.
