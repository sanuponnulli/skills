# Foundations

Contents: 1. Typography · 2. Color · 3. Layout & spacing · 4. Materials & Liquid Glass · 5. Shape & icons · 6. Motion & feedback · 7. Accessibility · 8. Writing

---

## 1. Typography

**Goals:** legibility first, then hierarchy, then voice. Use as few typefaces as possible (usually one) and build hierarchy from size, weight, and color.

**System typefaces**
- **SF Pro** — system font on iOS, iPadOS, macOS, tvOS, visionOS. Variable font with dynamic optical sizes (no need to pick "Text" vs "Display" in code; the system interpolates).
- **SF Compact** — watchOS (SF Compact Rounded in complications).
- **SF Mono** — code and tabular/monospaced contexts.
- **SF Pro Rounded** — for soft, friendly UI or numerals in widgets/fitness contexts.
- **New York (NY)** — serif companion for editorial/reading experiences.
- Download from developer.apple.com/fonts for mockups; natively, never embed system fonts — request them via font design APIs.

**Default and minimum sizes**

| Platform | Default | Minimum |
|---|---|---|
| iOS, iPadOS | 17 pt | 11 pt |
| macOS | 13 pt | 10 pt |
| tvOS | 29 pt | 23 pt |
| visionOS | 17 pt | 12 pt |
| watchOS | 16 pt | 12 pt |

**Weights:** prefer Regular, Medium, Semibold, Bold. Avoid Ultralight, Thin, Light for interface text, especially at small sizes. Thin custom fonts need larger-than-recommended sizes.

**iOS/iPadOS text styles at the default (Large) Dynamic Type size**

| Style | Weight | Size / Leading (pt) | Emphasized |
|---|---|---|---|
| Large Title | Regular | 34 / 41 | Bold |
| Title 1 | Regular | 28 / 34 | Bold |
| Title 2 | Regular | 22 / 28 | Bold |
| Title 3 | Regular | 20 / 25 | Semibold |
| Headline | Semibold | 17 / 22 | Semibold |
| Body | Regular | 17 / 22 | Semibold |
| Callout | Regular | 16 / 21 | Semibold |
| Subheadline | Regular | 15 / 20 | Semibold |
| Footnote | Regular | 13 / 18 | Semibold |
| Caption 1 | Regular | 12 / 16 | Semibold |
| Caption 2 | Regular | 11 / 13 | Semibold |

Body scales roughly 14 → 23 pt across standard sizes (xSmall → xxxLarge) and up to 53 pt at AX5. Large Title goes 31 → 40 standard, up to 60 at AX5.

**macOS text styles:** Large Title 26/32, Title 1 22/26, Title 2 17/22, Title 3 15/20, Headline 13/16 **Bold**, Body 13/16, Callout 12/15, Subheadline 11/14, Footnote 10/13, Caption 1 10/13, Caption 2 10/13 (Medium). macOS has no Dynamic Type.

**tvOS:** Title 1 76, Title 2 57, Title 3 48, Headline 38, Body 29, Caption 1 25, Caption 2 23 (mostly Medium weight).

**watchOS (Large, 40–42 mm default):** Large Title 36, Title 1 34, Title 2 28, Title 3 19, Headline/Body 16, Caption 1 15, Caption 2 14, Footnote 1 13, Footnote 2 12.

**Tracking (SF Pro, for mockups/web — native apps get this automatically):** small sizes get positive tracking, ~17–20 pt slightly negative, display sizes slightly positive, ≥80 pt zero. Useful points: 11 pt +0.06, 12 pt 0, 13 pt −0.08, 15 pt −0.23, 17 pt −0.43, 20 pt −0.45, 22 pt −0.26, 28 pt +0.38, 34 pt +0.40 (all in points). In CSS, letter-spacing ≈ points ÷ size in em (e.g., 17 px → −0.025em).

**Dynamic Type rules**
- Use text styles so text scales with the person's setting; custom fonts must also scale and honor Bold Text.
- Test at the largest accessibility sizes. Wrap rather than truncate; let labels use as many lines as needed.
- At large sizes, switch horizontal arrangements to stacked (text above secondary items like timestamps/glyphs), and reduce columns.
- Scale meaningful icons with text (SF Symbols do this automatically).
- Keep primary items at the top regardless of size. Not everything must grow — prioritize the content people are reading over chrome like tab titles.
- Leading: loose for long passages/wide columns, tight only for 1–2 lines in constrained rows; never tight for 3+ lines.
- Since the Liquid Glass update, section headers in lists/forms use title-style capitalization rather than ALL CAPS.

---

## 2. Color

**Principles**
- Use color judiciously: to communicate status and interactivity, express brand, and create continuity — not decoration for its own sake.
- **Never rely on color alone** to convey meaning; pair with text, symbols, or shape.
- **Don't use the same color for different meanings**, and use color consistently across the app.
- Pick **one tint/accent color** for interactive elements (buttons, links, selected states). Keep it out of non-interactive text and decoration so tappability stays obvious.
- Prefer **system and semantic (dynamic) colors**; they adapt to light/dark, increased contrast, vibrancy, and glass automatically. Custom colors need light, dark, and increased-contrast variants for each.
- Be sparing with color in controls and navigation on Liquid Glass; color there should signal meaning (e.g., the primary action) — glass takes its tint from content.
- Test colors in light and dark, with Increase Contrast, under different lighting and on different displays, and against glass over varied content.
- Consider cultural meanings of color for your audience.

**System colors** (approximate sRGB reference values; natively always use the named system color — Apple tunes these per OS release)

| Name | Light | Dark |
|---|---|---|
| Red | #FF3B30 | #FF453A |
| Orange | #FF9500 | #FF9F0A |
| Yellow | #FFCC00 | #FFD60A |
| Green | #34C759 | #30D158 |
| Mint | #00C7BE | #63E6E2 |
| Teal | #30B0C7 | #40C8E0 |
| Cyan | #32ADE6 | #64D2FF |
| Blue | #007AFF | #0A84FF |
| Indigo | #5856D6 | #5E5CE6 |
| Purple | #AF52DE | #BF5AF2 |
| Pink | #FF2D55 | #FF375F |
| Brown | #A2845E | #AC8E68 |
| Gray | #8E8E93 | #8E8E93 |
| Gray 2–6 | #AEAEB2 #C7C7CC #D1D1D6 #E5E5EA #F2F2F7 | #636366 #48484A #3A3A3C #2C2C2E #1C1C1E |

Conventional meanings: Blue = default tint/links; Red = destructive & errors; Green = success/on; Orange/Yellow = warning/attention.

**Semantic colors (iOS)** — describe *role*, not hue:
- Labels: `label` (black / white), `secondaryLabel` (≈ rgba(60,60,67,0.6) / rgba(235,235,245,0.6)), `tertiaryLabel` (≈0.3 alpha), `quaternaryLabel` (≈0.18 / 0.16). Use primary for main content, secondary for supporting text, tertiary for placeholder/disabled-ish text.
- Backgrounds (plain): `systemBackground` #FFFFFF / #000000 → `secondarySystemBackground` #F2F2F7 / #1C1C1E → `tertiarySystemBackground` #FFFFFF / #2C2C2E.
- Backgrounds (grouped, e.g., Settings-style): `systemGroupedBackground` #F2F2F7 / #000000 → `secondarySystemGroupedBackground` #FFFFFF / #1C1C1E → `tertiarySystemGroupedBackground` #F2F2F7 / #2C2C2E.
- Fills (translucent, for controls/shapes): `systemFill` … `quaternarySystemFill`.
- `separator` (translucent hairline) and `opaqueSeparator`; `link`; `placeholderText`.
- macOS has its own set (`labelColor`, `controlAccentColor`, `windowBackgroundColor`, `controlBackgroundColor`, `selectedContentBackgroundColor`, etc.) and respects the user's chosen accent color — let the system accent drive interactive color unless brand truly requires otherwise.

**Dark Mode**
- Support it; people expect every app to follow their setting. Don't offer an app-specific toggle unless there's a strong reason.
- Dark palette is *dimmed lights*, not an inversion: dimmer backgrounds, brighter foregrounds. Some colors stay similar.
- Two background sets: **base** (recedes) and **elevated** (popovers, sheets, multitasking in front appear lighter) — system backgrounds handle this automatically. In dark mode, depth comes from lighter surfaces rather than shadows.
- Avoid pure-white large surfaces in dark mode; if you need a white background, slightly dim it so it doesn't glow.
- Use SF Symbols and images with light/dark variants.

---

## 3. Layout & spacing

**Hierarchy through placement**
- Put the most important content and actions where people look first: top and leading edge (respecting right-to-left reversal).
- Group related items using **proximity, alignment, and spacing** first; add separators or backgrounds only when spacing isn't enough. Spacing implies relationship — tighter = more related.
- Keep consistent alignment edges; misaligned items read as unfinished.
- Give content room to breathe; the Liquid Glass-era lists, tables, and forms use larger row heights and padding, and grouped sections use larger corner radii.
- Use progressive disclosure for secondary details — reveal with minimal interaction rather than showing everything.

**Safe areas, margins, guides**
- Lay out with layout margins and safe-area insets, never fixed screen sizes or display-specific assumptions. Safe areas avoid the Dynamic Island, camera housing, rounded corners, Home indicator, and bars.
- Backgrounds and full-bleed imagery may extend edge-to-edge; text and controls stay inside safe areas/margins.
- Readable content width: constrain long text so lines don't become too long on wide screens.
- Avoid placing controls in far corners — hard to reach. On iPhone, the middle and bottom of the screen are most reachable; support swipe-back and swipe actions.
- Avoid full-width buttons that ignore margins (they no longer feel at home; inset them).

**Typical metrics (iOS)**
- Layout margins ≈ 16 pt on compact iPhone widths, ≈ 20 pt on larger widths and iPad. Use an 8-pt-based spacing rhythm (4, 8, 12, 16, 20, 24, 32…).
- Standard list row ≈ 44 pt minimum (taller in the current design); navigation bar ≈ 44 pt + large-title area; tab bar floats above content.
- Touch target ≥ 44×44 pt.

**Adaptivity**
- Support both orientations on iPhone where sensible, all window sizes on iPad and Mac (continuous resizing — design for any width, not presets).
- Think in **size classes**: compact vs regular width/height. Build two well-considered layouts (compact and regular) that expand gracefully; don't design a bespoke layout per device.
- At regular width, show an additional level of hierarchy (e.g., list + detail side by side) rather than stretching a phone layout.
- Prepare for text-size changes, localization (text can grow 30–50%+), and right-to-left mirroring.
- Grids: prefer column counts that divide cleanly (even numbers suit foldables).

---

## 4. Materials & Liquid Glass

**Two layers, two kinds of material**
- **Liquid Glass** — a dynamic material for the *control and navigation layer*: tab bars, toolbars, sidebars, sheets, popovers, menus, floating buttons, slider/toggle knobs during interaction. It bends and concentrates light, adapts its appearance to the content behind it, and morphs fluidly (a button can morph into a menu or popover). Content scrolls and peeks beneath it.
- **Standard materials** (ultra-thin → thick, with vibrancy and blur) — for structure *within the content layer*, e.g., backgrounds behind content groups.

**Rules**
- Don't use Liquid Glass in the content layer. Don't stack glass on glass. Don't overlap or crowd glass elements; use standard spacing.
- Use it sparingly on custom controls — only the most important functional elements. Overuse distracts from content, which glass exists to elevate.
- Two variants: **regular** (adaptive, legible over anything — default) and **clear** (more transparent, for controls over rich media where a dimming layer keeps legibility). Use clear only when the content beneath is visual media and the controls can stay legible.
- Prefer letting the system draw bar/sheet/popover backgrounds; custom backgrounds interfere with glass and the scroll-edge effect.
- Use the **scroll edge effect** under custom bars so content scrolling beneath stays legible.
- Glass respects Reduce Transparency, Increase Contrast, Reduce Motion, and the person's chosen glass appearance — test custom elements under each.
- Group related controls so they share one glass background (e.g., Undo/Redo together; Markup/More together); separate groups with fixed space. Don't mix text and icons inside one shared background.
- Sheets: half-height sheets are inset with larger corner radius and let content peek; at full height they become more opaque to focus the task.
- Background extension: content (hero imagery) can visually extend beneath sidebars/inspectors via a mirrored, blurred extension rather than placing real content under them.

---

## 5. Shape & icons

- **Concentricity**: hardware corner radii inform the UI. Nested shapes share a center: inner radius = outer radius − padding. Controls nestle into rounded window/display corners. Use capsules for buttons in bars, rounded rectangles for cards/sections.
- **SF Symbols**: 6,000+ symbols that match SF text weights and scale with Dynamic Type; rendering modes monochrome, hierarchical, palette, multicolor; variable values and animations. Use them for interface icons rather than custom drawings when one exists.
- Use the **standard symbol for standard actions** (trash = delete, square-and-arrow-up = share, ellipsis = more/overflow, plus = add, magnifying glass = search). Never repurpose a familiar symbol for a different meaning.
- When no symbol clearly conveys an action (e.g., Select, Edit), use a **text label**. Ambiguous icons (pencil, checkmark) are easily misread.
- Bars and menus now favor symbols; in menus, a symbol can introduce a group and text does the rest — don't put symbols on every item if they add noise.
- Every icon-only control needs an accessibility label and a title.
- App icons: layered (foreground/middle/background), solid filled overlapping shapes, no baked-in masking/shadows/blur — the system adds lighting and effects; provide default, dark, clear, and tinted appearances; compose in Icon Composer; keep important elements centered.

---

## 6. Motion & feedback

- Motion should **inform**: show where something came from and went, confirm an action, reflect state. Never gratuitous.
- Prefer fast, physical, interruptible spring animations; let people interrupt or reverse a gesture mid-animation.
- Keep context through transitions (zoom from the tapped item, morph a button into its menu).
- Give **immediate feedback** for every interaction — highlight on press, progress for waits, haptics for meaningful moments (success, warning, error, selection) on iPhone/Watch, used consistently and sparingly.
- Respect **Reduce Motion**: replace large movement, zooms, and parallax with crossfades or none.
- Avoid motion that loops endlessly or flashes; never block interaction while animating.

---

## 7. Accessibility

Treat it as a priority from the start, not an add-on. Test with the actual features turned on.

**Vision**
- Contrast: ≥ 4.5:1 for text at standard sizes (≤ 17 pt), ≥ 3:1 for large or bold text and essential glyphs; aim higher. Check custom colors in light, dark, and Increase Contrast.
- Support Dynamic Type to the largest accessibility sizes, Bold Text, Increase Contrast, Reduce Transparency, Smart Invert (exclude photos/media from inversion), Differentiate Without Color.
- **VoiceOver**: every meaningful element reachable and labeled; labels are short and describe purpose ("Add to cart", not "button plus"); add hints only when the result isn't obvious; declare traits (button, header, selected); group related elements into one logical element; order matches visual order; announce dynamic changes; decorative images hidden from assistive tech.
- Provide alternatives for audio/video (captions, audio descriptions, transcripts).

**Mobility**
- Control sizes: iOS/iPadOS 44×44 pt (minimum 28×28 in dense, non-primary cases), macOS 28×28 pt (min ~20×20), visionOS 60×60 pt, tvOS ~66×66 pt focusable, watchOS 44×44 pt. Leave space between targets (≈ 12 pt around bezeled controls, ~24 pt when unbezeled).
- Every gesture-only action needs a visible alternative (button, menu item). Avoid requiring complex or timed gestures.
- Full keyboard access on iPad/Mac, Voice Control (visible labels must match accessibility labels), Switch Control.

**Hearing & cognition**
- Never convey information only through sound; pair audio cues with visuals/haptics.
- Keep interactions predictable and consistent; avoid time limits (or make them adjustable); minimize auto-playing media and flashing; let people review and undo; use plain language.

---

## 8. Writing

- Be **concise and specific**: the fewest words that make the meaning clear. Cut filler ("Please", "Simply", "In order to").
- Use **plain language**, the person's vocabulary, not internal or technical jargon.
- Buttons are **verbs** describing the outcome: "Save", "Delete Album", "Send". Avoid "OK/Yes/No" when a verb fits. Destructive buttons name what will be destroyed.
- Alerts: a short title that states the situation, optional one-sentence message, and clearly labeled actions. Don't use alerts for routine information.
- Error messages: say what happened, why if useful, and how to fix it — without blame.
- Capitalization: title-style for titles, buttons, menu items, and section headers on Apple platforms; sentence case for longer descriptive text. Be consistent.
- Write for everyone: inclusive, gender-neutral, culturally neutral; avoid idioms that don't translate.
- Empty states explain what will appear and how to start.
