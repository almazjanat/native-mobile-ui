---
name: native-mobile-ui
description: Design rules and a review checklist for native mobile app UI/UX — iOS, Android, and cross-platform (React Native, Flutter). Use this whenever the user is designing, building, reviewing, or critiquing a mobile app screen, flow, or component — onboarding, navigation, tab bars, forms, empty/loading/error states, touch targets, spacing, typography, dark mode, or illustrations. Trigger even when the request is vague and never says the words "design", "UX", or "mobile" — phrasings like "make this screen better", "improve/fix/clean up/polish this screen", "why does this screen feel off", "something's wrong with this layout", or "review my app screen" all qualify as long as the subject is a phone-app screen or flow. Default to using this skill for any app-screen work rather than answering from generic instinct. Do NOT use it for desktop web or responsive website layout — that is a different problem.
---

# Mobile Design

Design rules for native mobile interfaces, written to be platform-agnostic at the level of principle and platform-specific where it matters. A phone is not a small website: input is a thumb, not a cursor; the screen is held in one hand, often in motion, often outdoors; the OS owns the edges of the screen and a set of system gestures. Design from those constraints, not from a desktop layout shrunk down.

Work in two modes with this skill:

- **Designing / building** a screen or flow → apply the principles below, then run the review checklist before calling it done.
- **Reviewing / critiquing** an existing screen → go straight to the review checklist and report each item as pass / fail / not-applicable with a concrete fix.

## Pin the context first

Before designing, state three things out loud (infer them if the brief doesn't say): the **platform target** (iOS, Android, or cross-platform), the **screen's single job**, and the **primary action** the user takes on it. Everything else — where the button goes, what's in the nav, what can be cut — follows from those. If it's cross-platform, decide upfront which parts are shared brand and which must defer to platform convention (see "Diverging by platform").

## Core principles (all platforms)

These hold on every platform. Exact numbers that differ between iOS and Android live in `references/ios.md` and `references/android.md` — read the relevant one when you need a hard figure.

**Touch targets and reach.** Every tappable element needs a comfortable target (≈44pt on iOS, ≈48dp on Android — see platform files) with spacing between adjacent targets so the wrong one isn't hit. Put the primary action in the thumb's natural arc — the lower third of the screen — not in a top corner. Reserve top corners for low-frequency or destructive actions. This is why mobile uses bottom tab bars, bottom sheets, and floating action buttons instead of top toolbars: the bottom is reachable one-handed, the top is not.

**Respect the system's space.** The OS owns the status bar, the notch / Dynamic Island, the home indicator, and the edge-swipe zones. Lay out content inside the safe area; never place interactive elements under a cutout or in the home-indicator strip, and never fight the system back-gesture region. Content can scroll *under* the status bar, but controls must stay clear of it.

**Navigation is structural, not decorative.** Use the right pattern for the relationship between screens: a tab bar (3–5 destinations) for switching between top-level sections; a push/back stack for drilling into hierarchy; a modal or bottom sheet for a focused, self-contained task the user will finish and dismiss. Don't stack more than one modal. Keep navigation visible and predictable — a user should always know where they are and how to go back. Label the path with the same words throughout: the screen you push to from "Settings" is titled "Settings".

**Spacing on a grid.** Lay everything out on an 8pt grid (use 4pt for fine adjustments). Consistent spacing is most of what makes a screen feel "designed" rather than assembled. Pick a small spacing scale (e.g. 4 / 8 / 16 / 24 / 32) and use only those values.

**Typography that scales.** Set a clear type scale with intentional weights, and keep body text readable (≈16sp / 17pt minimum). Critically, mobile text must respect the OS's user font-size setting (Dynamic Type on iOS, font scale on Android) — never hard-lock font sizes, and make sure layouts don't break when type is scaled up for accessibility. Watch line length: on a narrow screen, long unbroken lines and tiny captions both hurt.

**Density and units.** Design in density-independent units (pt on iOS, dp/sp on Android), not raw pixels, so the UI is consistent across screen densities. Prefer vector assets (SVG / vector drawables / SF Symbols) over raster so nothing blurs at @2x/@3x. If raster is unavoidable, supply @1x/@2x/@3x.

**Color, contrast, and dark mode.** Meet WCAG AA contrast: 4.5:1 for body text, 3:1 for large text and meaningful UI elements. Never encode meaning in color alone (error states need an icon or text too, not just red). Treat dark mode as a real design pass with its own color tokens — not a mechanical inversion. Use semantic color roles (surface, on-surface, primary, error) so both themes derive from one system.

**Gestures need affordances.** A gesture the user can't see, they won't find. Back up swipe-to-delete, pull-to-refresh, and swipe-between-tabs with a visible cue or an equivalent tappable control. Don't overload one gesture with multiple meanings, and never override the OS's reserved gestures (edge-swipe back, swipe-up home, notification pull-down).

**Every screen has four states.** Design loading, empty, error, and success — not just the happy "full of data" state. Prefer skeleton placeholders over spinners for content that's loading (they communicate structure and feel faster). An empty state is an invitation to act, with a clear next step, not a blank void. An error state says what went wrong and how to fix it, in plain language. Account for offline: mobile loses connectivity constantly.

**Forms minimize typing.** Typing on glass is painful — design to avoid it. Use the right keyboard per field (email, number pad, phone), enable autofill / content-type hints, default smartly, and offer pickers over free text where possible. Validate inline, near the field, as the user goes. Handle the keyboard: when it opens it covers the bottom half of the screen, so the active field and the submit button must stay visible above it (keyboard avoidance), or the user is stuck.

**Motion with purpose, and a quality floor.** Animation should communicate hierarchy and continuity (where a screen came from, what's connected to what), be quick (≈200–300ms), and never block the user. Respect the reduce-motion setting. Give instant feedback to every tap (<100ms) — a press state, a ripple, a highlight — and use optimistic UI so actions feel immediate even while the network catches up.

**Accessibility is part of the floor, not a feature.** Label every control and image for screen readers (VoiceOver / TalkBack), keep a sensible focus order, hit the contrast and target-size minimums above, and support Dynamic Type. Building this in from the start is far cheaper than retrofitting it.

## Illustrations

Illustrations are a high-leverage place to add character on mobile — onboarding, empty states, success moments, permission priming — but they're easy to misuse (inconsistent style, bloated raster files, no dark-mode variant, pushing the real CTA below the fold). When a task involves illustrations, art, empty/onboarding states that could use a visual, or asks where to source graphics, **read `references/illustrations.md`** for when to use them, how to keep them consistent, free vector sources with license notes, and an optional AI-generation path.

## Diverging by platform

For a single-platform app, follow that platform's conventions fully. For cross-platform apps (React Native, Flutter, or a shared design system), the rule of thumb: **share the brand, respect the platform for navigation, system gestures, and core controls.** Users expect "back" to work the way their OS works; a brand color is welcome, a foreign navigation model is not. The biggest divergences:

- **Back navigation** — iOS: a back chevron at top-left plus edge-swipe-back. Android: the system back (gesture or button) plus an Up affordance. Don't put a custom in-screen back button on Android that competes with system back.
- **Top-level switching** — both use a bottom bar, but the component and behavior differ (iOS tab bar vs Material navigation bar). Item counts, label rules, and active states differ.
- **Transient messages & menus** — iOS uses action sheets and alerts; Android uses snackbars, Material dialogs, and bottom sheets. A "snackbar" on iOS or an "action sheet" on Android reads as foreign.
- **Primary-action placement** — Android's floating action button is a native idiom; iOS rarely uses a FAB and favors a bar-button or bottom-bar action instead.
- **Type and icons** — SF Pro + SF Symbols (iOS) vs Roboto + Material Symbols (Android).

When you hit one of these, read the matching platform file for the specifics. In React Native / Flutter, prefer platform-adaptive components over forcing one platform's look onto both.

- `references/ios.md` — Human Interface Guidelines specifics: exact sizes, safe-area details, navigation idioms, SF Symbols, iOS components.
- `references/android.md` — Material Design specifics: exact sizes, system back, navigation bar, FAB, snackbars, Material components.

## Review checklist

Run this when finishing a design or when asked to review one. For each item report **pass / fail / N/A**, and on any fail give its **severity** and the concrete fix. Severity tells the user what to fix first:

- **[Blocker]** — ships broken, inaccessible, or breaks a platform contract. Must fix before release: targets below the platform minimum, text below AA contrast, broken/duplicated system back, a missing state that strands the user, controls under a cutout or in the home-indicator strip, no screen-reader labels.
- **[Major]** — clearly wrong and degrades the experience, but not a hard block: off-grid spacing, missing dark mode, fixed font sizes that ignore Dynamic Type, weak keyboard handling, inconsistent illustration style, an undistinguished destructive action.
- **[Minor]** — polish: motion timing, micro-feedback niceties, copy tightening.

Each item below carries a default severity, but adjust by degree — a target at 42pt is a Minor miss, a 24pt one is a Blocker. This is the audit that turns the principles above into something verifiable.

**Touch & reach**
- [ ] [Blocker] All tap targets meet the platform minimum (44pt iOS / 48dp Android), with spacing between adjacent ones.
- [ ] [Major] The primary action sits in the lower (thumb-reachable) zone, not a top corner.

**Layout & safe area**
- [ ] [Blocker] Content and controls respect the safe area; nothing interactive sits under the notch / Dynamic Island or in the home-indicator strip.
- [ ] [Major] Everything aligns to the 8pt grid; spacing uses the defined scale.

**Navigation**
- [ ] [Major] The navigation pattern matches the screen relationship (tabs / push / modal-sheet); no double modals.
- [ ] [Blocker] Back behavior matches the platform (no custom control competing with system back); the user always knows where they are and how to leave.

**Typography & density**
- [ ] [Major] Type follows the scale; body ≥ ~16sp/17pt; nothing breaks when the OS font size is scaled up.
- [ ] [Major] Assets are vector (or @1x/@2x/@3x); units are pt/dp/sp, not raw px.

**Color, contrast & dark mode**
- [ ] [Blocker] Text meets 4.5:1 (3:1 for large text / UI); meaning never relies on color alone.
- [ ] [Major] Dark mode is a real pass with its own tokens, not an inversion.

**States**
- [ ] [Blocker] Loading, empty, error, and success states all exist; loading uses skeletons where appropriate.
- [ ] [Major] Offline / no-connectivity is handled.

**Forms & keyboard**
- [ ] [Major] Each field uses the correct keyboard type and autofill hints; pickers replace free text where possible.
- [ ] [Blocker] When the keyboard is open, the active field and submit button stay visible; validation is inline.

**Motion & feedback**
- [ ] [Minor] Every tap gives feedback < 100ms; transitions are ≈200–300ms and purposeful.
- [ ] [Major] Reduce-motion is respected.

**Accessibility**
- [ ] [Blocker] All controls and images have screen-reader labels; focus order is sensible.
- [ ] [Blocker] Dynamic Type, contrast, and target sizes are all met.

**Illustrations** (if any)
- [ ] [Major] One library / one style across the whole app; SVG optimized; dark-mode-safe; doesn't push the CTA below the fold. (See `references/illustrations.md`.)

**Platform fit** (cross-platform only)
- [ ] [Blocker] Navigation, system gestures, and core controls feel native on each platform; only the brand is shared.
