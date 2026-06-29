# Native Mobile UI — a Claude skill

Design rules and a severity-tagged review checklist for native mobile app UI/UX — iOS, Android, and cross-platform (React Native, Flutter). It teaches Claude to design and audit phone-app screens the way a mobile design lead would — touch targets, safe areas, navigation, four screen states, accessibility, and illustration sourcing — instead of shrinking a desktop website down.

## What it does

The skill works in two modes:

- **Design / build** — when you're creating a screen or flow, it applies mobile-first principles (thumb-reachable primary actions, safe-area layout, the right navigation pattern, an 8pt grid, scalable typography, dark mode as a real pass, the four states every screen needs, keyboard-aware forms, purposeful motion, and built-in accessibility).
- **Review / critique** — when you ask it to look at an existing screen, it runs a checklist and reports each item as **pass / fail / N/A**, and on every fail gives a **severity** (`Blocker` / `Major` / `Minor`) and a concrete fix, so you know what to fix before release versus what's polish.

It triggers automatically on mobile-app UI work — including vague asks like "make this screen better", "clean up this screen", or "why does this screen feel off" — and deliberately stays out of desktop-web and responsive-website layout.

## What's inside

```
native-mobile-ui/
├── README.md
├── SKILL.md                    # core cross-platform principles + review checklist
└── references/
    ├── ios.md                  # Human Interface Guidelines specifics (44pt, safe area, SF Symbols…)
    ├── android.md              # Material specifics (48dp, system back, FAB, snackbars…)
    └── illustrations.md        # when to use illustrations, free vector sources + licenses, technique
```

The skill uses progressive disclosure: `SKILL.md` holds the platform-agnostic principles and the checklist, and the platform/illustration files are loaded only when a task actually needs them.

## Installation (Claude Code)

Claude Code auto-loads any valid `SKILL.md` it finds in a watched skills directory — no registration step. Pick one of these.

### Option 1 — personal (available in all your projects)

```bash
git clonehttps://github.com/almazjanat/native-mobile-ui.git ~/.claude/skills/native-mobile-ui
```

Or, if you have the packaged `native-mobile-ui.skill` file (it's just a zip):

```bash
unzip native-mobile-ui.skill -d ~/.claude/skills/
```

Or copy the folder by hand:

```bash
cp -r native-mobile-ui ~/.claude/skills/
```

### Option 2 — project (committed to a repo, shared with your team)

```bash
mkdir -p .claude/skills
cp -r native-mobile-ui .claude/skills/
git add .claude/skills/native-mobile-ui && git commit -m "Add native-mobile-ui skill"
```

Anyone who clones the project gets the skill. When the same skill name exists at multiple levels, the order is enterprise → personal → project → bundled (earlier wins).

### Option 3 — as a Claude Code plugin (marketplace)

Add a `.claude-plugin/marketplace.json` to the repo and push it to GitHub, then teammates run:

```
/plugin marketplace add <you>/native-mobile-ui
/plugin install native-mobile-ui@<marketplace-name>
```

### Verify

```bash
ls ~/.claude/skills/native-mobile-ui        # should list SKILL.md and references/
```

Edits inside an already-watched skills directory take effect within the current session. Creating a top-level skills directory that didn't exist when the session started requires restarting Claude Code so it can be watched.

## Usage

Once installed, Claude pulls the skill in automatically when a request is about a mobile-app screen. You can also invoke it explicitly. Examples:

- "Design an onboarding flow for a salon booking app."
- "Review this profile screen and tell me what to fix first."
- "Why does this checkout screen feel off?"
- "Make this empty state better."

In review mode you get a triaged report — `Blocker` items (e.g. tap targets below the platform minimum, text below AA contrast, broken system back) before `Major` and `Minor` ones.

## Compatibility

Built for **Claude Code** (personal, project, or plugin). The `SKILL.md` format is also usable on **claude.ai** (upload as a custom skill) and via the **Claude API**, and is portable to other agents that read the `SKILL.md` standard.

## Customize

- **Swap the brand** — the principles are palette-agnostic; point the design at your own tokens.
- **Tighten platform scope** — if you only ship iOS or only Android, you can trim the other reference file; the core principles still apply.
- **Illustrations** — `references/illustrations.md` defaults to free vector sources (unDraw, Open Peeps, Lottie) with license notes and a one-library-per-project rule. There's an optional AI-generation branch if you use a generator like Higgsfield; edit it to match the source you actually license.

## License

Released under the [MIT License](LICENSE) — free to use, modify, and share, with no warranty.
