# Cursor Task: Mobile Optimize & Fix Visibility — **Products** Section

## Objective

Make the **Products** section fully readable and premium on all mobiles (360px–430px first, then up to 768px), fix any "text not visible" issues, and align styling with a dark, premium palette (blues/indigo/purple, minimum white). Keep animations modern but light.

## Files to Edit

* `index.html`
* `styles.css` (or your main stylesheet if different)
* (If there is a `script.js` handling overlays/hero/video, scan for z-index/opacity interactions that might affect the Products section.)

## Brand & Palette Constraints

* Use a **dark base** (near-black/obsidian) with **accents in blue/indigo/purple**.
* Avoid pure white; prefer **near-white** text: `#E6E9FF` to `#C9D1FF`.
* Subtle gradients okay, no hard separators.

## Likely Root Causes (Find & Fix)

1. **Overlay/Z-Index Issue**

   * In the **Products** section container, check if a global hero/video overlay or section overlay is spilling into it.
   * Ensure stacking order: `section background/video (z: 0) < section overlay (z: 1) < products content (z: 2+)`.
   * If there's a global `.overlay` with `position: fixed/absolute` and high `z-index`, **scope it only to the sections that need it** or disable it within `#products` using `positioning` and `isolation: isolate` at the section wrapper.

2. **Low Contrast Text**

   * Verify text color inside **Products**: ensure headings, body text, list items, and buttons use a high-contrast near-white or light indigo.
   * If any `mix-blend-mode`, `opacity < 1`, or `filter: brightness()` is applied to parents, **remove/override** within the products container.

3. **Background Too Busy/Too Dark Under Text**

   * If the background is a video/gradient that crushes text, **add a local, subtle backdrop** for text (soft gradient, 4–6% opacity dark layer) or apply a **layered radial gradient mask** behind cards only.
   * **Do not** blanket-darken the whole screen; use **local scopes** (cards/panels) to maintain premium feel.

4. **Text Hidden by Absolute Elements**

   * Search for absolutely positioned decorative elements overlapping content; constrain within the section, or lower their `z-index`.

## Responsive Typography & Spacing (Mobile-First)

Implement **fluid sizes** and accessible spacing:

* Use `clamp()` for headings and body:

  * H2 (section title): `clamp(24px, 5vw, 34px)`
  * H3 (card titles): `clamp(18px, 4.2vw, 24px)`
  * Body: `clamp(14px, 3.5vw, 18px)`
* Line-height: 1.35–1.55 for readability on mobile.
* Increase letter-spacing slightly on tiny screens if needed (≤390px).
* Ensure **touch targets** (buttons/links) ≥44×44 px.

## Products Section Structure (Keep or Refine)

* Confirm semantic structure: a wrapper like `section#products` → header (H2 + paragraph) → grid of product cards.
* For mobile (≤430px) use **single-column** stack with **16–20px gap**.
* For phablets (431–600px), allow **2 columns** if card width ≥280px; otherwise keep single column.
* At 601–768px, **2 columns** with comfortable gaps.

## Card Styling (Premium Dark)

* Card background: **semi-transparent indigo/blue** on dark, e.g. rgba(30,36,64,0.65) with **backdrop-filter: blur(6–10px)** if supported.
* Border: 1px hairline **indigo/blue** with 12–16px radius (rounded-2xl if Tailwind-like).
* Text colors:

  * Titles: near-white `#E6E9FF`
  * Subheads/hooks: `#B8C1FF` / `#9AA8FF`
  * Body: `#C9D1FF`
* Add **very subtle text-shadow** (e.g., 0 1px 8px rgba(0,0,0,.3)) only if contrast still struggles over videos.
* Icons (if any): set to **light indigo** and ensure 20–28px size on mobile.

## Buttons & Links

* Primary button: **indigo/purple** fill with **near-white** text; hover/active: slightly brighter.
* Focus visible: **outline** with 2px glow (indigo) for accessibility.
* No turquoise unless it complements the palette; prefer indigo/purple.

## Animation (Modern but Light)

* On scroll into view (Products section): **fade + 16px upward translate** for cards, stagger 80–120ms per card.
* Respect `prefers-reduced-motion`: **disable** transforms/opacity transitions for those users.
* Avoid long parallax on mobile.

## Concrete Steps for Cursor

1. **Audit & Scope Overlays**

   * Search for any global `.overlay`, video backdrop, or `position: fixed/absolute` layers that could cover later sections.
   * In `#products`, add `position: relative; isolation: isolate;` to form a new stacking context. Ensure the products content container has higher `z-index` than any background/overlay behind it.
   * If a global overlay is unintentionally spanning, **limit its height to the hero section only** or **unset it for `#products`**.

2. **Fix Colors & Contrast**

   * Define/update CSS variables at `:root` (or section scope) for the dark palette:

     * `--bg-obsidian: #0A0D14;`
     * `--indigo-600: #4F46E5;`
     * `--indigo-500: #6366F1;`
     * `--violet-500: #7C3AED;`
     * `--text-hi: #E6E9FF;`
     * `--text-mid: #C9D1FF;`
     * `--text-subtle: #9AA8FF;`
   * Apply to Products headings/body/links. Remove any low-contrast color or `opacity` on text parents.

3. **Responsive Type using `clamp()`**

   * Replace any hard-coded px font-sizes in the Products section with the `clamp()` values above.
   * Ensure headings don't wrap awkwardly; tune `max-width` of text blocks (e.g., 62–70ch on desktop; 28–34ch on mobile).

4. **Grid & Spacing**

   * Mobile (≤430px): 1-column grid; gap: 16–20px; container side padding: 16–20px.
   * 431–600px: try 2 columns if each card ≥280px (else stay 1 column).
   * 601–768px: 2 columns, larger gap (20–24px).
   * Ensure images/icons scale down correctly (`max-width: 100%; height: auto`).

5. **Local Backdrop for Readability**

   * If background under cards is noisy/dark, give cards a **soft translucent panel** (see Card Styling) rather than a full-section overlay.
   * If the section uses a video background, ensure **the video is below the content layer** and does not apply filters to the content node.

6. **Buttons & CTAs**

   * Enforce a clear primary button style with the palette.
   * Minimum touch size, accessible focus ring, and readable label (`16px+`).

7. **Motion Preferences**

   * Add `@media (prefers-reduced-motion: reduce)` to **remove/shorten** animations/transitions for accessibility.

8. **Accessibility & Testing**

   * Use **Lighthouse** (or DevTools) to check color contrast (AA or better).
   * Manually test on widths: **360, 390, 414, 430, 480, 540, 768**.
   * Verify no text is clipped/overlapped; z-index layering is correct; buttons are tappable.

## Acceptance Criteria

* Text in the **Products** section is **clearly visible** on 360–430px screens with **AA contrast or better**.
* No overlay/video/absolute element sits **above** product text or buttons.
* Typographic sizes are **fluid**; no overflow or cut-off lines in card titles or features.
* Grid gracefully collapses to 1 column on small devices; spacing feels premium and airy (within dark theme).
* Animations are smooth and **respect reduced-motion** settings.
* No paid libraries added; only **HTML/CSS/vanilla JS** edits.

## Notes

* If there is a custom "obsidian" overlay logic used in the hero that extends globally, **contain it** to the hero only.
* If mix-blend modes are used for stylized headlines, **disable** them in the Products section to avoid washout on mobile.

**Make these changes now and confirm with a short diff summary of `index.html` and `styles.css`.**
If you find additional visibility blockers (e.g., `backdrop-filter` performance on low-end devices), implement fallbacks (solid translucent backgrounds on mobile).
