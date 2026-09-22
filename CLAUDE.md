# ImageWorks Creative — general guidelines

These apply to **every** page we build. They are the operating rules, and they
are short enough to keep loaded the whole time.

Everything else is looked up as needed:

- **[STYLE-GUIDE.md](STYLE-GUIDE.md)** — the map
- **[references/](references/)** — the reference, by subject. Load the one file
  the task needs, not all ten
- **[decisions/](decisions/)** — why things are the way they are. Read before
  overruling anything here
- **[iwc-system.css](iwc-system.css)** — the code itself, and the source of
  truth. Where it and a document disagree, the stylesheet is right
- **[migration.md](migration.md)** — what the pages still owe the system

---

## What we build

A **subpage**: one self-contained static page, no framework, no build step, no
dependencies. It gets published to GitHub Pages for review and then dropped
into the production site (Drupal) as an article.

A subpage carries **no site header and no footer**. It is the content; the
chrome belongs to whatever it is placed into. The nav lives in its own repo
(`imageworksc/menu-iwc`).

---

## 1. Three files, and nothing crosses between them

```
index.html    the markup, and nothing else
styles.css    every rule on the page
script.js     only the behaviour that genuinely needs a script
```

- No `<style>` block. No `style=` attribute. No `<script>` body.
- The script never sets a style. The one thing it may set is a **custom
  property holding a measurement** the stylesheet cannot know ahead of time
  (a rendered label's width, for instance) — what that measurement *does* is
  still decided in the CSS.
- The only inline exception is **JSON-LD in the head**. Moved to a file,
  crawlers would not read it.

## 2. The system half is not yours to edit

Every `styles.css` is two things kept apart:

```
┌─ iwc-system.css, verbatim ────────── the shared system. Do not touch.
└─ this page's own block ───────────── prefixed (bd-, mp-, ai-, …)
```

**Found a bug in the system half? Fix it upstream in
`imageworksc/Custom-Web-Design` and carry the fix across.** Patching it inside
one page makes that page drift, and the next page inherits the drift. If a rule
belongs on every page, it belongs upstream.

**Carry the system whole.** Leave the parts this page has no use for. Pruning
piecemeal is how a system becomes eight slightly different systems. The only
thing worth stripping is genuinely large, genuinely unused weight — the eight
base64 portfolio thumbnails, say.

## 3. Scope is the copy — this is the rule people break

The page carries the sections of the source copy. **Nothing else.**

- Do not invent a statistic, a testimonial, a price, a client name, an award,
  a years-in-business figure, or an FAQ.
- Do not add a section because the layout looks thin. If a band feels empty,
  the fix is the design, not filler.
- Do not soften or rewrite a client's claim to make it read better.
- If the copy is missing something the page needs, **say so and ask** — new
  copy comes from the client, not from us.

Everything factual on the page must be traceable to the source document or to
the confirmed brand facts below.

### Confirmed brand facts

```
ImageWorks Creative · founded 1997 · in-house team
44679 Endicott Dr Suite 300 Unit 580, Ashburn, VA 20147, US
+1 703 928 7309 · sales@imageworkscreative.com
linkedin.com/company/imageworks-creative · x.com/imageworks · instagram.com/imageworks_creative
```

Anything not on that list needs confirming before it ships.

## 4. Markup

- Semantic HTML first. `<section>`, `<h2>`, `<ul>`, `<details>`, `<button>`.
  A `<div>` with a click handler is a bug.
- Every `<section>` takes `aria-labelledby` pointing at its own heading id.
- One `<h1>`, in the hero. Headings descend without skipping.
- Decoration is `aria-hidden="true"` — the wash layer, the icon sheet, every
  icon inside an already-labelled control.
- Icons come from the **SVG symbol sheet** at the top of `<body>`, used as
  `<svg class="icon" aria-hidden="true"><use href="#i-check"/></svg>`.
- Section order is always: hero → bands → `.band--cta` closing call.

## 5. CSS

- Use the tokens. If you are typing a hex value or a bare pixel size into the
  page block, stop and check whether a token already says it.
- **Every size the page block uses is declared once**, prefixed, at the head
  of that block (`--mp-h1`, `--mp-icon`, …). Nothing else carries a bare pixel
  size. That is what lets the whole page move from one place at the ends of the
  range instead of restating forty rules.
- Keep things derived: `calc(var(--mp-icon) * 22 / 48)` sizes a mark's icon off
  the mark itself.
- Prefer logical properties (`padding-block`, `inline-size`, `margin-inline`).
- The corner is `var(--r)` — 2px. Always. No pills, no 12px radius.
- No `!important` outside the reduced-motion blanket.
- No dark mode. `color-scheme: light`. One visual world.

## 6. JavaScript

- Ask first: **does this need a script at all?** `<details>` beats an accordion
  routine — the browser toggles it, announces the state, and keeps closed copy
  out of the accessibility tree for free. A CSS transition beats a `requestAnimationFrame`
  loop. Most of what looks like behaviour is a stylesheet.
- Loaded with `defer`. `'use strict'`. Modern ES — `const`/`let`, arrow
  functions, `for…of`, `??`. No `var`, no jQuery, no polyfill.
- Feature-detect and degrade: if `IntersectionObserver` is missing, everything
  is simply revealed.
- Never let a script stand between the user and a form submission.

## 7. Accessibility — non-negotiable

- `:focus-visible` on everything interactive, using `--ring`. Never
  `outline: none` without a replacement.
- Tab all the way through before calling it done. Nothing skipped, nothing
  trapped, focus returns where it came from after a panel or drawer closes.
- Green that carries text is `--green-ink` (`#5c9a2e`). `#80c34a` on white does
  not clear AA. Check any new pair.
- **Body copy never goes below 16px**, at any width. Form inputs never below
  16px either, or iOS zooms the page.
- `prefers-reduced-motion` is honoured on every page, and honoured properly:
  colour and tint changes stay, only the travel goes. Nothing may end on a
  wrong frame or disappear.
- A `.skip-to-content` link, and `.visually-hidden` for text the screen reader
  needs and the eye does not.

## 8. Performance

- **The page makes no external network request.** The font is embedded as
  base64; the icons are inline SVG. Never a Google Fonts `<link>`, never a CDN.
- Images are sized, compressed, and carry real `alt` text (or `alt=""` if
  decorative). Below the fold they are `loading="lazy"`.
- Animate `transform` and `opacity`. Nothing that triggers layout.
- Ambient animation is cheap and slow — three washes, minute-long periods, one
  `will-change`. Not a canvas.

## 9. The head

Every page ships with: `title` (`Page Name | ImageWorks Creative`), a real
`description`, `theme-color` `#143c66`, `canonical`, the Open Graph set, the
Twitter set, and one JSON-LD `@graph` (`Organization` → `WebPage` with
`BreadcrumbList` → `Service`).

- **No `PLACEHOLDER` may ever reach a review link.** If a route or an image is
  not confirmed yet, it goes in the README's "Before this goes live" list, and
  you say so out loud when you hand the page over.
- `og:image` must be a real 1200×630 file that actually exists at that URL.
- If the production site already has sitewide Organization schema, the
  subpage's `provider` is name + url only, so the two do not conflict.

## 10. The range

Built and measured **320px → 5120px**, no horizontal overflow at any width,
with every disclosure open.

Below 1800px the shell caps are the intended measure — leave them alone. Above
it, step the tokens: 1320/1560/1840 shell, 18/20/23 body. See STYLE-GUIDE.md §8.

## 11. Comments

Comments explain **why**, not what. The rejected alternative, the measurement
behind a number, the bug the rule fixes. This is the house style and it is the
reason these pages are still editable a year later — keep writing them.

```css
/* Was a jump straight to navy, which read louder than the green button
   next to it. #c3d6ea is the ring the reached process step already uses. */
.btn--quiet:hover { border-color: #c3d6ea; }
```

## 12. Repo

```
index.html · styles.css · script.js · assets/ · .nojekyll · README.md
```

Published from the repository root at `https://imageworksc.github.io/<repo>/`.

Bump `?v=` on `styles.css` and `script.js` **together** whenever markup and CSS
change in step — Pages serves both with `max-age=600`, and a browser holding
one while it refetches the other renders the page unstyled.

The README states the page's scope, the stylesheet split, and a **"Before this
goes live"** list naming every route, phone number, meeting link and canonical
URL still to confirm.

---

## Before you say it is done

- [ ] Every claim on the page traces to the source copy
- [ ] No `PLACEHOLDER`, no lorem, no invented figure
- [ ] Canonical, `og:url` and JSON-LD `@id` agree and point at the real route
- [ ] `og:image` exists, 1200×630
- [ ] Font embedded; zero external requests (check the network panel)
- [ ] No `<style>`, no `style=`, no inline `<script>` body
- [ ] 320 → 5120px, no horizontal overflow, every disclosure open
- [ ] Tabbed through: ring visible, nothing trapped
- [ ] Reduced motion on: nothing snapped, nothing hidden
- [ ] The system half of `styles.css` is identical to `iwc-system.css`
- [ ] `?v=` bumped

---

## How to work with us

- **Ask before inventing.** Missing copy, an unconfirmed route, an ambiguous
  claim — ask. A wrong fact on a client page costs more than a round trip.
- **Show the whole page, not a snippet.** We review in the browser, at the real
  widths.
- **Say what you did not do.** If something was left out or could not be
  confirmed, name it. Do not let it surface at launch.
- **One change at a time in the system half.** It reaches nine pages.

---

## House rules — typography sizes

From **Global UX + Design Rules**. These are the sizes the type scale is built
to hold. The scale itself is in `iwc-system.css`; use its tokens rather than
typing these numbers into a page.

**Desktop**

```
Body            17–18px, never under 16px, line-height ~1.6
H1              42–56px
H2              32–42px
H3              22–28px
Headlines       line-height 1.1–1.25
```

**Mobile**

```
Body            16–17px minimum
H1              30–36px
H2              26–32px
```

Hierarchy in every major section: **headline** (largest, says what the section
is about) → **subhead** (smaller, the point or benefit, only when needed) →
**body** (smaller again, the supporting detail).

These are guidelines, not specifications — the hierarchy matters more than
hitting an exact number. Where our scale sits against each range, and the two
places it deliberately falls outside, is the table in STYLE-GUIDE.md §4.

<!-- Only the typography sizes from that document are carried here. The rest of
     it — content width, spacing, CTA and mobile rules — has not been merged. -->

