# 0002 · One light theme, no dark mode

**Status** Settled
**Date** 2026-09-09 (recorded)
**Touches** `color-scheme`, every colour token, every page

## What we decided

`color-scheme: light`. No `prefers-color-scheme` block, no dark variant of any
component, no theme toggle.

## Why

The brand commits to one visual world. These are marketing pages carrying a
client's identity, not an application someone sits in for eight hours — the
argument for dark mode (long sessions, low light, user preference) does not
apply, and the argument against (two sets of every colour decision, two sets of
contrast checks, two things to keep in step across nine pages) does.

The dark surfaces the pages do have — `.band--cta`, `.band--deep` — are
*designed* dark, not a theme. They are part of the light page's rhythm.

## What we gave up

Respecting a visitor's system preference. On a page they will spend ninety
seconds on, we judged the consistency worth more.

## What breaks if this changes

Everything, twice. The colour tokens are semantic enough to re-point (see
[0008](0008-band-deep-repoints-tokens.md)), but every contrast pair would need
re-checking, the hero washes are tuned for a light ground and would need
rebuilding, and the card recipe's white-to-near-white gradient has no dark
equivalent that reads the same.
