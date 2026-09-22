# Design Decision Records

Short notes on decisions that shape more than the one rule they sit on, or that
someone will eventually want to overturn. They exist so the answer to
"why is it like this?" is a document, not a comment buried at line 287.

Write one when:

- the decision touches several rules, or every page
- it is a deliberate exception to a guideline we otherwise follow
- you had to measure something to reach it
- you can imagine someone changing it next year without knowing what breaks

Do not write one for an ordinary rule. `--r: 2px` needs a record; the fact that
`.btn-row` uses `gap: 14px` does not.

## The records

| # | Decision | Status |
| --- | --- | --- |
| [0001](0001-two-pixel-corner.md) | The corner is 2px, everywhere | Settled |
| [0002](0002-single-light-theme.md) | One light theme, no dark mode | Settled |
| [0003](0003-font-embedded.md) | The webfont is embedded as base64 | Settled |
| [0004](0004-three-files.md) | Three files, nothing inline | Settled |
| [0005](0005-fix-upstream.md) | The system half is fixed upstream, never in a page | Settled |
| [0006](0006-h2-cap-44.md) | The H2 cap stays at 44px, over the 42px guideline | Settled, revisit if the `--one` runs are re-measured |
| [0007](0007-hero-h1-floor.md) | The hero h1 floor stays at 9vw, under the 30px mobile minimum | Settled, conflict noted |
| [0008](0008-band-deep-repoints-tokens.md) | `.band--deep` re-points tokens instead of getting a dark variant | Settled, known wart |
| [0009](0009-shell-stops-at-1840.md) | The shell stops growing at 1840px | Settled |
| [0010](0010-native-details.md) | Disclosure is native `<details>`, not a script | Settled |

## The template

```markdown
# NNNN · Title

**Status** Settled | Open | Superseded by NNNN
**Date** YYYY-MM-DD
**Touches** which files or pages

## What we decided

One paragraph, in the present tense.

## Why

The reasoning, and the measurement if there was one.

## What we gave up

The alternative, and what it would have bought.

## What breaks if this changes

The thing the next person needs to know before overturning it.
```
