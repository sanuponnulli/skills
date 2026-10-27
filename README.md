# Skills

Agent skills for Claude.

| Skill | What it does |
|---|---|
| [apple-design-hig](skills/apple-design-hig/SKILL.md) | Designs, builds and reviews UI using Apple's 2026 Human Interface Guidelines: the eight design principles, Liquid Glass, SF typography, Dynamic Type, semantic color, layout and accessibility. Covers iOS, iPadOS, macOS, watchOS, tvOS, visionOS and the web, plus SwiftUI, UIKit, React Native, Flutter, Electron and Tauri. |

## Install

### Claude Code (plugin marketplace)

```
/plugin marketplace add sanuponnulli/skills
/plugin install apple-design-hig@sanuponnulli-skills
```

### Claude Code (manual)

Copy the skill folder into your personal skills directory:

```bash
git clone https://github.com/sanuponnulli/skills.git
cp -r skills/skills/apple-design-hig ~/.claude/skills/
```

Or copy it into `.claude/skills/` inside a project to use it only there.

### Claude.ai

1. Download `apple-design-hig.zip` from the [latest release](https://github.com/sanuponnulli/skills/releases/latest).
2. In Claude, go to **Settings › Capabilities › Skills** and upload the zip.

## Use

The skill loads automatically when a task is about how a UI looks, reads or flows. For example:

- "Make this SwiftUI settings screen feel native."
- "Review this dashboard for UX issues."
- "Build an Apple-style landing page for my app."

## Structure

```
skills/apple-design-hig/
├── SKILL.md              # core guidance, always loaded
└── references/           # loaded section by section as a task needs them
    ├── foundations.md
    ├── components-patterns.md
    ├── platforms.md
    ├── web.md
    ├── cross-platform.md
    ├── review-checklist.md
    └── sources.md
```

## Disclaimer

This skill is an independent summary of Apple's public Human Interface Guidelines, written in its own words. It is not affiliated with or endorsed by Apple. For authoritative details, see the official sources listed in [`references/sources.md`](skills/apple-design-hig/references/sources.md).

## License

[MIT](LICENSE)
