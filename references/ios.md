# iOS specifics (Human Interface Guidelines)

Read this when a design targets iOS or when a cross-platform screen hits a divergence point. These are the concrete iOS numbers and idioms that override or specialize the cross-platform principles in SKILL.md.

## Hard numbers

- **Minimum touch target:** 44×44 pt. This is the floor — controls smaller than this are hard to hit reliably.
- **Spacing grid:** 8 pt base, 4 pt for fine work. Standard screen margins are 16–20 pt.
- **Body text:** 17 pt is the default body size; don't go below ~15 pt for primary reading text. Support Dynamic Type — size text with text styles (Body, Headline, Caption…) rather than fixed point sizes so it scales with the user's setting.
- **Corner radii / heights** follow the current iOS look; prefer system components so they update with the OS.

## Safe area

- Respect the top safe-area inset (status bar + notch / Dynamic Island) and the bottom inset (home indicator). Place no interactive control in the home-indicator strip.
- Content may extend edge-to-edge and scroll under the status bar and a large title, but interactive controls stay within the safe area.
- The bottom edge belongs to the system swipe-up gesture — keep critical controls a comfortable distance above it.

## Navigation idioms

- **Back:** a chevron + (optional) title at the top-left of the navigation bar, plus the interactive edge-swipe-from-left to go back. Don't disable edge-swipe-back without good reason.
- **Tab bar:** bottom tab bar for 3–5 top-level destinations; icon + short label; one active tab.
- **Large titles:** iOS favors large navigation-bar titles that collapse to inline on scroll for top-level screens.
- **Modality:** sheets (including the resizable/detented bottom sheet) for focused tasks; action sheets for a short list of choices tied to an action; alerts only for critical, blocking decisions.
- **Segmented control** for switching between a few mutually exclusive views of the same data.

## Components & system idioms

- iOS rarely uses a floating action button — put the primary action in the navigation bar, a bottom toolbar, or inline.
- Use **SF Symbols** for iconography so weight and scale match the system font and Dynamic Type.
- Default font is **SF Pro** (San Francisco); use the system font unless brand demands otherwise.
- Prefer native controls (switches, steppers, pickers, the date/time picker) — users know them and they handle accessibility for free.
- Haptics: use the system haptic patterns for confirmation/selection/impact sparingly and meaningfully.

## When cross-platform

If you're sharing a codebase, keep the iOS build feeling like iOS for: back gesture, sheet presentation, action sheets vs snackbars, and the absence of a FAB. The brand palette and illustrations can be shared; the navigation feel should not be Android's.
