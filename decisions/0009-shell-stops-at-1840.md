# 0009 · The shell stops growing at 1840px

**Status** Settled
**Date** 2026-09-09 (recorded)
**Touches** `--shell` and the large-screen steps in each page block

## What we decided

The shell is 1180px at the design width and steps up three times — 1320 at
1800px, 1560 at 2400px, 1840 at 3200px — and then stops. A 5120px viewport gets
generous margins, not a wider column.

Nothing below 1800px is touched.

## Why

Past 1800px the caps stop being a measure and start being a stripe: on a 4K
panel reporting 3840 CSS pixels, an 1180px shell covers under a third of the
screen at a body size physically half what the same value gives on a 1080p
monitor. So the shell and the type grow together.

They stop together too. More width past 1840px would only lengthen the line —
an open detail measures 75 characters at the design width and still only 85 at
4K. Wider is worse to read, not better.

## What we gave up

Filling a 5K display. Someone will eventually say the page "looks narrow" on
one; the answer is that a 110-character line is unreadable and the margin is
doing its job.

## What breaks if this changes

Every measured `--one` / `--two` run, which is set against a known column
width, and the four size steps in each page block, which are tuned in pairs
with the shell.
