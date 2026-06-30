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
├── LICENSE
├── .claude-plugin/
│   ├── marketplace.json        # Claude Code marketplace catalog (for /plugin install)
│   └── plugin.json             # plugin manifest
└── skills/
    └── native-mobile-ui/
        ├── SKILL.md            # core cross-platform principles + review checklist + example review output
        └── references/
            ├── ios.md          # Human Interface Guidelines specifics (44pt, safe area, SF Symbols…)
            ├── android.md      # Material specifics (48dp, system back, FAB, snackbars…)
            ├── tokens.md       # starter token set (spacing, type, semantic color, radius, motion)
            └── illustrations.md # when to use illustrations, free vector sources + licenses, technique
```

The repo is packaged as a **Claude Code plugin** (so it installs from a marketplace) that ships one skill, `native-mobile-ui`, under `skills/`. The skill uses progressive disclosure: `SKILL.md` holds the platform-agnostic principles and the checklist, and the platform/token/illustration files are loaded only when a task actually needs them.

## Installation (Claude Code)

This repo is a Claude Code plugin marketplace. The recommended way to install is through the marketplace; the other options copy the bare skill if you prefer.

### Option 1 — Claude Code marketplace (recommended)

Inside Claude Code, add this repo as a marketplace, then install the plugin:

```
/plugin marketplace add almazjanat/native-mobile-ui
/plugin install native-mobile-ui@almaz-skills
```

- `almazjanat/native-mobile-ui` is the GitHub repo that hosts `.claude-plugin/marketplace.json`.
- `almaz-skills` is the marketplace's `name` (from `marketplace.json`); `native-mobile-ui` is the plugin.
- Update later with `/plugin marketplace update almaz-skills`, and manage it under `/plugin`.

You can also add it from a local clone for testing:

```
/plugin marketplace add /path/to/native-mobile-ui
```

### Option 2 — personal skill (available in all your projects)

Copy just the skill folder into your personal skills directory:

```bash
git clone https://github.com/almazjanat/native-mobile-ui.git
cp -r native-mobile-ui/skills/native-mobile-ui ~/.claude/skills/
```

> **Windows note:** PowerShell and cmd.exe do **not** expand `~` to your home directory (only Git Bash / WSL / macOS / Linux do). In PowerShell, copy with an explicit path instead:
> ```powershell
> Copy-Item -Recurse native-mobile-ui\skills\native-mobile-ui "$HOME\.claude\skills\native-mobile-ui"
> ```

### Option 3 — project skill (committed to a repo, shared with your team)

```bash
mkdir -p .claude/skills
cp -r native-mobile-ui/skills/native-mobile-ui .claude/skills/
git add .claude/skills/native-mobile-ui && git commit -m "Add native-mobile-ui skill"
```

Anyone who clones the project gets the skill. When the same skill name exists at multiple levels, the order is enterprise → personal → project → plugin (earlier wins).

### Verify

```bash
# Marketplace install:
/plugin                                      # native-mobile-ui shows as installed & enabled

# Copied skill:
ls ~/.claude/skills/native-mobile-ui         # should list SKILL.md and references/
```

Plugin skills are namespaced — invoke explicitly with `/native-mobile-ui:native-mobile-ui` if needed, though Claude pulls the skill in automatically on mobile-app UI work either way. Edits inside an already-watched skills directory take effect within the current session; a newly created top-level skills directory needs a Claude Code restart to be watched.

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
- **Tokens** — `skills/native-mobile-ui/references/tokens.md` is a starter spacing/type/color/motion scale; replace its values with your brand's tokens.
- **Illustrations** — `skills/native-mobile-ui/references/illustrations.md` defaults to free vector sources (unDraw, Open Peeps, Lottie) with license notes and a one-library-per-project rule. There's an optional AI-generation branch if you use a generator like Higgsfield; edit it to match the source you actually license.

## License

Released under the [MIT License](LICENSE) — free to use, modify, and share, with no warranty.
