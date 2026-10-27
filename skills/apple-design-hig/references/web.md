# Applying Apple's design philosophy on the web (React / HTML / CSS)

The HIG is written for native apps, but its principles transfer directly. The goal on the web is a site that *feels* considered, calm, and content-first the way Apple's apps do — not a fake iOS screen. Respect web conventions (links, scrolling, back button, URLs, keyboard) the same way the HIG asks you to respect platform conventions.

**Don'ts up front**
- Don't self-host or embed SF Pro/New York font files on a website — Apple's font license limits them to designing for Apple platforms. Use the system font stack below (renders SF on Apple devices, a good native font elsewhere).
- Don't use Apple logos, product imagery, or branding, and don't imitate Apple's own website or a real Apple app UI as if it were Apple's.
- Don't fake an iOS status bar, home indicator, or notch in a web page meant for real use.

**Two web surfaces — pick one per page (see SKILL.md step 1)**
- **App surface** (web apps, dashboards, tools): everything in this file except "Marketing pages". Compact, dense-enough, standard components, no hero sections.
- **Marketing surface** (landing, product, portfolio pages): the tokens below plus the "Marketing pages" section at the end.

---

## Typography

```css
:root {
  --font-sans: -apple-system, BlinkMacSystemFont, "SF Pro Text", "SF Pro Display",
               "Helvetica Neue", "Segoe UI", Roboto, Inter, system-ui, sans-serif;
  --font-rounded: ui-rounded, "SF Pro Rounded", var(--font-sans);
  --font-serif: ui-serif, "New York", Georgia, serif;
  --font-mono: ui-monospace, "SF Mono", SFMono-Regular, Menlo, Consolas, monospace;
}
body { font-family: var(--font-sans); font-size: 17px; line-height: 1.29; -webkit-font-smoothing: antialiased; }
```

Text-style scale (iOS default size, px ≈ pt), with tracking:

| Token | Size / line-height | Weight | letter-spacing |
|---|---|---|---|
| `--text-large-title` | 34 / 41 | 700 for page titles (400 regular style) | 0.012em |
| `--text-title1` | 28 / 34 | 400–700 | 0.013em |
| `--text-title2` | 22 / 28 | 400–700 | −0.012em |
| `--text-title3` | 20 / 25 | 400–600 | −0.022em |
| `--text-headline` | 17 / 22 | 600 | −0.025em |
| `--text-body` | 17 / 22 | 400 | −0.025em |
| `--text-callout` | 16 / 21 | 400 | −0.02em |
| `--text-subheadline` | 15 / 20 | 400 | −0.015em |
| `--text-footnote` | 13 / 18 | 400 | −0.006em |
| `--text-caption1` | 12 / 16 | 400 | 0 |
| `--text-caption2` | 11 / 13 | 400 | 0.006em |

- Body never below 16px on the web (avoids iOS Safari zoom on inputs); nothing below 11px.
- For desktop-dense app UIs (macOS-like), body 13–14px is acceptable; marketing/reading pages can go 17–21px.
- Use `rem` so browser text-size settings scale text (the web's Dynamic Type). Test at 200% zoom; layouts must reflow, not truncate.
- Avoid font-weight 100–300 for UI text.
- Use `font-variant-numeric: tabular-nums` for numbers that update or align in columns.
- Limit line length to ~60–80 characters for reading.

## Color tokens (light/dark, semantic)

```css
:root {
  color-scheme: light dark;
  --tint: #007AFF;              /* one accent, interactive only */
  --label: #000000;
  --label-secondary: rgba(60,60,67,.60);
  --label-tertiary: rgba(60,60,67,.30);
  --label-quaternary: rgba(60,60,67,.18);
  --bg: #FFFFFF;  --bg-2: #F2F2F7;  --bg-3: #FFFFFF;
  --bg-grouped: #F2F2F7;  --bg-grouped-2: #FFFFFF;  --bg-grouped-3: #F2F2F7;
  --fill: rgba(120,120,128,.20);  --fill-2: rgba(120,120,128,.16);
  --fill-3: rgba(118,118,128,.12);  --fill-4: rgba(116,116,128,.08);
  --separator: rgba(60,60,67,.29);
  --red: #FF3B30; --orange: #FF9500; --yellow: #FFCC00; --green: #34C759;
  --teal: #30B0C7; --blue: #007AFF; --indigo: #5856D6; --purple: #AF52DE; --pink: #FF2D55;
}
@media (prefers-color-scheme: dark) {
  :root {
    --tint: #0A84FF;
    --label: #FFFFFF;
    --label-secondary: rgba(235,235,245,.60);
    --label-tertiary: rgba(235,235,245,.30);
    --label-quaternary: rgba(235,235,245,.16);
    --bg: #000000;  --bg-2: #1C1C1E;  --bg-3: #2C2C2E;
    --bg-grouped: #000000;  --bg-grouped-2: #1C1C1E;  --bg-grouped-3: #2C2C2E;
    --fill: rgba(120,120,128,.36);  --fill-2: rgba(120,120,128,.32);
    --fill-3: rgba(118,118,128,.24);  --fill-4: rgba(118,118,128,.18);
    --separator: rgba(84,84,88,.65);
    --red: #FF453A; --orange: #FF9F0A; --yellow: #FFD60A; --green: #30D158;
    --teal: #40C8E0; --blue: #0A84FF; --indigo: #5E5CE6; --purple: #BF5AF2; --pink: #FF375F;
  }
}
@media (prefers-contrast: more) { /* darken tint/labels in light, brighten in dark */ }
```

- Swap `--tint` for the brand color if needed, but keep it the *only* interactive accent and verify 4.5:1 against its backgrounds in both modes.
- Elevated surfaces in dark mode (modals, popovers) use `--bg-2`/`--bg-3`, not shadows.
- Check contrast of secondary labels over grouped backgrounds; translucent label colors can fail on tinted surfaces.

## Layout & spacing

- 8-px rhythm: 4, 8, 12, 16, 20, 24, 32, 44, 64. Side margins 16px on phones, 20px on tablets, wider containers centered with max-width on desktop.
- `padding: env(safe-area-inset-*)` with `viewport-fit=cover` for full-bleed mobile web apps; never put controls under the home indicator area.
- Inset grouped lists: card-like sections with radius 10–26px (larger in the current design), 16px horizontal padding, rows ≥ 44px tall, hairline separators inset from the leading edge (`1px` at 0.5 scale or `0.5px` on high-DPI) using `--separator`.
- Concentric radii: `inner-radius = outer-radius − padding`.
- Responsive breakpoints map to size classes: compact (< ~600px) single column + bottom tab bar; regular (≥ ~768px) sidebar or split view. Don't just scale a phone layout up.
- Hit areas ≥ 44×44px (pad icon buttons); ≥ 8px between adjacent targets.

## Liquid Glass approximation (control layer only)

```css
.glass {
  background: color-mix(in srgb, var(--bg) 60%, transparent);
  backdrop-filter: blur(20px) saturate(180%);
  -webkit-backdrop-filter: blur(20px) saturate(180%);
  border: 0.5px solid color-mix(in srgb, var(--label) 12%, transparent);
  box-shadow: 0 8px 24px rgba(0,0,0,.12), inset 0 1px 0 rgba(255,255,255,.35);
  border-radius: 999px; /* capsule for bars/buttons */
}
@media (prefers-reduced-transparency: reduce) {
  .glass { background: var(--bg-2); backdrop-filter: none; -webkit-backdrop-filter: none; }
}
```

- Use for floating tab bars, toolbars, sticky headers, floating action groups, popovers — never for cards in the content.
- One glass layer at a time; never glass inside glass.
- Add a scroll-edge fade (gradient mask) behind sticky glass bars so text underneath doesn't fight the controls.
- Always provide a solid fallback (`@supports not (backdrop-filter: blur(1px))`).

## Components translated

- **Bottom tab bar (mobile)**: 2–5 destinations, symbol + short label, fixed/floating at bottom within safe area, active = tint; real links (`<a>`/router links) with `aria-current="page"`.
- **Sidebar (desktop)**: grouped sections, collapsible, keyboard navigable.
- **Navigation header**: large title that collapses to an inline sticky title on scroll; back link uses previous page name.
- **Buttons**: one filled primary per view (`background: var(--tint); color: #fff`), secondary tinted fill (`--fill-3` with tint text), plain text tertiary; capsule or 12px radius; destructive in `--red`. Use `<button>`, not clickable divs.
- **Sheets/modals**: `<dialog>` with focus trap, Escape to close, Cancel/Done in header, bottom sheet on mobile with drag handle, centered on desktop. Confirm before discarding edits.
- **Segmented control**: `role="radiogroup"` or tabs pattern; sliding selected pill.
- **Switches**: `<input type="checkbox" role="switch">` with visible label; immediate effect.
- **Search**: field with magnifying-glass icon, "Search X" placeholder, instant results, recent searches, clear button.
- **Toasts/feedback**: subtle, non-blocking, `aria-live="polite"`; errors inline near fields.
- **Icons**: use a consistent line-weight icon set matched to text weight (e.g., stroke ~1.5–2px at 20–24px). SF Symbols may be used only in apps for Apple platforms per their license — on the web use an open icon set with a similar style.

## Motion

```css
:root { --spring: cubic-bezier(.2,.8,.2,1); --dur-fast: 150ms; --dur: 250ms; --dur-slow: 400ms; }
@media (prefers-reduced-motion: reduce) { *, *::before, *::after { animation-duration: .01ms !important; transition-duration: .01ms !important; scroll-behavior: auto !important; } }
```
- Press feedback: `transform: scale(.97)` + opacity on `:active`, instant.
- Transitions show spatial relationships (sheet slides up, detail zooms from card); keep them short and interruptible. Consider the View Transitions API for list→detail continuity.

## Accessibility on the web

- Semantic HTML first; ARIA only to fill gaps. Every icon-only button has `aria-label`.
- Visible `:focus-visible` rings (2px tint outline with offset); full keyboard operation; logical tab order; skip link.
- Contrast ≥ 4.5:1 text, ≥ 3:1 large text and UI components (WCAG AA — matches the HIG).
- Honor `prefers-color-scheme`, `prefers-reduced-motion`, `prefers-reduced-transparency`, `prefers-contrast`, and browser zoom/text size.
- Don't disable pinch-zoom. Labels on all inputs; `autocomplete` attributes for AutoFill; correct `inputmode`/`type` for the right mobile keyboard.

## Tailwind quick mapping

`font-sans` → the stack above; text sizes via `text-[17px] leading-[22px] tracking-[-0.025em]`; colors via CSS variables (`bg-[var(--bg-grouped)]`); `rounded-full` for bar buttons, `rounded-2xl`/`rounded-3xl` for sections; `backdrop-blur-xl backdrop-saturate-150 bg-white/60 dark:bg-black/40` for glass; `min-h-11 min-w-11` (44px) for targets; `motion-reduce:transition-none`.

---

## Marketing pages (landing, product, portfolio)

Expressive, but the principles still rule: one idea per section, the product or work is the hero, and nothing moves without a reason.

- **Structure**: a sequence of full-width sections, each with one message — a short headline, one supporting sentence, one visual, one call to action at most. Alternate light and dark sections to pace the story.
- **Type**: large display headlines (48–96px on desktop, 34–48px on mobile, weight 600–700, slightly negative tracking ≈ −0.02em to −0.015em at large sizes), short line lengths, body 17–21px. Use `clamp()` so type scales fluidly.
- **Imagery**: high-quality product/work imagery on plain backgrounds; let it run large; no stock-photo clutter or decorative gradients competing with it.
- **Feature grids ("bento")**: tiles of varied size in a consistent grid with equal gaps (16–24px) and a shared corner radius (≈ 18–28px); each tile one feature, one headline, one visual. Don't fill tiles with paragraphs.
- **Calls to action**: one primary capsule button per section in the accent color, plus at most one secondary text link ("Learn more ›").
- **Motion**: fade/slide-in on scroll with `IntersectionObserver` or CSS `animation-timeline: view()`; subtle parallax or scale at most. Never hijack scrolling speed or direction, never block reading until an animation finishes, and turn it all off under `prefers-reduced-motion`.
- **Navigation**: slim sticky top bar (≈ 44–52px) with glass background, a few text links, and the primary action; collapses to a menu button on mobile (a menu is fine on the web marketing surface).
- **Performance is craft**: lazy-load media, serve modern image formats at the right size, avoid layout shift, keep the page fast on mobile.
- **Accessibility**: same rules as everywhere — contrast over images (add a scrim), alt text, captions on video, pause controls on autoplaying media, keyboard-reachable everything.
