# Android specifics (Material Design)

Read this when a design targets Android or when a cross-platform screen hits a divergence point. These are the concrete Android numbers and idioms that override or specialize the cross-platform principles in SKILL.md.

## Hard numbers

- **Minimum touch target:** 48×48 dp (the visual element can be smaller, but the touch area should be ≥48 dp). Keep ≥8 dp between targets.
- **Spacing grid:** 8 dp base, 4 dp for fine work. Standard screen margins are 16 dp.
- **Body text:** ~16 sp for body. Always size text in **sp** (not dp) so it honors the user's font-scale setting; size touchable layout in **dp**.
- **Elevation:** Material uses elevation/tonal layering to express hierarchy (app bar, cards, FAB, sheets). Keep elevation meaningful, not decorative.

## Safe area / insets

- Handle window insets for the status bar, the navigation bar / gesture area, the display cutout, and the IME (keyboard). Modern Android is edge-to-edge: draw behind the system bars but inset interactive content.
- The bottom gesture area belongs to the system (back and home gestures) — keep controls clear of it.

## Navigation idioms

- **System back is sacred.** Android has a global back (gesture from either edge, or a button) that the user expects to work everywhere. Never add a custom in-content back control that competes with it; provide an **Up** affordance in the app bar for hierarchical up-navigation, which is distinct from system back.
- **Navigation bar (bottom):** Material bottom navigation for 3–5 top-level destinations. For more destinations or larger screens, consider a navigation drawer or navigation rail.
- **Top app bar:** holds the title, Up affordance, and primary screen actions / overflow menu.
- **FAB:** the floating action button is the native idiom for a screen's single most important action — use it deliberately, one per screen.

## Components & system idioms

- **Snackbars** for brief, transient feedback (with an optional single action) — the Android equivalent of an iOS toast/alert for non-blocking messages.
- **Material dialogs** for decisions; **bottom sheets** (standard or modal) for a set of actions or a focused task.
- Use **Material Symbols** for icons and **Roboto** (or the Material default) as the system typeface unless brand demands otherwise.
- Prefer Material components (switches, chips, sliders, menus, date pickers) — they handle theming, ripple feedback, and accessibility.
- Ripple: every tappable Material surface shows a ripple on press — keep that touch feedback.

## When cross-platform

If you're sharing a codebase, keep the Android build feeling like Android for: system back behavior, snackbars (not iOS alerts) for transient messages, the FAB idiom, and Material component shapes. Share the brand palette and illustrations; don't impose iOS's navigation feel on Android.
