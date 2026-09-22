# Migration backlog

Everything the nine pages owe the system. Nothing here is broken today — these
are places a page and the system disagree, and each one is a small job the next
time that page is opened for another reason.

Fix upstream and carry across ([5](decisions/5-fix-upstream.md)); nothing
in this list is a local patch.

## Pending carries

Changes that live in the kit and have not reached the pages yet.

| Change | Pages | Risk |
| --- | --- | --- |
| `--step-0` floor `15.5px → 16px`, to clear the 16px body minimum | all nine | None visible on desktop — the design width still renders 17px. Only 320–400px phones change. |
| `--step-2` retuned `19–23px → 22–28px` (H3) | all nine | None. The token is declared and no rule reads it. |
| `--step-4` retuned `34–46px → 30–56px` (H1) | all nine | None. Same — declared, unused. |

Deferred deliberately on 2026-09-22: the kit carries them, the live pages do
not. When they go across, they go as one pass so the shared half stays
byte-identical.

## Drift

| Page | Drift | Fix |
| --- | --- | --- |
| `drupal-and-wordpress`, `setup-optimization`, `menu-iwc`, `contact-form-iwc`, `portfolio-iwc` | pull Plus Jakarta Sans from **Google Fonts** instead of embedding it — an external request the newer pages do not make | inline the base64 `@font-face`, drop the `<link>` and both `preconnect`s ([3](decisions/3-font-embedded.md)) |
| `contact-form-iwc` | links the live `imageworks-home/styles.css` off github.io rather than carrying the system | carry `iwc-system.css` in, drop the remote link ([5](decisions/5-fix-upstream.md)) |
| `setup-optimization`, `seo-blogging` | still carry `PLACEHOLDER` canonicals and `og:image` paths | confirm the real routes with the client, then replace |
| `seo-blogging`, `drupal-and-wordpress`, `setup-optimization` | split the CSS as `iwc-foundation` / `iwc-base` + a page file; the newer pages ship one `styles.css` | concatenate into one `styles.css` on the next real edit ([4](decisions/4-three-files.md)) |
| `portfolio-iwc` | the local clone's remote points at a personal fork rather than `imageworksc/portfolio-iwc` | `git remote set-url origin` |
| `ai-web-design` | the local folder is not a git working copy of `imageworksc/ai-web-design` | clone the repo and move the work into it |

## Open questions

- **The 64px hero cap** against the rules' 56px. The weaker of the two type
  exceptions and the first to give up if the rules are enforced strictly — but
  it reflows nine heroes. See [7](decisions/7-hero-h1-floor.md).
- **A real semantic token layer**, so `.band--deep` stops renaming `--navy` to
  white. Low-risk with aliases, but it is a nine-page pass.
  See [8](decisions/8-band-deep-repoints-tokens.md).
