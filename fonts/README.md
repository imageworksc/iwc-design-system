# Plus Jakarta Sans

`plus-jakarta-sans-latin.woff2` — latin subset, variable, weights 300–800.

Copyright 2020 The Plus Jakarta Sans Project Authors
(<https://github.com/tokotype/PlusJakartaSans>), licensed under the SIL Open
Font License 1.1. The full licence is in [OFL.txt](OFL.txt) and must travel
with the font wherever it goes, including when it is embedded as base64 in a
stylesheet.

## Inlining it

The system embeds the font rather than linking it, so a page makes no external
network request ([decisions/0003](../decisions/0003-font-embedded.md)).
`iwc-system.css` ships with a placeholder; before a page goes live:

```bash
base64 -w0 fonts/plus-jakarta-sans-latin.woff2
```

Paste the result over `PASTE_PAYLOAD_HERE` in the `@font-face` block.
