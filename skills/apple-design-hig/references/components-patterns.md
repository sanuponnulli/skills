# Components & Patterns

Contents: 1. Choosing navigation · 2. Bars & toolbars · 3. Buttons & controls · 4. Menus · 5. Modality (sheets, alerts, popovers) · 6. Search · 7. Lists, collections, forms · 8. Feedback, loading, status · 9. Onboarding, permissions, accounts · 10. Undo, editing, data entry · 11. AI features

Rule of thumb: **use the system component**. Natively it gives you Liquid Glass, accessibility, Dynamic Type, dark mode, and future design updates for free. On the web, recreate its *behavior and hierarchy*, not a pixel copy.

---

## 1. Choosing navigation

| Need | Use | Avoid |
|---|---|---|
| 2–5 peer top-level sections on iPhone | **Tab bar** | Hamburger/drawer menus |
| Many sections or deep hierarchy on iPad/Mac | **Sidebar** (tab bar can adapt into sidebar) | Tabs for 8+ items |
| Drill down from list to detail | **Navigation stack** (push/back, swipe back) | Custom back behaviors |
| List + detail side by side at regular width | **Split view** (2–3 columns, optional inspector) | Stretched phone layouts |
| Short, self-contained sub-task | **Sheet** | Pushing a full screen for a quick edit |
| Choosing a view mode within one screen | **Segmented control** | Tabs for in-page filtering |

**Tab bars**
- Tabs are destinations, not actions. Never use a tab to trigger an action (e.g., "Compose" belongs in a toolbar).
- Keep tabs always visible and enabled; don't hide or disable a tab because its content is empty — show an empty state inside.
- Short single-word labels plus SF Symbols; the selected tab uses the tint.
- Search gets its own **search tab** at the trailing end (semantic search role).
- The tab bar floats on glass and may minimize on scroll (opt in), re-expanding when scrolling the other way.
- Preserve each tab's navigation state when switching.

**Sidebars**: group sections with headers, allow collapse, let people customize/reorder where useful; sidebar floats on glass above content; extend hero content beneath it with background extension.

**Navigation stack**: title reflects the current view; Back button shows previous title (or just the chevron if long); don't override swipe-back; large titles at top levels, inline titles deeper.

---

## 2. Bars & toolbars

- Toolbars hold **frequently used actions for the current view**. Put primary navigation (Back/Close) leading or top, the prominent confirming action (Done) trailing and visually prominent.
- **Group related items** so they share one glass background; separate groups with fixed space; keep groupings and order consistent across platforms and screens.
- Prefer **standard symbols** for common actions to declutter; use text only where no symbol is clear. Don't mix text and icon items in one group.
- Provide both a **title and a symbol** for each item (title is used in overflow menus and by accessibility).
- Set visibility priority so the most-used items (Compose, New Note) and status-bearing items (badges) overflow last. Use the **system overflow menu** (ellipsis) rather than a custom one; reserve the ellipsis symbol for overflow only.
- Hide the whole toolbar item, not just its content (avoid empty glass bubbles).
- Don't paint custom bar backgrounds; rely on the scroll edge effect for legibility.
- Keep items few: roughly 3 per side on iPhone before overflow.

---

## 3. Buttons & controls

**Hierarchy by style, not size**
- One **prominent** (filled/tinted, e.g., glassProminent or borderedProminent) button for the primary action per view — at most two prominent buttons in a view.
- Secondary actions: bordered/gray/glass; tertiary: plain/borderless text or symbol.
- Destructive actions use the **destructive role** (red), are never the default, and are separated from safe actions.
- Default (Return-key) button on Mac/iPad: the safe, likely action.

**General**
- Minimum 44×44 pt hit area; generous spacing between adjacent buttons.
- Labels are verbs in title case; icon-only buttons need accessibility labels.
- Show pressed/highlight state instantly; show progress or disable briefly if an action takes time (and explain why when disabled).
- Bar buttons are capsule-shaped and concentric with their container; extra-large control size exists for prominent actions.
- Don't make non-interactive text look like a button or link; don't use the tint color on non-interactive elements.

**Other controls**
- **Toggles (switches)**: binary on/off settings that take effect immediately; label states the setting, not the action. On Mac, checkboxes are typical in forms; switches for major on/off.
- **Segmented controls**: 2–5 mutually exclusive, equally-weighted options; consistent label type (all text or all symbols).
- **Sliders**: continuous values; show min/max symbols or values when meaningful.
- **Steppers**: small incremental changes; show the value next to it.
- **Pickers/menus**: choose from a list; use inline menus for few options, wheels/date pickers for dates.
- **Text fields**: placeholder describes expected content (not a label substitute in forms — use labels too); appropriate keyboard type; clear button; validate inline and gently.
- **Links**: tinted color plus another cue (underline or context) when inside body text.

---

## 4. Menus

- Use menus for secondary actions and options that don't need to be always visible; buttons can **morph** into their menus.
- Order items by frequency or logical sequence; group with separators; put destructive items last (and red).
- Use standard icons for standard actions (Copy, Paste, Share, Delete) and keep wording consistent.
- **Context menus** (long-press/right-click) offer actions relevant to the item; the top actions should match that item's swipe actions.
- Mac: every command available in the **menu bar** with standard menus (App, File, Edit, View, Window, Help), keyboard shortcuts using standard ones (⌘C, ⌘Z, ⌘,…). iPadOS now has a menu bar too.
- Use an ellipsis (…) in a menu item title when it opens a dialog requiring more input.

---

## 5. Modality

Modality interrupts; use it only when it clearly helps people focus on a task or a critical decision.

**Sheets**: for focused sub-tasks (compose, add item, edit settings). Provide clear Cancel (leading) and Done/primary (trailing). Support swipe-to-dismiss, but confirm before discarding unsaved changes. Use detents (half/full) when people benefit from seeing content behind. Avoid stacking sheets; avoid modal-over-modal.

**Alerts**: only for critical information or decisions that need immediate attention (unsaved changes, destructive confirmation, errors that block progress). Short title, optional brief message, 1–2 (max 3) buttons with specific verbs. Destructive option red; Cancel bold/default when the alternative is destructive. Never use alerts for success confirmation or tips.

**Action sheets / confirmation dialogs**: choices related to an action the person initiated; they originate from the control that triggered them (anchored), and include Cancel.

**Popovers** (iPad/Mac): transient content anchored to a control; dismiss by tapping outside; don't put another popover inside.

**Full-screen modals**: immersive tasks (camera, media playback, multistep creation) — always with an obvious way out.

---

## 6. Search

- iPhone: search typically lives at the **bottom** (toolbar or search tab) within thumb reach; field moves up with the keyboard. iPad/Mac: top-trailing in the toolbar.
- App-wide search → search tab. Searching within a list → search field in that view.
- Show recent searches/suggestions before typing; results update as people type; scope bar/tokens for filtering; clear empty-result state with a suggestion.
- Placeholder names what's searchable ("Search Recipes").

---

## 7. Lists, collections, forms

- **Lists/tables**: one clear primary line per row, secondary info in secondary label color; leading image/symbol optional; disclosure chevron only when row navigates; swipe actions for common item actions (destructive swipe = full-swipe delete with undo); support reordering/multi-select where useful via Edit/Select.
- **Grouped (inset) style** for settings and forms; plain style for content feeds.
- Section headers in title-style capitalization; footers explain settings.
- **Collections/grids**: consistent item sizes, adaptive column count, even counts for foldables.
- **Forms**: group related fields into sections; labels beside or above fields; sensible defaults; mark optional fields rather than every required one; inline validation with clear fixes; keep primary action in the toolbar/bottom; respect AutoFill (names, addresses, one-time codes, passwords/passkeys).
- **Settings**: put frequently changed settings in-app; rarely changed ones may go to system Settings; never require settings to start using the app.

---

## 8. Feedback, loading, status

- Every action gets visible feedback; state changes are shown where they happen.
- **Loading**: show content as soon as possible; use placeholders/skeletons that match final layout; determinate progress when duration is known, indeterminate spinner when not; never a blank screen; let people keep working where possible; avoid modal blocking.
- **Empty states**: explain what goes here and offer the action to start.
- **Errors**: inline, near the source, in plain language with a fix; don't clear what people typed.
- **Badges**: for counts that need attention; don't overuse.
- **Notifications**: valuable, timely, actionable; never marketing spam; ask permission in context.
- **Haptics**: consistent mapping (success/warning/error/selection/impact); don't overuse.

---

## 9. Onboarding, permissions, accounts

- Get people **into the experience fast**. Prefer learning by doing over tutorial carousels; if onboarding exists, keep it brief and **skippable**.
- Don't require an account before showing value; delay sign-in until it's needed. Offer Sign in with Apple / passkeys where relevant; never ask for info you can get from the system.
- **Permissions**: request at the moment of need, after explaining the benefit; write a specific purpose string; respect "No" gracefully and keep working with reduced functionality; offer a path to Settings later. Never prompt at launch without context.
- Collect only necessary data; be transparent about what you collect and why.
- Make account deletion available in-app if accounts can be created.

---

## 10. Undo, editing, data entry

- Support **undo/redo** broadly (shake/three-finger swipe on iOS, ⌘Z on Mac, toolbar buttons where useful). Undo makes exploration safe — prefer it over confirmations.
- Auto-save where possible; don't make people manage saving.
- Preserve input on errors, backgrounding, and orientation changes.
- Minimize typing: defaults, pickers, AutoFill, suggestions, scanning, dictation.
- Drag and drop between views/apps on iPad and Mac; copy/paste everywhere; let people select text.

---

## 11. AI and generative features (Responsibility)

- Be clear when content is generated; set expectations about accuracy.
- Keep people in control: preview before applying, easy edit and undo, never take irreversible actions on people's behalf without confirmation.
- Anticipate harmful or wrong output (e.g., a recipe model ignoring a logged allergy) and add safeguards — previews, confirmations, constraints — or remove the feature if risk outweighs value.
- Offer feedback mechanisms; protect privacy of inputs.
