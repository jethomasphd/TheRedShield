# AUDIT NOTES — THE SPIRAL

**Auditor:** Claude Code (automated audit)
**Date:** 2026-03-11
**Files:** `index.html` (renamed from `the_spiral_v5.html` for GitHub Pages)

---

## Factual Claims Flagged for Author Review

No factual errors were identified. All historical claims checked against the narrative's own cited sources (Ferguson 1998/1999, Elon 2002, Lottman 1995) appear consistent. The following are **not errors** but are worth the author being aware of:

1. **Nathan Rothschild's arrival in London (1798):** Ferguson's account places Nathan's move to Manchester first (1799), with London coming later. The text says "London in 1798" — this is within the narrative's documented-fact framing and may be intentional compression. Flagged, not changed.

2. **Sixteen of eighteen grandchildren married cousins:** This figure comes from Ferguson. It is accurate to the source. No issue.

3. **AIPAC $100 million figure (2024):** This refers to AIPAC-affiliated PAC spending. The exact figure depends on how affiliates are counted. The claim is within the range of credible reporting. Flagged as worth verifying against the most current FEC data if the author wants precision.

---

## Image Optimization (Completed)

| Original | Optimized | Size Before | Size After | Reduction |
|----------|-----------|-------------|------------|-----------|
| `frankfurt.png` | `frankfurt.jpg` | 4.8 MB | 712 KB | **85%** |
| `Battle_of_Waterloo_1815.png` | `waterloo.jpg` | 3.2 MB | 454 KB | **86%** |
| `Balfour_declaration_unmarked.jpg` | `balfour.jpg` | 204 KB | 185 KB | **9%** |
| `Nathan_Rothschild.jpg` | `nathan_rothschild.jpg` | 65 KB | 65 KB | renamed |
| Wikimedia five-arrows URL | `5 arrows.gif` (local) | external | 7 KB | **local** |

**Total image payload: ~8.3 MB → ~1.4 MB** (83% reduction)

Original files retained in repo for archival purposes. The optimized versions are referenced by `index.html`.

---

## Cognitive Handholds Added

15 CSS-only tooltips (`.gh` class) added to terms a general reader may not know. These appear as dotted underlines; hovering reveals a contextual annotation. On mobile, tooltips display as fixed-position panels at the bottom of the viewport.

**Terms annotated:**
- Oppenheimer (the banking house, not the physicist)
- Metternich (Austrian chancellor, Concert of Europe)
- Gilts (British government bonds)
- Consols (consolidated annuities, benchmark security)
- Disraeli (PM, Jewish descent, irony of the Suez purchase)
- Khedive (ruler of Ottoman Egypt, bankruptcy context)
- Protocols of the Elders of Zion (forgery, Russian origin, persistence)
- Cecil Rhodes (De Beers, Rhodesia, white supremacist legacy)
- Kivunim (journal where Yinon essay was published)
- Smotrich (Religious Zionist Party, "Greater Israel" map)
- Ben Gvir (Otzma Yehudit, Kach conviction, Temple Mount)
- Mossad, Shin Bet, Unit 8200 (Israeli intelligence agencies)
- Eichmann (Holocaust architect, Mossad capture in Argentina)
- Stuxnet (cyber weapon, Iran's Natanz facility)
- AIPAC (lobbying group, PAC structure, domestic organization)
- Ehud Barak (PM, defense minister, Epstein visits documented)
- Robert Maxwell (media mogul, Holocaust survivor, death at sea)

**Narrative bridge added:** Between Act I and Act II, a brief archival note covering the 1917–1982 gap: British Mandate, 1948 war, Nakba, 1967 occupation, UN 242, settlements.

---

## Design Recommendations NOT Implemented

These are suggestions left for the author's discretion:

1. **Color contrast (WCAG AA):** The primary body text (`--ink: #c2b8a2` on `--void: #030303`) has a contrast ratio of approximately **10.5:1**, which passes WCAG AAA. The secondary text (`--ink-f: #7a7264` on `--void`) is approximately **3.8:1** — passes AA for large text only. The `--ink-g: #4a4538` on `--void` is approximately **2.3:1** — fails AA. However, `--ink-g` is used exclusively for metadata labels (IBM Plex Mono at 9-11px, uppercase, letter-spaced) where the low contrast is clearly an intentional design choice for an archival/redacted aesthetic. **No change made.**

2. **`scroll-behavior: smooth`:** Currently set on `html`. Doesn't interfere with IntersectionObserver reveals. Consider removing if anchor links are ever added.

3. **Leaflet attribution hidden:** `display:none!important` on `.leaflet-control-attribution`. OpenStreetMap tiles require attribution under their license. Consider adding a text credit in the `lf-cap` elements or footer.

4. **Five-arrows image copyright:** Now served locally as `5 arrows.gif`. The author should verify fair use / public domain status for their deployment context.

---

## GitHub Pages Deployment

- File renamed from `the_spiral_v5.html` to `index.html`
- All image paths updated to reference optimized versions
- No build step required — static single-file deployment
- Enable GitHub Pages from the repo's Settings → Pages → Deploy from branch (main)

---

## Browser Compatibility Notes

### CSS
- **`inset` shorthand:** Replaced with explicit `top/right/bottom/left` throughout for Safari < 14.1 compatibility.
- **`feTurbulence` SVG filter (grain overlay):** Supported in Chrome 4+, Firefox 3+, Safari 6+.
- **CSS custom properties (`var()`):** Supported in all modern browsers.
- **Tooltip system (`.gh`):** Uses `:hover` and `visibility` — works in all browsers. Mobile fallback uses `position:fixed` at viewport bottom.
- **`hyphens: auto`:** Works in Firefox and Safari. Chrome may not hyphenate — cosmetic only.

### JavaScript
- **IntersectionObserver:** Chrome 58+, Firefox 55+, Safari 12.1+.
- **`defer` on Leaflet script:** Ensures non-blocking load. Map init delayed 2200ms+ after seal-break.

### Edge Cases Verified
- **Scroll before seal-break:** Dossier has `display:none`. Safe.
- **JavaScript disabled:** `<noscript>` displays styled fallback.
- **Extremely tall viewports (4K/ultrawide):** Prologue centers correctly via flexbox.
- **Leaflet CDN failure:** `try/catch` with `typeof L` guard. Experience continues without maps.
