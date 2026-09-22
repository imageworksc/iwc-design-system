# 0007 · The hero h1 floor stays at 9vw, under the 30px mobile minimum

**Status** Settled — genuine conflict, recorded rather than resolved
**Date** 2026-09-22
**Touches** `.hero h1` on every page

## What we decided

`font-size: clamp(min(9vw, 36px), 4.2vw + 8px, 64px)` stays as written. At
320px that floor gives **28.8px**, against the Global UX + Design Rules' mobile
H1 minimum of 30px.

## Why

The two cannot both be had. The largest size that still holds the hero headline
to three lines at 320px measured **29.5px**. The rules want 30px and up. There
is no value that satisfies both.

Of the two failures, a headline broken across five lines on the first screen is
worse than one sitting 1.2px under a guideline nobody will measure.

The miss is also narrow: from **334px** up the ramp is inside the range, and
334px is below every phone still in meaningful use.

## The other end

The same clamp caps at 64px against a 56px maximum. At the 1180px design width
it renders 57.6px, and only a display wider than 1333px ever reaches 64. Left
as is for now — changing it reflows nine heroes — but it is the weaker of the
two exceptions and the first one to give up if the rules are enforced strictly.

## What we gave up

A clean compliance table. The scale now has two asterisks in it instead of
none, which is why both are written down.

## What breaks if this changes

Raise the floor to 30px and the headline on a 320px phone breaks to four or
five lines. Before changing it, re-measure the actual headline of the longest
page at 320px — the 29.5px figure is specific to *"Custom Web Design"* and a
shorter headline may leave room.
