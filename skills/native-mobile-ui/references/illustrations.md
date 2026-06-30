# Illustrations on mobile

Read this when a mobile task involves illustrations or art, an empty/onboarding/success screen that could carry a visual, or a question about where to source graphics. Illustrations add character and warmth, but on mobile they're easy to get wrong. This file covers *when* they earn their place, *how* to keep them consistent and performant, *where* to get them for free, and an optional AI-generation path.

**Confirm with the developer first.** Before adding an illustration to a screen where one fits, and unless the brief already specifies it, ask two things in order: (1) include an illustration here at all? and only if yes, (2) which source — their own assets, a free vector library below, or AI-generated? Lock that answer in and keep every illustration in the app consistent with it. Don't raise the question on screens where illustrations don't belong (settings, forms, dense lists/feeds, data tables).

## When an illustration earns its place

Use one only where it does a job. Good places on mobile:

- **Onboarding** — set tone and explain value in a glance.
- **Empty states** — turn a blank screen into an invitation to act (paired with a clear primary action).
- **Success / completion** — a small moment of delight after a task.
- **Errors** — soften a dead-end and point to the fix.
- **Permission priming** — explain *why* before the system permission dialog.

Where to skip them: dense list/feed screens, forms, settings, anywhere they'd push the real primary action below the fold or just decorate. On a small screen, an illustration competes with the content for the most valuable space — make it earn that space or cut it.

## The two rules that matter most

1. **One library, one style, across the whole app.** Mixing illustration styles is the visual equivalent of mixing three fonts on one screen. Consistency beats variety — pick a single source and stick to it. This is the single biggest lever for looking "designed" vs "assembled".
2. **Mind the real estate and the CTA.** The illustration supports the action; it never buries it. On an empty state, the user must still see and reach the button without scrolling.

## Free vector sources (with licenses)

Prefer **vector (SVG)** for in-app illustrations: crisp at every density, tiny, and recolorable for dark mode. License safety for a commercial app runs CC0 / open ≥ MIT ≥ attribution-required ≥ paid-for-commercial.

**Default — unDraw** (undraw.co): minimalist flat SVGs, recolor to one accent on-site, SVG/PNG, open license, **commercial use without attribution**. License only forbids repackaging the catalog, building a competing service, or training AI on it — none of which touch normal app work. Trade-off: one style, one accent, widely recognized.

**People / onboarding — Open Peeps, Open Doodles, Humaaans** (Pablo Stanley): **CC0**, no attribution, mix-and-match characters (clothing, hair, expression). Best for character variety and representation in onboarding and empty states.

**Scenes — ManyPixels** (manypixels.co): large gallery, on-site recolor, SVG/PNG, free for personal and commercial use, no attribution.

**Motion states — LottieFiles** (lottiefiles.com): Lottie animations render as vector and weigh kilobytes, so they're the performant way to animate loading / empty / success states, and they play natively via the Lottie libraries on iOS / Android / React Native. **License varies per animation — check each one;** most community animations are free.

**Gradient style — IRA Design**: MIT, free for commercial.

**Attribution-required (use only if you can credit) — Storyset** (storyset.com): many styles, on-site recolor, and built-in simple animation, but the **free tier requires an attribution link**; a Freepik Premium subscription removes it. Great if you can credit; otherwise fall back to unDraw / Open Peeps.

Recommended default stack for an app: **unDraw** for general scenes, **Open Peeps** when you need people, **Lottie** for animated states — and never more than one static style in the same product.

## Technique (mobile-specific)

- **Optimize SVGs** through SVGO to strip metadata and redundant paths before shipping.
- **Accessibility:** decorative illustrations get `aria-hidden` / no screen-reader exposure; meaningful ones get a role and a short descriptive label.
- **Dark mode:** recolor for dark mode rather than overlaying a light illustration on a dark surface; use sources that let you set colors (unDraw, ManyPixels) so both themes share one palette.
- **Performance:** lazy-load below-the-fold art; prefer inline/vector over large rasters; one Lottie beats a heavy GIF.
- **Density:** vector means you skip @1x/@2x/@3x entirely — another reason to prefer it.

## Optional: AI-generated illustrations

If the user has access to an AI image tool (e.g. Higgsfield) and wants richer, more photographic/cinematic visuals for hero or marketing-style onboarding screens, treat it as an **optional path, not a default** — for these reasons:

- It outputs **raster**, not vector, so you lose crispness-at-any-density, easy dark-mode recolor, and the tiny file sizes that vector gives you. Fine for a hero image, poor for repeated in-app UI states.
- **Free tiers are usually watermarked and limited for commercial use** — verify the plan's commercial license before shipping any generated asset.
- AI output is **hard to keep stylistically consistent** across many screens, which collides with the one-style rule above.

When it *is* the right call (one rich onboarding or marketing visual), keep it on-brand by generating from the project's design tokens. Build the prompt from: the app's palette (named hex values), the intended mood, the subject, and an explicit style direction, plus aspect ratio for the target screen. Generate a few variants, pick the one that sits closest to the rest of the UI, and don't mix it with a different illustration style elsewhere in the product.
