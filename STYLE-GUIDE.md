# ImageWorks Creative — Style Guide

The design system every IWC subpage is built from. It was lifted from the live
home page (`imageworksc/imageworks-home`), settled in
[`Custom-Web-Design`](https://github.com/imageworksc/Custom-Web-Design), and
carried from there into every page since.

This file is the map. The reference itself is in [references/](references/), the
reasoning in [decisions/](decisions/), and the source of truth is
`Custom-Web-Design/styles.css` — where it and any document here disagree, the
stylesheet wins and the document is wrong.

---

## 1. Lineage and the one rule

```
imageworks-home  (the live site — where the colours and the 2px corner come from)
      │
      └── Custom-Web-Design        the system, first written down
             │
             └── branding-page     the system, carried whole + a page block
                    │
                    ├── marketing-plans      (--mp-)
                    ├── ai-web-design        (.ai-)
                    ├── menu-iwc             (tokens only — the nav is its own thing)
                    ├── portfolio-iwc        (tokens + wash + closing band)
                    ├── seo-blogging         (split: iwc-foundation.css + page.css)
                    ├── drupal-and-wordpress (split: iwc-base.css + maintenance.css)
                    ├── setup-optimization   (split: iwc-base.css + iwc-setup.css)
                    └── contact-form-iwc     (tokens + the form block)
```

Every page's stylesheet is **two things kept apart**: the carried system first,
the page's own block after it.

> **Fix the system upstream and carry it across, not in the page.**
> A page that patches the shared half drifts, and the next page carries the
> drift. If a rule belongs to every page, it belongs in `Custom-Web-Design`.

**Carry the system whole.** Unused pieces — the process flow on a page with no
process, the marquee on a page with no portfolio — stay in place rather than
being pruned piecemeal. Carrying it whole is what keeps it a system. The only
thing worth stripping is weight that is genuinely large and genuinely unused
(the branding page drops the eight base64 portfolio thumbnails, ~200KB).

---

## 2. Non-negotiables

| | |
| --- | --- |
| **One theme** | Light. No dark mode. `color-scheme: light`. The brand commits to one visual world. |
| **One corner** | `--r: 2px`. Everything. Buttons, cards, inputs, panels. Never a pill, never a 12px radius. |
| **One typeface** | Plus Jakarta Sans, 300–800. |
| **Three files** | `index.html` · `styles.css` · `script.js`. Nothing crosses between them. |
| **No inline anything** | No `<style>` block, no `style=` attribute, no `<script>` body, and the script never writes a style. The one exception is JSON-LD in the head — moved to a file, crawlers would not read it. |
| **No dependencies** | No framework, no build step, no CDN. Open `index.html` and it works. |
| **No network requests** | The webfont goes in as a base64 `@font-face` in the stylesheet; the icons as an SVG symbol sheet at the top of `<body>`. |
| **No chrome** | A subpage carries no site header and no footer. It is the article; the chrome belongs to whatever it is placed into. The nav lives in `menu-iwc`. |
| **Scope is the copy** | The page carries the sections of the source copy and nothing else. No invented statistic, testimonial, price or FAQ. Anything added later comes from the client, not from the design. |

---

## 3. The rest of it

The reference is split so a reader — or Claude — loads the part in hand rather
than all of it. Nothing was cut; these are the sections that used to be
numbered 3 to 13 in this file.

| | |
| --- | --- |
| [references/tokens.md](references/tokens.md) | The `:root` block, verbatim, and how each colour is used |
| [references/type.md](references/type.md) | The scale, the sizes table, the type components |
| [references/layout.md](references/layout.md) | `.wrap`, the bands and their variants, `.stack` |
| [references/components.md](references/components.md) | Buttons, links, chips, icons, the hero, cards, disclosure, forms, the nav |
| [references/motion.md](references/motion.md) | Easing, the reveal, reduced motion, print |
| [references/responsive.md](references/responsive.md) | The 320 → 5120px range, both directions |
| [references/accessibility.md](references/accessibility.md) | The floor, not the ceiling |
| [references/page-anatomy.md](references/page-anatomy.md) | The head, the JSON-LD, the repo conventions |
| [references/code-style.md](references/code-style.md) | No leading zeros, comment discipline, the house habits |
| [references/checklist.md](references/checklist.md) | Before a page goes live |

## 4. Why things are the way they are

Decisions that shape more than the rule they sit on live in
[decisions/](decisions/) as short records — including the two places the type
scale deliberately sits outside the Global UX rules, and the reason the shared
half is never patched locally.

Start with [decisions/README.md](decisions/README.md).

## 5. What the pages still owe the system

[migration.md](migration.md) — six drift items and three pending carries. None
of it is broken today; all of it is a small job the next time that page is
opened.

---

## Working on this

- The operating rules for every page: [CLAUDE.md](CLAUDE.md)
- The procedure for building one: [.claude/skills/iwc-subpage/SKILL.md](.claude/skills/iwc-subpage/SKILL.md)
- The code itself: [iwc-system.css](iwc-system.css)
- Installing it: [INSTALL.md](INSTALL.md)
