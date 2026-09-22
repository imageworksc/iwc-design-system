# 0004 · Three files, nothing inline

**Status** Settled
**Date** 2026-09-09 (recorded)
**Touches** every page repo

## What we decided

`index.html`, `styles.css`, `script.js`. No `<style>` block, no `style=`
attribute, no `<script>` body, and the script never writes a style.

The single exception is JSON-LD in the head, which is structured data rather
than behaviour — moved to a file, crawlers would not read it.

## Why

One place to look for each kind of thing. A rule is in the stylesheet or it
does not exist; behaviour is in the script or it does not exist. The pages get
handed between people and pasted into a CMS, and the failure mode we kept
hitting was a `style=` overriding a rule nobody could find.

The script may set **one** kind of thing: a custom property holding a
measurement the stylesheet cannot know ahead of time — a rendered label's
width, for instance. What that measurement *does* is still decided in the CSS.

## What we gave up

Critical-CSS inlining, and the convenience of a one-off `style=` during a quick
fix. The second is the one people reach for; it is also the one that rots.

## What breaks if this changes

Nothing at once. It degrades — one inline style becomes five, and then the
stylesheet is no longer the answer to "why does this look like that?"
