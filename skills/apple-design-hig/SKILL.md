---
name: apple-design-hig
description: "Apple's 2026 Human Interface Guidelines (Liquid Glass, SF type, Dynamic Type, color, layout, accessibility) for designing, building, polishing and reviewing UI on iOS, iPadOS, macOS, watchOS, tvOS, visionOS and the web. Use it for any task about how an app or page looks, reads or flows, even small ones you could do from memory, since the HIG and APIs changed in 2025–26: making a SwiftUI, UIKit, React Native, Flutter, Electron or Tauri screen feel native, iOS-style or Mac-like; cleaning up a screen with hard-coded colors, fixed font sizes or broken dark mode; adding Liquid Glass; polishing a tab bar, sheet, toolbar, sidebar or settings screen; building an Apple-quality landing or product page; and any UX critique, audit or feedback on a screen, form, flow or dashboard — including one only described in words, with no Apple mention. Not for non-visual work (crashes, builds, tests, CI, signing, release notes, App Store text), Android Material UI, or a CSS bug with no design question."
---

# Apple Design

Design and review interfaces the way Apple's Human Interface Guidelines intend: purposeful, human, and at home on the platform. This skill covers two jobs — **building** UI and **reviewing** UI — on any Apple platform and on the web.

Everything here is distilled (in our own words) from Apple's official HIG, its technology overviews, and WWDC design sessions. When a detail matters and might have changed, check the live source listed in `references/sources.md`.

## The philosophy in one breath

Apple defines design as *making something with intention*. Every feature costs people time, attention, and trust, so choosing what **not** to build is as important as what you build. The HIG (re-stated June 2026) organizes this into eight principles. Use them as tools for weighing trade-offs, not as a formula — leaning into one can pull against another, and judgment decides.

| Principle | One-line test | What it looks like in practice |
|---|---|---|
| **Purpose** — make something meaningful | Does this element serve why people came? | Focus on the few features that matter and make them great; don't clone existing solutions — find what sets yours apart. |
| **Agency** — let people do things their way | Can people act freely and undo mistakes? | Get people straight to the task; no forced flows (guided flows are skippable); undo everywhere; confirm only truly destructive actions. |
| **Responsibility** — act in people's best interest | Would people trust this if they saw everything it does? | Ask for permissions in context with a clear reason; collect only what's needed; anticipate misuse and harm (especially AI output); add safeguards or drop the feature. |
| **Familiarity** — build on what people know | Will people predict what happens? | Use established metaphors and system icons with their standard meaning; things that look the same behave the same; consistent placement; clear feedback for every action. |
| **Flexibility** — adapt to diverse contexts | Does it work for every size, input, ability, and language? | Accessibility from day one; resizable layouts; support touch, keyboard, pointer, voice; give each platform equal care; allow personalization where no single layout fits all. |
| **Simplicity** — be clear and direct | Does every element earn its place? | Simple ≠ minimal (burying features in one menu is not simple). Plain, concise words; strong hierarchy so the most important thing is the most obvious; sometimes add context to make things clearer. |
| **Craft** — care about every detail | Does it feel solid, fast, and finished? | Great type, adaptive color, crisp icons, fluid responsive animation, instant feedback, no jank or misalignment; prototype and iterate; keep it current after shipping. |
| **Delight** — make it human | What should people *feel*? | Pick the emotion (calm, energized, confident) and reinforce it; create small defining moments; delight is never decoration that gets in the way — it's the sum of all the above done well. |

The older HIG triad — **clarity, deference, depth** — still describes the visual stance well: content first, UI that steps back, and layering that explains hierarchy. Today that layering is expressed through **Liquid Glass**: controls and navigation float on a distinct glass layer above the content layer.

## How to use this skill

1. **Classify the surface before anything else.** Building or reviewing? Then decide which surface it is, because it decides how much visual drama is allowed:
   - **App / utility surface** — native apps, web apps, dashboards, admin tools, desktop apps (Electron/Tauri). Full HIG restraint: content first, standard components, compact chrome, no scroll-driven theatrics, no oversized hero sections. Load `foundations.md` + `components-patterns.md` (+ `platforms.md` for a native target, `web.md` for browser, `cross-platform.md` for Flutter/React Native/Electron/Tauri/SwiftUI glass APIs).
   - **Marketing / landing surface** — product pages, portfolios, launch pages. Expressive is allowed (large display type, product-first imagery, scroll reveals) but still governed by the principles. Load `foundations.md` + `web.md` (its "Marketing pages" section).
   - Never mix them: no hero sections or scroll-jacking inside an app; no tab bars or modal sheets imitating iOS on a desktop marketing page. If unclear, ask once or assume from context and say which you assumed.
2. **Load only the sections the task needs.** The references total about 20k tokens, and reading them whole is the main cost of this skill, while most tasks need two or three sections. The Quick rules below already cover the most common checks, so start from the table, read those sections (each file is organized by `##` headings; `grep -n '^## ' <file>` gives the line ranges, then read just that range), and open more only when a specific question comes up.

   | Task | Read |
   |---|---|
   | Review / critique (any surface) | `review-checklist.md` in full (required — it holds the report format), plus only the sections matching the issues you find |
   | Web app or page (HTML/CSS/React) | `web.md` › Typography, Color tokens, Liquid Glass approximation, Components translated, Motion, Accessibility on the web; add › Marketing pages for landing pages |
   | SwiftUI / UIKit / AppKit screen | `foundations.md` › Typography and › Color; `components-patterns.md` › the section for the component you're building; `cross-platform.md` › 1 only when using Liquid Glass APIs |
   | React Native, Flutter, Electron, Tauri | `cross-platform.md` › that framework's section; `foundations.md` › Typography |
   | A specific platform (watchOS, tvOS, visionOS, macOS, iPad, foldable) | `platforms.md` › that platform's section |
   | Choosing navigation or a flow (onboarding, permissions, undo, modality) | `components-patterns.md` › that section |

   Section contents: `foundations.md` — Typography (exact Dynamic Type scale), Color (system + semantic, dark mode), Layout & spacing, Materials & Liquid Glass, Shape & icons, Motion, Accessibility, Writing. `components-patterns.md` — navigation, bars, buttons, menus, modality, search, lists/forms, feedback, onboarding/permissions, undo, AI features. `sources.md` — official URLs to verify a detail that may have changed.
3. **Do the work** using the workflow below.

## Building UI

Work from the inside out — content and purpose first, chrome last.

1. **State the purpose.** In one sentence, what is this screen for, and what is the single most important thing on it? Everything else is ranked against that.
2. **Structure the hierarchy.** Decide primary, secondary, and tertiary content. Put the most important content top/leading; group related items with proximity and alignment rather than borders and boxes.
3. **Pick standard components before inventing.** Tab bar or sidebar for top-level navigation, navigation stack for drill-down, toolbar for actions, sheet for focused sub-tasks, menu for secondary actions. Natively, use the system component (it gets Liquid Glass, accessibility, Dynamic Type, and dark mode for free). Only build custom when a system component genuinely can't do the job — and then match its behavior.
4. **Separate layers.** Content layer (lists, media, documents) uses solid backgrounds / standard materials. Control layer (bars, floating buttons, sheets) uses Liquid Glass. Never put glass in the content layer, never stack glass on glass.
5. **Apply the foundations.** System font and the text-style scale; semantic colors that adapt to light/dark/increased contrast; one accent (tint) color used *only* for interactive elements; 44 pt minimum touch targets; layout margins and safe areas; concentric corner radii.
6. **Design every state.** Empty, loading, error, partial, offline, first-run, and largest Dynamic Type size. Undo for destructive actions. Feedback for every tap.
7. **Write the words.** Short, plain, specific labels; verbs on buttons ("Save", "Delete Photo"), not "OK"/"Yes"; title-style capitalization for section headers and titles; no jargon.
8. **Verification gate (do not skip).** Before presenting, check the output against every item in "Quick rules" below and fix failures — reading your own code against the list catches nearly everything. For a full screen, app, or anything the user will ship, also run the "What to check" list in `references/review-checklist.md`. If you render web output to look at it, one screenshot in light and one in dark at phone width is enough; screenshots of every state cost minutes and many tokens while rarely surfacing a new problem. In your reply, note any rule you deliberately broke and why.

When presenting a design, briefly explain the key decisions in terms of the principles (e.g., "Delete lives in a context menu with undo rather than a confirmation alert — Agency"). Don't lecture; one line per major decision is plenty.

## Reviewing UI

**Always read `references/review-checklist.md` before writing any review** — even when the foundations feel sufficient — and use its report format exactly. Cite each issue as `file › section` (e.g., `foundations.md › Accessibility`) so the user can trace it. In short: understand the purpose first, evaluate against the eight principles and the foundations, rank issues by impact on people (not by how easy they are to spot), cite the HIG area for each, and give a concrete fix for each. Lead with what most hurts the experience. Acknowledge what's working — briefly.

## Quick rules (the ones most often broken)

- **Touch targets** ≥ 44×44 pt on iOS/iPadOS (60 pt on visionOS); pad small icons to reach it.
- **Text**: iOS body 17 pt default, nothing below 11 pt; macOS body 13 pt, minimum 10 pt. Avoid Ultralight/Thin/Light weights for UI text. Support Dynamic Type; layouts must survive the largest accessibility sizes (stack instead of truncate).
- **Contrast**: at least 4.5:1 for normal text, 3:1 for large/bold text and essential UI glyphs. Check in both light and dark, and over glass.
- **Color is never the only signal** — pair with a symbol, label, or shape.
- **One accent color**, reserved for interactivity. Red only for destructive/error. Don't reuse a color for two meanings.
- **Liquid Glass sparingly** — only on the control/navigation layer, only for the most important functional elements, never glass-on-glass, never in content.
- **Respect safe areas and layout margins**; backgrounds may run edge-to-edge, controls and text may not. Avoid controls in hard-to-reach corners.
- **Concentric corners**: a nested element's radius = parent radius − inset.
- **No permission prompts at launch**; ask at the moment of need, with a reason.
- **Undo over confirmation** for most actions; confirm only destructive, hard-to-reverse ones, and name the action in the confirm button.
- **Don't hide or disable tab bar items**; don't use a hamburger menu for primary navigation on Apple platforms.
- **Every icon-only control has an accessibility label** (and a title, used in overflow menus).
- **Respect Reduce Motion, Reduce Transparency, Increase Contrast, Bold Text, and Dark Mode.**
- **Preserve context** across sizes and devices: keep controls in consistent, predictable positions; animate transitions so people don't lose their place.

## Native code notes

Prefer SwiftUI with system components; they adopt the current design automatically. Use text styles (`.font(.body)`, `.headline`) not fixed sizes — this includes glyphs inside custom controls like a checkmark on a color swatch (use `.font(.caption.weight(.bold))` or `.imageScale(.small)`, or `@ScaledMetric` for a size that must track Dynamic Type), since a fixed size there is the most common slip; semantic colors (`.primary`, `.secondary`, `Color(.systemBackground)`) not hex; SF Symbols with `Label` (title + symbol); `.glassEffect()` / `.buttonStyle(.glass)` / `.glassProminent` only for custom controls that truly need it, grouped in a `GlassEffectContainer`; `NavigationSplitView`, `TabView` (`.sidebarAdaptable`, `Tab(role: .search)`), `.toolbar` with `ToolbarItemGroup`; `ConcentricRectangle` for nested shapes; `.inspector` for inspectors. Don't paint custom backgrounds on bars, toolbars, sheets, or popovers — let the system draw them.
