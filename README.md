# Kirby Preferred Sources & Direct Trust Override

A specialized AI Agent skill for implementing Google's **Preferred Sources** button, **Direct Trust Override** architecture, **Discover Natural Language Feed Customization**, and **Google News Audio Briefing Attribution** (introduced August 2026).

---

## 🪄 The Magic Prompt

Copy and paste this directly into your AI coding assistant (Cursor, Windsurf, Claude Code, Antigravity):

```markdown
@agent Please install the Kirby Preferred Sources skill into this workspace.
1. Read the `SKILL.md` file and `references/` directory from this repository: https://github.com/markkirby125/kirby-preferred-sources
2. Identify the correct rules/skills system for our current environment (e.g., `.cursor/rules/` for Cursor, `.windsurfrules` for Windsurf, or `~/.gemini/config/skills/` for Antigravity).
3. Save the contents appropriately, preserving the multi-file dispatcher structure.
4. Confirm when the installation is complete.
```

---

## Overview

Traditional SEO is an algorithmic guessing game that requires ongoing defensive maintenance against algorithm updates. **Direct Trust Override** bypasses algorithmic volatility by enabling visitors and customers to explicitly designate your domain as a **Preferred Source** in their Google Personalization Graph.

### Key Performance Benchmarks:
* **2x CTR Advantage**: Users who mark a site as a preferred source are twice as likely to click through when it appears in their Google AI search results (AI Mode, AI Overviews, and Top Stories).
* **3x Conversion Placement**: Isolating the CTA immediately after high-value content or 5-star reviews achieves 3x higher click-through rates than footer/sidebar placements.
* **Audio Attribution**: Preferred sources gain priority inclusion in Google News personalized daily audio briefings on Android.

---

## Manual Installation

### Google Antigravity / Claude Code (CLI)
To install with live local sync (recommended):
```bash
ln -sf "/path/to/kirby-skills/kirby-preferred-sources" "$HOME/.gemini/config/skills/kirby-preferred-sources"
```
Or clone standalone directly into your skills directory:
```bash
git clone https://github.com/markkirby125/kirby-preferred-sources.git ~/.gemini/config/skills/kirby-preferred-sources
```

### Cursor IDE
Create `.cursor/rules/kirby-preferred-sources.md` and copy the contents of `SKILL.md` and its `references/` files.

### Windsurf IDE
Add the contents to your `.windsurfrules` file.

---

## Repository Structure

```
kirby-preferred-sources/
├── SKILL.md                                  # Master Dispatcher & Index
├── README.md                                 # Magic Prompt & Installation Guide
├── .gitignore                                # Environment ignore rules
└── references/
    ├── module_1_direct_trust_mechanics.md   # Official JS SDK, deep links, domain rules
    ├── module_2_value_peak_cta_cro.md        # Isolated CTA psychology, 3x CTR copy formulas
    ├── module_3_discover_nl_audio_briefs.md # Discover NL customization, News audio briefings
    └── module_4_telemetry_attribution.md     # GA4/GTM custom events & GSC correlation
```
