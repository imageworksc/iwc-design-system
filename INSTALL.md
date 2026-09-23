# Quick install

The ImageWorks Creative design system, packaged so an AI assistant builds pages
that match it instead of inventing something adjacent.

You get the rules, the reference, the reasoning behind it, and the CSS itself.
Point your tool at them once and every page after that starts from the same
place.

---

## The fastest way — one file

**Download [`CLAUDE.md`](CLAUDE.md).** It is the operating rules for every page,
readable on its own, and it is enough to start:

```bash
curl -O https://raw.githubusercontent.com/imageworksc/iwc-design-system/main/CLAUDE.md
```

Or open it in GitHub and use the **download raw file** button at the top right
of the file view.

| Tool | Put it at |
| --- | --- |
| **Claude Code** | `CLAUDE.md` in the repo root — loads automatically, nothing to invoke |
| **Claude.ai / Claude desktop** | Project → **Set project instructions** → paste the whole file |
| **Cursor** | `.cursorrules` |
| **Codex** | `AGENTS.md` |
| **Copilot** | `.github/copilot-instructions.md` |

Then ask for the page — *"Build the IWC subpage in the attached copy"* — and the
rules are already loaded.

Everything below is for when you want the rest: the stylesheet, the reference,
the decision records and the skill.

---

## Claude Code — 30 seconds

```bash
git clone https://github.com/imageworksc/iwc-design-system.git
```

Then, from the repo you are building a page in:

```bash
cp -r ../iwc-design-system/{CLAUDE.md,STYLE-GUIDE.md,iwc-system.css,references,decisions,migration.md} .
cp -r ../iwc-design-system/.claude .
```

That is it. `CLAUDE.md` loads automatically at the start of every session in
that repo, and the skill is available as `/iwc-subpage` — Claude will also
reach for it on its own when the task is an IWC page.

**Prefer not to copy nine times?** Keep the clone next to your page repos and
import it instead. A one-line `CLAUDE.md` in each page repo:

```markdown
@../iwc-design-system/CLAUDE.md
@../iwc-design-system/STYLE-GUIDE.md
```

Then a `git pull` in the clone updates every page repo at once.

**Want it on for everything you do**, regardless of which repo is open:

```bash
cp iwc-design-system/CLAUDE.md ~/.claude/CLAUDE.md
cp -r iwc-design-system/.claude/skills/iwc-subpage ~/.claude/skills/
```

---

## Claude.ai — a shared Project

1. **Projects → Create project.** Name it `ImageWorks Creative — Subpages`.
2. **Set project instructions** → paste all of `CLAUDE.md`. These are read on
   every message, which is where rules that must always apply belong.
3. **Add to project knowledge** → upload `STYLE-GUIDE.md`, `iwc-system.css`,
   `migration.md`, and everything in `references/` and `decisions/`.
4. On a Team plan, **share the project with the organisation** so everyone
   works from one copy rather than their own.

---

## Cursor, Codex, Copilot, or anything else

There is nothing Claude-specific in the content — it is Markdown and CSS.

- Put `CLAUDE.md` wherever your tool reads always-on rules
  (`.cursorrules`, `AGENTS.md`, `.github/copilot-instructions.md`, …).
- Keep `references/`, `decisions/` and `iwc-system.css` in the repo so the tool
  can open them, and tell it they are there.

---

## Building your first page

Start the session with the source copy and say what it is:

> Build the ImageWorks subpage in the attached copy.

The assistant should come back with the page's sections listed before it writes
anything. If it starts generating markup without settling the scope first, stop
it — that step is the one that keeps invented content off the page.

### Where it should be looking

The reference is split so only the part in hand gets loaded:

| Working on | File |
| --- | --- |
| colours, surfaces, shadows | `references/tokens.md` |
| headings, body, the scale | `references/type.md` |
| bands, the shell, rhythm | `references/layout.md` |
| buttons, chips, cards, hero, FAQ, forms, nav | `references/components.md` |
| animation and reduced motion | `references/motion.md` |
| any width question | `references/responsive.md` |
| focus, ARIA, contrast | `references/accessibility.md` |
| the head, JSON-LD, repo layout | `references/page-anatomy.md` |
| writing the CSS itself | `references/code-style.md` |
| shipping | `references/checklist.md` |

`decisions/` holds ten records explaining choices that look odd until you know
why — the 44px H2 cap, `--navy` being white inside `.band--deep`, the rule that
the shared half is never patched locally. **Read the record before overruling
anything.**

---

## The one thing to get right

Every page's `styles.css` is two halves:

```
┌─ iwc-system.css, pasted in verbatim ──── the shared system. Do not edit.
└─ this page's own block ───────────────── behind a prefix (bd-, mp-, ai-, …)
```

Found a bug in the shared half? Fix it **here**, in this repo, and carry it
across every page. Patching it inside one page is how nine pages become nine
slightly different systems.

---

## Before a page ships

Inline the font. `iwc-system.css` ships with a placeholder so the file stays
readable:

```bash
base64 -w0 fonts/plus-jakarta-sans-latin.woff2
```

Paste the result over `PASTE_PAYLOAD_HERE` in the `@font-face` block. A shipped
page makes no external network request.

Then run `references/checklist.md`.

---

## Staying current

```bash
git -C iwc-design-system pull
```

When `iwc-system.css` changes here, it has to reach every page — the shared
half is byte-identical across the newer pages today, and that property is what
makes a fix carryable at all. `migration.md` tracks what has and has not gone
across.
