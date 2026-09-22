# 5 · The system half is fixed upstream, never in a page

**Status** Settled
**Date** 2026-09-09 (recorded)
**Touches** all nine page repos and `Custom-Web-Design`

## What we decided

Every page's `styles.css` is two things kept apart: the shared system carried
in verbatim, then the page's own block behind a prefix. A bug in the shared
half is fixed in `Custom-Web-Design` and carried across every page, never
patched inside the page that happened to be open.

The system is carried **whole**. The parts a page has no use for stay.

## Why

It is the only thing keeping nine pages one system. The shared half is
currently byte-identical across `branding-page`, `marketing-plans` and
`ai-web-design` — that property is what makes a fix carryable at all, and it
survives exactly as long as nobody patches locally.

Carrying it whole matters for the same reason. Pruning the unused parts
page-by-page means nine subsets that diverge, and the next carry has to be
merged by hand instead of pasted.

## What we gave up

Dead CSS in every page — the process flow on a page with no process, the
marquee on a page with no portfolio. Roughly a third of the shared half is
unused on any given page. That is the rent.

The one thing worth stripping is genuinely large, genuinely unused weight: the
branding page drops the eight base64 portfolio thumbnails, about 200KB.

## What breaks if this changes

The byte-identical property, and with it every future fix. Once two pages
disagree about the shared half, there is no longer an upstream.
