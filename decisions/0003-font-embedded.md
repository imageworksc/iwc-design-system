# 0003 · The webfont is embedded as base64

**Status** Settled
**Date** 2026-09-09 (recorded)
**Touches** the `@font-face` at the top of every `styles.css`

## What we decided

Plus Jakarta Sans ships inside the stylesheet as a base64 `data:` URI, latin
subset, variable across `300 800`. Never a Google Fonts `<link>`, never a
same-origin `url(fonts/…)`. The page makes no network request for type.

## Why

Two round trips removed and no flash. A Google Fonts link costs a DNS lookup, a
TLS handshake, a CSS fetch, and only then the font file — on a phone on a slow
connection that is most of a second of unstyled or invisible text on the one
screen that has to land.

It also makes the page portable. It is dropped into Drupal as an article;
whatever that page already loads, ours does not depend on.

## What we gave up

About 27KB of the stylesheet, uncacheable separately from it, and the ability
to update the font without touching every page.

## What breaks if this changes

Nothing structural — but five of the nine pages still load from Google Fonts
and are the reason this is written down. See [migration.md](../migration.md).

The kit ships `iwc-system.css` with a `PASTE_PAYLOAD_HERE` placeholder so the
file stays readable; inlining it is a step in the build, not an option.
