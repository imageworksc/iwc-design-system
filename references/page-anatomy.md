# Page anatomy and repo conventions

_Part of the ImageWorks Creative design system. Index: [../STYLE-GUIDE.md](../STYLE-GUIDE.md) · Rules: [../CLAUDE.md](../CLAUDE.md) · Code: [../iwc-system.css](../iwc-system.css)_


```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Page Name | ImageWorks Creative</title>
<meta name="description" content="…">
<meta name="theme-color" content="#143c66">
<link rel="canonical" href="https://www.imageworkscreative.com/…">

<meta property="og:type" content="website">
<meta property="og:site_name" content="ImageWorks Creative">
<meta property="og:title" content="…">
<meta property="og:description" content="…">
<meta property="og:url" content="…">
<meta property="og:image" content="…">          <!-- 1200×630, must exist -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="…">
<meta name="twitter:description" content="…">

<script type="application/ld+json">{ "@context": "https://schema.org", "@graph": [ … ] }</script>

<link rel="stylesheet" href="styles.css">
<script src="script.js" defer></script>
</head>
```

The JSON-LD is one `@graph`, typically `Organization` (+ `LocalBusiness`) →
`WebPage` (with `BreadcrumbList`) → `Service`. The Organization node is the
canonical one and carries the real details:

```
ImageWorks Creative · founded 1997
44679 Endicott Dr Suite 300 Unit 580, Ashburn, VA 20147, US
+1 703 928 7309 · sales@imageworkscreative.com
```

If the host site already has sitewide Organization schema, a subpage's
`provider` should be name + url only, so the two do not conflict.

Body order: symbol sheet → `<main id="main">` → hero → bands → `.band--cta`
closing call.


## 11. Repo conventions

```
index.html
styles.css        the carried system, then the page block
script.js         loaded with defer
assets/           images, and only what the page references
.nojekyll         GitHub Pages serves the folder as-is
README.md         scope, the stylesheet split, what to confirm before launch
```

- **GitHub Pages from the repository root**, published at
  `https://imageworksc.github.io/<repo>/`.
- **Prefix the page block.** `bd-` / `bk-` (branding), `mp-` (marketing plans),
  `ai-` (AI web design). The shared half keeps the system's own names.
- **Bump `?v=` on `styles.css` and `script.js` together** when markup and CSS
  change in step. Pages serves both with `max-age=600`; a browser holding one
  while it refetches the other renders the page unstyled.
- Comments explain **why**, not what — the rejected alternative, the measurement
  behind a number, the bug a rule fixes. That is the house style; keep writing
  them.
- The README carries a **"Before this goes live"** section listing every route,
  phone number, meeting link and canonical URL that still needs confirming.


