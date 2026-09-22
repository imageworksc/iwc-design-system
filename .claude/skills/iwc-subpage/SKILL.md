---
name: iwc-subpage
description: Build or update an ImageWorks Creative subpage — a standalone static landing page on the shared IWC design system. Use whenever the task is an IWC page, section, hero, band, CTA, form or nav, or when someone hands over source copy or a deck to turn into a page. Also use before editing any existing IWC page repo (branding-page, marketing-plans, ai-web-design, menu-iwc, portfolio-iwc, seo-blogging, drupal-and-wordpress, setup-optimization, contact-form-iwc, Custom-Web-Design).
---

# Building an ImageWorks Creative subpage

This file is the procedure. The rules are in [CLAUDE.md](../../../CLAUDE.md) —
read that first, always.

The reference is split, so **load only the part in hand** rather than all of it:

| Working on | Read |
| --- | --- |
| colours, surfaces, shadows, the `:root` block | [references/tokens.md](../../../references/tokens.md) |
| headings, body, the scale, the sizes table | [references/type.md](../../../references/type.md) |
| bands, the shell, section rhythm | [references/layout.md](../../../references/layout.md) |
| a button, chip, card, hero, FAQ, form, the nav | [references/components.md](../../../references/components.md) |
| animation, reveals, reduced motion | [references/motion.md](../../../references/motion.md) |
| any width question, the large-screen steps | [references/responsive.md](../../../references/responsive.md) |
| focus, ARIA, contrast | [references/accessibility.md](../../../references/accessibility.md) |
| the head, JSON-LD, repo layout | [references/page-anatomy.md](../../../references/page-anatomy.md) |
| writing the CSS, HTML or JS itself | [references/code-style.md](../../../references/code-style.md) |
| shipping | [references/checklist.md](../../../references/checklist.md) |

[STYLE-GUIDE.md](../../../STYLE-GUIDE.md) is the map over all of them.

**Before overruling anything in those files, check
[decisions/](../../../decisions/).** Most of what looks like an oddity — the
44px H2 cap, `--navy` being white inside `.band--deep`, the shared half nobody
may patch — is a recorded decision with a measurement behind it. If you still
think it should change, say which record you are overturning and why.

What the pages currently owe the system is in
[migration.md](../../../migration.md).

## A new page

**1. Settle the scope before writing anything.**

Read the source copy end to end and list its sections back to the person who
handed it over — numbered, in order, with what each one carries. That list is
the page. Nothing joins it later without coming from the client.

Flag in the same message: anything missing, any claim you cannot source, any
route or link you cannot confirm.

**2. Scaffold.**

```
index.html · styles.css · script.js · assets/ · .nojekyll · README.md
```

`styles.css` opens with `iwc-system.css` pasted in verbatim. Everything you
write for this page goes underneath it behind a two-letter prefix.

**3. Declare the page's tokens.**

Before writing a single rule, list every size the page needs and declare them
once at the head of your block:

```css
/* --xx- : this page's own scale. Nothing below carries a bare pixel size. */
--xx-h1: clamp(32px, 4.2vw, 48px);
--xx-sec: clamp(26px, 3vw, 38px);
--xx-lead: 18px;
--xx-icon: 48px;
```

Sizes follow the branding page one for one at the design width unless the copy
demands otherwise: 48px headline, 38px section heads, 18px lead.

**4. Build the page in bands.**

```html
<section class="band band--tint" aria-labelledby="x-title">
  <div class="wrap stack reveal">
    <p class="eyebrow">Kicker</p>
    <h2 class="sec-title sec-title--wide" id="x-title">Heading with an <em>accent</em></h2>
    <p class="lead">…</p>
    <!-- the section's own content -->
  </div>
</section>
```

Alternate white and `.band--tint` so the page reads in slabs. The hero comes
first with its three washes; the closing call is always `.band--cta`.

**5. Write the head.** Title, description, canonical, OG set, Twitter set, one
JSON-LD `@graph`. Real values or an entry in the README's "Before this goes
live" list — never `PLACEHOLDER` on a review link.

**6. Inline the font.** `base64 -w0 fonts/plus-jakarta-sans-latin.woff2` into
the `@font-face` `src`, replacing the kit's placeholder.

**7. Measure it.** 320px, 360px, 640px, 900px, 1180px, 1440px, 1920px, 2560px,
3840px, 5120px. Every disclosure open. No horizontal overflow anywhere.

**8. Run the checklist** — [references/checklist.md](../../../references/checklist.md),
also at the foot of CLAUDE.md — then hand it over with what still needs
confirming.

**9. Write down anything you had to decide.** If you measured something to
settle it, made a deliberate exception to a guideline, or answered a question
that will be asked again, it is a decision record, not a comment. Add it to
[decisions/](../../../decisions/) using the template in that folder's README,
and point the code comment at it.

## An existing page

**Before touching it:** open `styles.css` and find the boundary comment
(`Page additions only. Everything above is the shared … system`). Know which
side of it you are on.

- **Above the line** — stop. Fix it in `imageworksc/Custom-Web-Design`, then
  carry the fix into every page that has it. Say which pages those are.
- **Below the line** — go ahead, but use the page's own tokens; do not
  introduce a bare pixel size beside them.

Check whether the change needs the four size steps updated too (1800 / 2400 /
3200 and the base) — a new token that only exists at the design width is a bug
that only shows on a 4K panel.

Bump `?v=` if markup and CSS changed together.

## What to reach for

| Need | Use | Not |
| --- | --- | --- |
| An expanding row | `<details>` on the FAQ recipe | an accordion script |
| A tab pair | a real tablist, arrow keys, `#hash` opening its panel | divs with click handlers |
| A surface | the card recipe (gradient + `--shadow-card` + `--r`) | a new border-radius |
| A list of rows | `.signals` (ruled) or `.cms-list` (carded) | a table |
| Emphasis in a heading | `<em>` — the system makes it the green accent | a `<span>` and a colour |
| An icon | `<use href="#i-…">` from the symbol sheet | an inline path, an icon font |
| A section entrance | `.reveal` | a scroll library |
| A number that must be measured | a custom property set by the script | styling from JS |

## The three failures to watch for

1. **Inventing content** to fill a layout. The page carries the copy and
   nothing else.
2. **Patching the system half** because it is the file already open. It reaches
   nine pages.
3. **A bare pixel size** in the page block. It will not move at 1800px and the
   page will read as a stripe on a large display.
