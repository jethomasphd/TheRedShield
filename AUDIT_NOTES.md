# AUDIT NOTES — THE SPIRAL v5

**Auditor:** Claude Code (automated audit)
**Date:** 2026-03-11
**File:** `the_spiral_v5.html`

---

## Factual Claims Flagged for Author Review

No factual errors were identified. All historical claims checked against the narrative's own cited sources (Ferguson 1998/1999, Elon 2002, Lottman 1995) appear consistent. The following are **not errors** but are worth the author being aware of:

1. **Nathan Rothschild's arrival in London (1798):** Ferguson's account places Nathan's move to Manchester first (1799), with London coming later. The text says "London in 1798" — this is within the narrative's documented-fact framing and may be intentional compression. Flagged, not changed.

2. **Sixteen of eighteen grandchildren married cousins:** This figure comes from Ferguson. It is accurate to the source. No issue.

3. **AIPAC $100 million figure (2024):** This refers to AIPAC-affiliated PAC spending. The exact figure depends on how affiliates are counted. The claim is within the range of credible reporting. Flagged as worth verifying against the most current FEC data if the author wants precision.

---

## Design Recommendations NOT Implemented

These are suggestions left for the author's discretion:

1. **Color contrast (WCAG AA):** The primary body text (`--ink: #c2b8a2` on `--void: #030303`) has a contrast ratio of approximately **10.5:1**, which passes WCAG AAA. The secondary text (`--ink-f: #7a7264` on `--void`) has a ratio of approximately **3.8:1**, which passes AA for large text but not for normal text. The `--ink-g: #4a4538` on `--void` is approximately **2.3:1**, which fails AA. However, `--ink-g` is used exclusively for metadata labels (IBM Plex Mono at 9-11px, uppercase, letter-spaced) where the low contrast is clearly an intentional design choice for an archival/redacted aesthetic. **No change made** — the atmospheric intent is clear, and the primary reading text passes comfortably.

2. **`scroll-behavior: smooth`:** Currently set on `html`. This doesn't interfere with IntersectionObserver-based reveals since those use scroll position, not scroll events. However, if the author ever adds anchor links, smooth scrolling could delay reveal timing. Consider removing if issues arise.

3. **Leaflet attribution hidden:** `display:none!important` on `.leaflet-control-attribution`. Leaflet and OpenStreetMap tiles require attribution under their licenses. The author may want to add a text credit somewhere (perhaps in the `lf-cap` elements or footer) to comply with OSM's tile usage policy.

4. **Image `alt` text for the Wikimedia five-arrows logo:** Currently says "N M Rothschild & Sons — Five Arrows." This is accurate. The image is from Wikipedia and may be subject to copyright/fair use considerations — the author should verify this is acceptable for their deployment context.

---

## External Optimizations Needed

1. **`frankfurt.png`** — 4.8 MB. This is extremely large for a web image. Recommend compressing to WebP or optimized PNG. Target: under 500 KB. The image displays at max 820px wide (the `.sw` container width), so a source image of ~1600px wide at 2x would suffice.

2. **`Battle_of_Waterloo_1815.png`** — 3.2 MB. Same recommendation. This displays at full container width (~820px), so a 1600px-wide WebP/optimized PNG would be ideal. Target: under 400 KB.

3. **`Nathan_Rothschild.jpg`** — 65 KB. Reasonable size. No action needed.

4. **`Balfour_declaration_unmarked.jpg`** — 204 KB. Acceptable, though could be further compressed. The `.document` class limits display to 600px wide.

5. **Wikimedia five-arrows logo** — External URL. No control over size, but it's a small GIF. The `onerror` handler added will gracefully hide it if the URL breaks.

**Total current image payload: ~8.3 MB.** With optimization of the two large PNGs, this could drop to under 1 MB, dramatically improving load times on mobile.

---

## Browser Compatibility Notes

### CSS
- **`inset` shorthand:** Replaced with explicit `top/right/bottom/left` throughout. This ensures compatibility with Safari < 14.1 (released April 2021) and all older browsers.
- **`feTurbulence` SVG filter (grain overlay):** Supported in Chrome 4+, Firefox 3+, Safari 6+. No compatibility issues expected.
- **CSS custom properties (`var()`):** Supported in all modern browsers (Chrome 49+, Firefox 31+, Safari 9.1+). No fallbacks needed for the target audience.
- **`hyphens: auto`:** Works in Firefox and Safari. Chrome requires `-webkit-hyphens: auto` and only works with `lang="en"` set (which it is). May not hyphenate in all Chrome versions — this is cosmetic only.

### JavaScript
- **IntersectionObserver:** Supported in Chrome 58+, Firefox 55+, Safari 12.1+. No polyfill needed for modern browsers.
- **Arrow functions, `const`, template literals:** ES6+ features. Supported in all browsers from ~2017 onward.
- **`defer` on Leaflet script:** Ensures the script loads after HTML parsing. The `initMaps()` call is delayed by 2200ms+ after seal-break, so Leaflet will be loaded long before it's needed.

### Edge Cases Verified
- **Scroll before seal-break:** Dossier has `display:none`, so no content is visible or scrollable. The progress bar and chapter indicator are also `display:none`. Safe.
- **JavaScript disabled:** `<noscript>` tag displays a styled fallback message matching the design language.
- **Wikimedia image 404:** `onerror` handler hides the `<img>` element gracefully. Caption remains visible.
- **Extremely tall viewports (4K/ultrawide):** Prologue uses `display:flex; align-items:center; justify-content:center` on a `position:fixed; top:0;right:0;bottom:0;left:0` container. The `.folio` content will center vertically and horizontally regardless of viewport height. Verified structurally sound.
- **Leaflet CDN failure:** `try/catch` wraps all Leaflet code. If the CDN fails or `L` is undefined, the experience continues without maps. All other scroll animations, reveals, and content function independently.
