# Platforms

Each platform deserves the same level of care (Flexibility: "approach every platform with intention"). Shared foundations apply everywhere; this file covers what's different.

---

## iOS (iPhone)

- **Context**: medium high-res display, held in one or two hands at 1–2 ft, used on the go in short bursts or long sessions; frequent app switching.
- **Inputs**: Multi-Touch gestures, virtual keyboard, voice, sensors; personal data with permission.
- **Best practices**
  - Limit on-screen controls; make secondary details discoverable with minimal interaction.
  - Adapt to orientation, Dark Mode, and Dynamic Type.
  - Put key controls in the middle/bottom for reach; support swipe-back and row swipe actions.
  - Use platform capabilities (Apple Pay, Face ID, location, AutoFill) instead of asking people to type data.
- **Structure**: tab bar for top-level, navigation stack for depth, sheets for tasks, toolbars for actions. Bottom search on iPhone.
- **System touchpoints**: widgets, Live Activities, Home Screen quick actions, Spotlight, Shortcuts/App Intents, share sheet, notifications.

## iPhone Duo (foldable, 2026)

You're still designing for iPhone — iOS rules apply — but resizability is mandatory.
- **Two displays**: outer (closed; wider and shorter than other iPhones) and inner (open). Many poses: book, tent, flat, on edge.
- **Don't design per pose.** Build one compact-width layout (outer) and one regular-width layout (inner) with size classes, margins, and safe-area insets; let them expand. No fixed widths.
- **Consistent across displays**: same functionality and state; on the inner display show an extra hierarchy level (e.g., list + detail).
- **Vertical controls**: toolbars, tab bars, and navigation controls move to the **side** on the outer display and inner landscape (inner portrait keeps horizontal bars). Follow system placement; don't override it.
  - Top of the vertical axis: navigation (Back/Close), then prominent action (Done); keep remaining groups intact.
  - Set toolbar visibility priority; items overflow bottom-to-top into the system overflow menu.
  - Navigation-focused views keep the tab bar and overflow toolbar items; task-focused views minimize the tab bar to keep the toolbar.
  - Give every toolbar item a title and symbol; keep text buttons minimal (they stay horizontal).
  - Keep pane-specific controls with their pane, not on the side.
  - Account for asymmetry: content space is offset by side controls (use safe areas).
- **Reserved regions**: outer camera (always, expands into Dynamic Island), inner camera (only when active), folding region (when partially folded). Keep interactive elements away from the fold; system alerts, menus, and sheets move automatically; use the reserved-region APIs for custom UI.
- **Folding**: make small adjustments, not dramatic rearrangements. Split views rebalance panes; arrangement views (split/overlay) organize a primary and secondary view automatically — keep navigation containers outside them.
- **Full-width immersive** layouts (like Calculator) are fine for non-scrolling visual UIs if they avoid the Dynamic Island/status bar.
- **Games**: fill the screen in every pose; prefer changing aspect ratio over letterboxing.

## iPadOS

- Large display, touch + Apple Pencil + keyboard + trackpad; multitasking with continuously resizable windows (window controls, no fixed preset sizes) and a menu bar.
- Use sidebars and split views (with inspectors) instead of stretched phone layouts; tab bar can adapt into a sidebar.
- Support arbitrary window sizes and fluid column reflow; respect safe areas around window controls.
- Support pointer hover effects, keyboard shortcuts (discoverable via menu bar), drag and drop, Pencil and Scribble where text input exists.
- Popovers and context menus are appropriate here; toolbar and search trailing-top.

## macOS

- **Context**: large display(s) at 1–3 ft, stationary, keyboard + high-precision pointer; sessions from minutes to hours of deep work; many apps open.
- **Best practices**
  - Use space to show more content in fewer nested levels, with less modality, at a comfortable density.
  - Let people resize, hide, show, move windows; support full screen.
  - Put **every command in the menu bar** with standard menus and shortcuts; contextual menus on right-click.
  - Support precise selection/editing and keyboard-only workflows (full keyboard navigation, focus rings).
  - Support personalization: customizable toolbars, configurable windows, the system accent color.
- **Conventions**: window controls top-left (always same spot); toolbar integrated in title bar; sidebar + content + inspector; Settings window via ⌘,; undo via ⌘Z; drag and drop; document-based patterns; no hamburger menus or floating action buttons; don't fix window sizes.
- Body text 13 pt; controls come in mini/small/regular/large/extra-large sizes; hit targets ~28 pt.
- macOS doesn't support Dynamic Type — respect the system text size settings where available and the accent/highlight color.

## watchOS

- Glanceable, seconds-long interactions on a tiny display; Digital Crown, side button, touch, gestures (double tap).
- Show the most important info immediately; keep hierarchy shallow; use full-width elements and edge-to-edge content.
- SF Compact; large, legible type; high contrast on black backgrounds.
- Complications, Smart Stack widgets, Live Activities, notifications are primary touchpoints.
- Use standard toolbar and button styles (they adopt the current design).
- Haptics for meaningful moments; avoid requiring text input.

## tvOS

- Viewed from ~10 ft, controlled via Siri Remote with the **focus** model: every interactive element must have a clear focused state (lift, parallax, glass highlight via standard focus APIs).
- Large type (body 29 pt), generous spacing, simple navigation (top tab bar), edge-to-edge media.
- Avoid text-heavy screens and text entry; keep interactions shallow.

## visionOS

- Spatial: windows, volumes, and immersive spaces in the person's surroundings; inputs are eyes (look) + hands (pinch), plus voice and keyboards.
- Targets ≥ 60 pt; elements need visible hover/gaze highlights; keep content within a comfortable field of view; place UI at a comfortable distance; avoid requiring head/body movement.
- Glass windows by default; use vibrancy for text hierarchy; text mostly white on glass; prefer 2D text; bold text when not on a background (no shadows); billboard labels so they face the person.
- Respect people's comfort and surroundings: avoid sudden motion, keep immersion opt-in and easy to exit, don't block passthrough unnecessarily.
- Use ornaments for toolbars attached to windows; tab bars sit vertically on the leading side.

## Games (all platforms)

- Readable text at platform minimums; support platform inputs (touch, controller, keyboard) with on-screen prompts matching the active input; fill screens across sizes; pause/resume gracefully; respect accessibility settings.
