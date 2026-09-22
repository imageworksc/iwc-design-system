# ImageWorks Creative — design system

The system every IWC subpage is built from, packaged so an AI assistant — or a
new developer — produces pages that match it instead of something adjacent.

It is the rules, the reference, the reasoning behind both, and the CSS itself.
No framework, no build step, no dependencies: the pages it describes are three
static files that open in a browser.

**→ [INSTALL.md](INSTALL.md)** — get it working in about thirty seconds.

---

## What's here

```
CLAUDE.md                    the rules, always on
INSTALL.md                   how to install it
STYLE-GUIDE.md               the map over everything below
iwc-system.css               the shared half of every page stylesheet
references/                  the reference, ten files by subject
decisions/                   why things are the way they are
migration.md                 what the pages still owe the system
fonts/                       Plus Jakarta Sans, to inline before shipping
.claude/skills/iwc-subpage/  the build procedure, as a skill
```

| Piece | What it is |
| --- | --- |
| **`CLAUDE.md`** | The operating rules for every page — scope, markup, CSS, JS, accessibility, performance, the head, the typography sizes, and the pre-ship checklist. Short on purpose: it is meant to stay loaded the whole time. |
| **`references/`** | The reference, split by subject — tokens, type, layout, components, motion, responsive, accessibility, page anatomy, code style, checklist. Split so a reader loads the part in hand instead of thirty kilobytes. |
| **`decisions/`** | Ten short records on the choices that shape more than the rule they sit on, including the two places the type scale deliberately sits outside the Global UX rules. Read one before overruling it. |
| **`iwc-system.css`** | The shared half of every page stylesheet, verbatim. Paste it at the top of a new page's `styles.css` and write that page's own block underneath. |
| **`migration.md`** | Six drift items and three pending carries. Nothing broken today; each is a small job next time that page is opened. |
| **`.claude/skills/iwc-subpage/`** | The build procedure as an invocable skill. It routes to the right reference file per task. |

---

## Lineage

```
imageworks-home  (the live site — where the colours and the 2px corner come from)
      │
      └── Custom-Web-Design        the system, first written down
             │
             └── branding-page     the system, carried whole + a page block
                    │
                    ├── marketing-plans · ai-web-design · menu-iwc
                    ├── portfolio-iwc · contact-form-iwc
                    └── seo-blogging · drupal-and-wordpress · setup-optimization
```

The shared half is currently byte-identical across `branding-page`,
`marketing-plans` and `ai-web-design`. That property is what makes a fix
carryable at all.

---

## The rule that keeps it one system

> **Fix the system here and carry it across, never inside a page.**
> A page that patches the shared half drifts, and the next page inherits the
> drift.

When `iwc-system.css` changes:

1. Change it here.
2. Carry it into each page's `styles.css`, in one pass.
3. Bump `?v=` on the pages you touched.
4. Record it in the **Pending carries** table in `migration.md`, and strike it
   when it has reached every page.

When a *decision* is made — a measurement settled it, or it is a deliberate
exception — write a record in `decisions/` using the template in that folder's
README. That is what stops the same question being re-litigated every six
months.

---

## Status

Tracked in [migration.md](migration.md):

- **Three pending carries.** Type-scale fixes live here and have not reached the
  live pages — held deliberately so they go across in one pass.
- **Six drift items.** Five pages still load the font from Google Fonts, two
  still carry `PLACEHOLDER` canonicals, three still split the CSS across two
  files.
- **Two open questions.** The 64px hero cap against the Global UX rules' 56px,
  and whether to introduce a real semantic token layer so `.band--deep` stops
  renaming `--navy` to white.

Merged from **Global UX + Design Rules**: the typography sizes, in `CLAUDE.md`
under *House rules*. Content width, spacing, CTA and mobile rules from that
document have not been merged yet.

---

## Licence

MIT — see [LICENSE](LICENSE). The font in `fonts/` is separately licensed under
the SIL Open Font License 1.1; see [fonts/README.md](fonts/README.md).

Author: **Sam Aponte**
