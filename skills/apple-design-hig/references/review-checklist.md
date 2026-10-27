# Review checklist & report format

Use for critiques, audits, and "how can I improve this UI/UX" requests — screenshots, Figma descriptions, live sites, or code.

## Process

1. **Understand before judging.** What is this screen/app for? Who uses it, on which device, in what context? What's the primary task? If you can't tell, say what you assumed.
2. **Walk the primary task** as the person would. Note friction, confusion, dead ends, missing feedback.
3. **Check principles, then foundations, then components, then platform fit** using the lists below.
4. **Check states**: empty, loading, error, offline, first run, long text/localization, largest text size, dark mode, reduced motion/transparency.
5. **Rank by impact on people** (not by ease of spotting). Merge duplicates.
6. **Give a concrete fix** for each issue — specific values, components, or wording — and cite the HIG area.
7. For code reviews, point to the exact file/line and show the corrected snippet.

## Severity

- **Critical** — blocks or misleads people, excludes people (accessibility failure), risks data loss or privacy harm, or breaks platform expectations badly (e.g., no way back, destructive action without undo or confirmation, contrast far below 4.5:1, touch targets far below 44 pt, permission prompt at launch).
- **Major** — noticeable friction or confusion; inconsistent behavior; weak hierarchy; non-standard components where standard ones fit; broken in dark mode or large text.
- **Minor** — polish: alignment, spacing rhythm, wording, icon consistency, small craft details.

## What to check

**Principles**
- Purpose: is the primary purpose obvious within seconds? Are there features/elements that don't serve it?
- Agency: can people get straight to content? Forced flows/modes? Undo available? Easy escape from guided flows?
- Responsibility: permissions timed and explained? Minimal data? Dark patterns (confirm-shaming, hidden costs, pre-checked consent, hard-to-cancel)? Harmful AI output safeguards?
- Familiarity: standard icons/metaphors used with standard meaning? Same-looking things behave the same? Consistent placement? Clear feedback?
- Flexibility: works across sizes/orientations/inputs? Accessibility? Localization/RTL? Personalization where helpful?
- Simplicity: every element earns its place? Plain concise language? Strong hierarchy — is the most important thing the most prominent? Anything buried in a catch-all menu?
- Craft: alignment, spacing rhythm, type scale, icon consistency, smooth responsive animation, performance, no layout jank?
- Delight: is there a coherent emotional tone? Is delight decoration that gets in the way?

**Foundations**
- Type: system/limited typefaces; sizes ≥ platform minimums; no thin weights; clear scale; Dynamic Type/zoom support; no truncation of important text.
- Color: one interactive accent; no color-only meaning; semantic/adaptive colors; dark mode; contrast ≥ 4.5:1 / 3:1.
- Layout: safe areas & margins; grouping via spacing; alignment; top/leading priority; reachable controls; adapts at compact/regular widths.
- Materials: glass only on control layer; no glass-on-glass; legibility over content; custom bar backgrounds removed.
- Shape/icons: concentric radii; consistent icon style/weight; icon-only controls labeled.
- Motion: purposeful, quick, interruptible; Reduce Motion respected.
- Accessibility: 44 pt targets; screen reader labels/order/traits; keyboard/focus; captions; no info by sound only.
- Writing: verb buttons; specific alerts/errors; title-style caps where expected; no jargon.

**Components & patterns**
- Navigation model appropriate (tab bar vs sidebar vs stack); no hamburger for primary nav on Apple platforms; tabs not used as actions; tabs never hidden/disabled.
- Toolbars grouped sensibly; standard symbols; overflow via system menu.
- Button hierarchy (≤ 2 prominent); destructive styled and separated.
- Modality used sparingly and appropriately; alerts only for critical info.
- Search placement and behavior per platform.
- Lists/forms: grouping, labels, validation, swipe actions with matching context menu.
- Loading/empty/error states present and helpful.
- Onboarding skippable and short; sign-in deferred.

**Platform fit**: see `platforms.md` for the target platform (e.g., Mac menu bar & shortcuts, iPad resizable windows, iPhone Duo vertical controls and fold avoidance, visionOS 60 pt targets).

## Report format

```
## Summary
<2–3 sentences: what the UI is for, overall verdict, the one change that would help most>

## What's working
- <brief bullets, 2–4 max>

## Issues
### Critical
1. **<Issue title>** — <what's wrong and who it affects>.
   *Principle / reference:* <e.g., Agency; foundations.md › Accessibility>
   *Fix:* <specific change — values, component, wording, or code>

### Major
...

### Minor
...

## Suggested next step
<one concrete next action, e.g., a revised layout sketch or code patch>
```

Keep it proportionate: a single screenshot gets a focused review (≈5–10 issues), not an exhaustive essay. If asked to fix, implement the changes rather than only listing them.
