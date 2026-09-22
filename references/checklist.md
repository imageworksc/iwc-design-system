# Before a page goes live

_Part of the ImageWorks Creative design system. Index: [../STYLE-GUIDE.md](../STYLE-GUIDE.md) · Rules: [../CLAUDE.md](../CLAUDE.md) · Code: [../iwc-system.css](../iwc-system.css)_


- [ ] Canonical, `og:url` and JSON-LD `@id` point at the real production route
- [ ] `og:image` exists at that URL, 1200×630 — no placeholder path
- [ ] No `PLACEHOLDER` string anywhere in the file
- [ ] Every CTA points at the real destination (`/contact`, the HubSpot meeting
      link, `sms:7039287309`) and each has been clicked
- [ ] The font is embedded; the page makes no external request
- [ ] No `<style>` block, no `style=`, no inline `<script>` body
- [ ] 320px → 5120px with no horizontal overflow, every disclosure open
- [ ] Tab through it: the ring shows on everything, nothing is trapped
- [ ] Reduced motion on: nothing snapped to a wrong end frame, nothing hidden
- [ ] The system half of `styles.css` is identical to upstream
- [ ] `?v=` bumped


