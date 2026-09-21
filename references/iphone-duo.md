# iPhone Duo: rules for responsive websites

Apple's material is written for native iOS apps. This file keeps the device facts and layout logic and translates them into rules for websites. Every rule is marked **[Apple]** (stated by Apple's HIG or Tech Talks, as relayed in the sources), **[Repo]** (from `mirzaaghazadeh/iphone-duo-skills`, which distills Apple's material) or **[Heuristic]** (this skill's own web translation, to be tuned and tested).

## Contents
1. Device facts that shape layout
2. Core principle
3. Rules
4. CSS building blocks
5. Test matrix
6. Checklist
7. What is not verified

## 1. Device facts that shape layout

- iPhone Duo is Apple's first foldable iPhone (announced 9 Sept 2026, availability from 23 Oct 2026). Book-style inward fold. [Repo]
- Two displays: a 5.4-inch outer display (compact, used closed) and a 7.6-inch inner display (used open). Both have the **same aspect ratio**, and both are wider and shorter than a traditional iPhone display. [Repo, from Apple's announcement and Tech Talks]
- Size classes: outer portrait = compact width, regular height; outer landscape = compact width, compact height; inner display in any orientation = regular width, regular height. [Repo]
- The inner display does not follow an app's supported orientations. Do not branch layout on orientation or device idiom; branch on available space. [Repo]
- Poses Apple names: closed; open flat; partially folded ("book"), where the fold curves through the center of the inner display and divides it into two usable regions; tabletop/laptop (top region for viewing, bottom region for touch); tent/standing on an edge (glanceable content at the top). [Apple, via Repo and secondary summaries]
- The fold is a *division* reserved region. It is active only when the device is partially folded; when flat it is inactive and has zero width. Camera-related areas are *occlusion* regions. [Apple, Tech Talk on adaptive layouts]
- Keep **interactive elements** out of the curved fold region as much as possible. **Scrollable content does not need to avoid it.** [Apple, Design Tech Talk]
- System controls (toolbars, tab bars, navigation, status bar, Dynamic Island) move to the **side** on several configurations, so safe areas become **asymmetric**. Aligning to horizontal safe-area insets handles the offset; centering on the full display is acceptable only for immersive, non-scrolling content whose interactive elements are not under the side controls. [Apple, Tech Talk relayed in secondary sources]
- Resizability is central: apps must adapt live as the device opens, closes, folds, rotates, and in 50/50 Split View. [Apple]

## 2. Core principle

Do not design "for Duo" as a separate idiom. Design a wider continuum of sizes and replace every fixed assumption (this width, this orientation, this symmetric inset) with a question about the space available right now. [Repo, matching Apple's guidance to lean on size classes, margins and safe areas]

## 3. Rules

**R1. Two layout modes, not five poses.** Build a compact mode (narrow, like the outer display and ordinary phones) and a regular mode (wide, like the inner display, tablets, desktop). Do not build one layout per pose. [Apple]

**R2. Content-driven breakpoints, no device sniffing.** Do not test user agent, orientation or "is this a Duo". Use `min-width`, container queries and intrinsic sizing (`clamp()`, `minmax()`, `auto-fit`). [Repo]

**R3. Wide but short is normal.** Both displays are wider and shorter than classic phones. A hero built as `100vh` with a stacked headline, image and button will overflow on wide-short viewports. Use `min-height: 100svh` with content that can shrink, keep the primary action above the fold at short heights, and never put essential content only in the lower part of a tall block. [Heuristic]

**R4. Asymmetric horizontal safe areas.** Read `env(safe-area-inset-left)` and `env(safe-area-inset-right)` separately and apply them separately. Never write `width - inset * 2` or symmetric padding derived from one inset. Set `viewport-fit=cover` so the insets are provided. [Repo, Apple]

**R5. Fold-aware wide layouts.** In regular mode, treat a vertical center band as a possible fold. Do not put buttons, form fields, nav items, toggles or tap-only controls in that band. Body text, images and background can cross it. Prefer two-column compositions with a deliberate center gutter, or asymmetric compositions whose interactive elements sit left or right of center. [Apple for the principle; Heuristic for the width of the band]

**R6. Fixed bars are optional.** Sticky top/bottom bars use up scarce vertical space on wide-short viewports and may collide with side-moved system controls. Keep navigation in flow or collapsible; when a sticky bar is needed, make it compact at short heights, or switch to a side rail on wide-short viewports. [Heuristic, consistent with Apple's move of bars to the side]

**R7. Live resizing.** The viewport can change while the page is open (fold, unfold, Split View at half the inner display's width). Layout must reflow without reload and without losing scroll position, focus, form input or open menus. Use CSS for layout wherever possible; if JS measures layout, use `ResizeObserver`, not one-time reads at load. Treat Split View as simply a narrower viewport. [Apple for resizability; Heuristic for implementation]

**R8. Continuity across displays.** Same content order and same visual identity in compact and regular mode. Regular mode adds room and parallel context; it does not add different content. [Apple: one continuous experience]

**R9. Touch targets and reach.** In tabletop/laptop poses the lower region is for touch and the upper for viewing; on such viewports keep glanceable content (hero, media, key numbers) high, controls reachable low. Relevant mostly to media, dashboards and tools, low priority for static pages. [Apple poses, Heuristic for web]

**R10. Media and cameras.** For sites with video or images, use responsive `srcset`/`sizes` and `aspect-ratio` so media adapts to the shared display aspect ratio without letterboxing surprises. Sites that capture camera input should not assume one front camera or a fixed orientation. [Repo camera skill, Heuristic]

## 4. CSS building blocks

```html
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
```

```css
:root {
  --gutter: clamp(16px, 4vw, 48px);
  --safe-l: env(safe-area-inset-left, 0px);
  --safe-r: env(safe-area-inset-right, 0px);
  /* Conservative fold band, a tunable heuristic, not an Apple number */
  --fold-band: clamp(24px, 8vw, 96px);
}

.page {
  padding-inline-start: max(var(--gutter), var(--safe-l));
  padding-inline-end:   max(var(--gutter), var(--safe-r));
}

/* Wide layouts: two columns with a center gutter that keeps controls off the fold */
@container (min-width: 44rem) {
  .split { display: grid; grid-template-columns: 1fr var(--fold-band) 1fr; }
  .split > .left  { grid-column: 1; }
  .split > .right { grid-column: 3; }
  /* Body copy or media may span all three columns; controls stay in 1 or 3. */
  .split > .spans { grid-column: 1 / -1; }
}

/* Wide-short viewports: relax sticky chrome and full-height heroes */
@media (min-aspect-ratio: 4/3) and (max-height: 520px) {
  .site-header { position: static; }
  .hero { min-height: auto; }
}

/* Progressive enhancement only: Viewport Segments (supported on some foldable browsers).
   Do not depend on it in Safari on iPhone Duo. */
@media (horizontal-viewport-segments: 2) {
  .split { grid-template-columns: env(viewport-segment-width 0 0) env(viewport-segment-width 1 0); }
}

@media (prefers-reduced-motion: reduce) { * { animation: none !important; transition: none !important; } }
```

Set `container-type: inline-size` on the wrapper that the `@container` rule targets.

## 5. Test matrix

Exact CSS-pixel sizes of both Duo displays were not in the sources read. Do not hardcode them; confirm from Apple's simulator or device documentation when available. Until then test these shapes and a live resize between them:

1. Narrow portrait (ordinary phone width, outer display in portrait).
2. Wide-short (outer display in landscape; regular width but very low height).
3. Wide and moderately tall (inner display, flat).
4. Inner display at half width (Split View, 50/50).
5. Inner display with the center band checked visually: nothing interactive inside the band.
6. Resize 1 to 3 to 4 while the page is open: scroll position, focus and menus preserved.

## 6. Checklist

- [ ] `viewport-fit=cover`; left and right safe insets applied independently
- [ ] No orientation, user-agent or idiom checks; breakpoints from content and containers
- [ ] Hero works at short heights; primary action visible without scrolling on wide-short
- [ ] Nothing interactive in the center band at regular width
- [ ] Sticky bars compact or removable at short heights
- [ ] Live reflow without state loss
- [ ] Same content order in compact and regular mode
- [ ] Media uses `aspect-ratio` and `srcset`
- [ ] Reduced motion honored; focus visible

## 7. What is not verified

- Apple's HIG page (`developer.apple.com/design/human-interface-guidelines/designing-for-iphone-duo`) needs JavaScript and could not be read directly in the session that wrote this skill. Its content was taken from Apple Tech Talks and from summaries of the HIG. Re-read the page and update the rules if it differs.
- Whether Safari on iPhone Duo exposes fold information to web content (viewport segments or similar) is not confirmed in the sources read. R5 is therefore a heuristic that works without it.
- The APIs Apple describes (`reservedRegion`, arrangement views, vertical bars) are native iOS 27.1 APIs and are not available to websites. They are cited only as the source of the layout logic.