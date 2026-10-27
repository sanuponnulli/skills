# Cross-platform & framework specifics

How to get Apple-correct behavior in each stack. APIs evolve — if a name below doesn't compile, check the framework's current docs; the design intent stays the same.

Contents: 1. SwiftUI Liquid Glass APIs · 2. React Native · 3. Flutter · 4. Electron · 5. Tauri · 6. Desktop web apps that should feel Mac-like

---

## 1. SwiftUI — Liquid Glass (iOS/iPadOS/macOS 26+)

Default: use system components and they adopt glass automatically. Reach for these only for **custom controls on the control layer**.

```swift
// Single custom control
Button("Share", systemImage: "square.and.arrow.up") { share() }
    .buttonStyle(.glass)                 // secondary
// .buttonStyle(.glassProminent)         // primary action (one per view)

// Custom view with glass
Label("Recording", systemImage: "record.circle")
    .padding()
    .glassEffect(.regular.tint(.red).interactive(), in: .capsule)
// Variants: .regular (default, legible anywhere), .clear (only over rich media), .identity (no glass)

// Several glass elements near each other: wrap in a container
// (renders and blends them together, and is faster than separate effects)
@Namespace private var glassNS
GlassEffectContainer(spacing: 20) {
    HStack(spacing: 20) {
        ForEach(tools) { tool in
            Image(systemName: tool.symbol)
                .frame(width: 44, height: 44)
                .glassEffect()
                .glassEffectID(tool.id, in: glassNS)   // lets shapes morph during transitions
        }
    }
}

// Back-deploy fallback
if #available(iOS 26, *) {
    content.glassEffect(in: .rect(cornerRadius: 16))
} else {
    content.background(.ultraThinMaterial, in: .rect(cornerRadius: 16))
}
```

Rules: glass only on controls/navigation; never glass inside glass; group nearby glass elements in one `GlassEffectContainer`; use `.interactive()` for things people press; tint only to convey meaning; nested shapes use `ConcentricRectangle` / container-relative corners. Other new-design APIs: `.scrollEdgeEffectStyle`, `.safeAreaBar(edge:)` for custom bars, `.backgroundExtensionEffect()` under sidebars, `.tabBarMinimizeBehavior(.onScrollDown)`, `Tab(role: .search)`, `TabView` `.tabViewStyle(.sidebarAdaptable)`, `ToolbarSpacer(.fixed)` between toolbar groups.

---

## 2. React Native (incl. Expo)

| Apple concept | React Native |
|---|---|
| Safe areas | `react-native-safe-area-context` (`SafeAreaView` / `useSafeAreaInsets`) |
| Semantic colors | `PlatformColor('label')`, `PlatformColor('systemBackground')`, `DynamicColorIOS({light, dark})`; `useColorScheme()` |
| Dynamic Type | Leave `allowFontScaling` on (default); avoid fixed-height text containers; test with large text; use `maxFontSizeMultiplier` only for chrome, never body |
| Navigation stack | `@react-navigation/native-stack` (real native push, swipe back, `headerLargeTitle`, `headerSearchBarOptions`) |
| Tab bar | bottom tabs (prefer native tabs where available); 2–5 tabs, symbol + label |
| Sheets | native-stack `presentation: 'formSheet'` with `sheetAllowedDetents`; or a native sheet library — avoid JS-drawn fake sheets |
| Action sheet / alert | `ActionSheetIOS`, `Alert.alert` with `style: 'destructive' / 'cancel'` |
| SF Symbols | `expo-symbols` (`SymbolView`) on iOS |
| Blur / materials | `expo-blur` `BlurView` (control layer only) |
| Haptics | `expo-haptics` (`notificationAsync`, `selectionAsync`, `impactAsync`) |
| Touch targets | `Pressable` with `hitSlop` to reach 44×44 pt |
| Accessibility | `accessibilityLabel`, `accessibilityRole`, `accessibilityState`, `accessible` grouping, `AccessibilityInfo.isReduceMotionEnabled()` |

Use `Platform.OS` to keep Android Material conventions on Android — don't force iOS chrome there.

---

## 3. Flutter

- Use **Cupertino** widgets for an iOS feel: `CupertinoApp`, `CupertinoTabScaffold` + `CupertinoTabBar`, `CupertinoNavigationBar` / `CupertinoSliverNavigationBar` (large title), `CupertinoPageRoute` (swipe back), `CupertinoListSection.insetGrouped` + `CupertinoListTile`, `CupertinoAlertDialog`, `showCupertinoModalPopup` / `CupertinoActionSheet`, `CupertinoSwitch`, `CupertinoSlidingSegmentedControl`, `CupertinoSearchTextField`, `CupertinoContextMenu`.
- Or use adaptive constructors to match each platform: `Switch.adaptive`, `Slider.adaptive`, `CircularProgressIndicator.adaptive`, `AlertDialog.adaptive`.
- Colors: `CupertinoColors.label`, `.secondaryLabel`, `.systemBackground`, `.systemGroupedBackground`, `.systemBlue` — they're dynamic; resolve with `CupertinoDynamicColor.resolve(color, context)` when used outside Cupertino widgets.
- Respect `MediaQuery.textScalerOf(context)` (don't clamp body text), `SafeArea`, `MediaQuery.disableAnimationsOf(context)` (reduce motion), and `Semantics` labels on custom widgets.
- Icons: `CupertinoIcons` (close to SF Symbols in style).

---

## 4. Electron (macOS)

```js
new BrowserWindow({
  titleBarStyle: 'hiddenInset',          // native traffic lights, content under the title bar
  trafficLightPosition: { x: 16, y: 18 },// align with your toolbar's vertical center
  vibrancy: 'sidebar',                   // native material behind a transparent sidebar
  visualEffectState: 'followWindow',
  backgroundColor: '#00000000',
  minWidth: 640, minHeight: 400,         // resizable; never a fixed size
});
```
- Make the top toolbar area draggable with CSS `-webkit-app-region: drag`, and set `no-drag` on every button/input inside it. Leave ~78px of leading space for the traffic lights.
- Build a real **menu bar** with `Menu.setApplicationMenu` using standard roles (`appMenu`, `fileMenu`, `editMenu`, `viewMenu`, `windowMenu`, `help`) so Undo/Copy/Paste/Quit and their shortcuts work; add your commands with accelerators.
- Native context menus (`Menu.popup`), native dialogs (`dialog.showMessageBox`), `nativeTheme` for dark mode, system accent via `systemPreferences.getAccentColor()`.
- Settings window via ⌘, ; remember window size/position; support full screen.
- Use macOS sizes: body 13px, controls ~22–28px tall, compact sidebar rows (~28px).

## 5. Tauri (v2)

- Window config: `"titleBarStyle": "Overlay"`, `"hiddenTitle": true` (traffic lights over your content); add `data-tauri-drag-region` to the toolbar element for dragging.
- Window materials via the window effects config (e.g., sidebar/under-window vibrancy) with a transparent window background.
- Native menus via the menu API with predefined items (copy, paste, undo, quit) so standard shortcuts work.
- Same sizing and behavior rules as Electron above.

## 6. Desktop web apps that should feel Mac-like

When a browser app (React dashboard, admin tool) targets desktop users, use desktop density rather than phone layouts: sidebar + content + optional inspector, toolbar at top with grouped icon buttons, 13–14px body, 28px rows, keyboard shortcuts shown in tooltips and menus, right-click context menus where expected, visible focus rings, resizable panes. Don't add fake traffic lights inside a browser tab.
