# Starter tokens

Read this in **design / build** mode when you need concrete values to start from — a screen brief rarely hands you a spacing scale or a type ramp, and improvising those per-component is what makes a build feel assembled rather than designed.

This is **one sane default**, not a catalogue. It exists so you start from a coherent system and adjust to the brand, not from nothing. Pick these values, then deviate on purpose. Exact platform figures (44pt vs 48dp, etc.) still come from `ios.md` / `android.md` — these tokens layer on top.

The point of tokens is one source of truth: define each value once as a named role, reference the name everywhere. A raw `#3B82F6` or a bare `16` scattered through screens is the thing tokens exist to kill.

## Spacing

One scale, 4pt base, 8pt rhythm. Use only these steps — if you reach for a value not on the scale, the scale is wrong, not the layout.

```
space-0   0      space-3   12
space-1   4      space-4   16   ← default gutter / screen margin
space-2   8      space-5   24
                 space-6   32
                 space-7   48
                 space-8   64
```

Defaults: screen side margins `space-4` (16). Gap between related items `space-2`/`space-3`. Section separation `space-5`/`space-6`. Don't use `space-1` (4) for layout — it's for fine optical nudges (icon-to-label, baseline alignment) only.

## Type

A 7-step ramp with intentional weight, not size-only hierarchy. Sizes in pt/sp; **never hard-lock them** — map each role to the platform text style (iOS Dynamic Type, Android type roles) so it scales with the user's font setting. These are the *base* sizes before scaling.

```
role        size  weight   use
display     34    700      one big number / hero moment, sparingly
title       28    700      screen title
heading     22    600      section heading
subhead     17    600      card / row title, emphasized
body        17    400      primary reading text — the floor for content
callout     15    400      secondary text, supporting copy
caption     13    400/500  metadata, timestamps, labels
```

Line-height ≈ 1.3–1.4 for headings, ≈ 1.45–1.55 for body. Don't drop body below ~16sp/17pt. Use weight (400 / 500 / 600 / 700), not just size, to carry hierarchy. Use tabular figures for numbers in columns, prices, and timers so they don't jitter.

## Color (semantic roles)

Define **roles**, not raw hex, and give every role a light and a dark value — dark mode is a real pass, not an inversion. Components reference the role (`surface`, `on-surface`), never the hex. The hex below is a neutral placeholder ramp; swap in the brand.

```
role            light      dark       meaning
bg              #FFFFFF    #000000    app background, furthest back
surface         #F7F7F8    #1C1C1E    cards, sheets, raised areas
surface-alt     #EFEFF1    #2C2C2E    nested / secondary surface
on-bg           #11181C    #ECEDEE    primary text/icon on bg
on-surface      #11181C    #ECEDEE    primary text/icon on surface
on-surface-muted#5B6470    #9BA1A6    secondary text, captions
border          #E2E4E8    #2E3236    dividers, hairlines (visible in BOTH modes)
primary         #2563EB    #5B8DEF    brand action, primary CTA
on-primary      #FFFFFF    #0B1220    text/icon on a primary fill
success         #16A34A    #4ADE80    positive state (+ icon, never color alone)
warning         #D97706    #FBBF24    caution state (+ icon/text)
error           #DC2626    #F87171    error/destructive (+ icon/text)
```

Rules that come with these: meaning never rides on color alone (pair error with an icon or text). Verify each `on-*` / background pair hits 4.5:1 (3:1 for large text and meaningful glyphs) **separately** in each mode — the light ratio does not guarantee the dark one. Borders must stay visible in both themes.

## Radius & elevation

```
radius-sm   8     inputs, small controls, chips
radius-md   12    cards, list rows, sheets
radius-lg   20    large cards, modal corners
radius-full 999   pills, avatars, FAB

elevation-0   flat on surface (use border, not shadow, to separate)
elevation-1   resting card        — soft, short shadow
elevation-2   sheet / menu        — medium
elevation-3   modal / dialog      — strong, plus a scrim behind
```

Keep one elevation scale; don't invent per-component shadow values. In dark mode prefer a lighter `surface` tone over a heavy drop shadow to show elevation — shadows read poorly on black. Modal/sheet scrim ≈ 40–60% black.

## Motion

```
instant     <100ms   tap feedback — press state, ripple, highlight (always)
fast        150ms    state toggles, small fades
base        250ms    most transitions, sheet/modal present
slow        350ms    full-screen / hero transitions (cap here)
```

Easing: ease-out entering, ease-in exiting; exits ≈ 60–70% of the enter duration. Animate `transform` / `opacity` only — never width/height/top/left. Everything respects reduce-motion: when it's on, cut to a cross-fade or no motion, never block the user.

## How to apply

State the token set you're using at the start of a build, then reference roles by name in the output (`space-4`, `surface`, `primary`) rather than hardcoding numbers — that's what makes the result auditable against the [review checklist] and easy to retheme. If the project already has tokens, defer to those; this file is the floor for when it doesn't.
