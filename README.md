# Executive Slide Generator

**MBB-tier executive strategy slides, generated as React artifacts by Claude.**

An Agent Skill for [Claude Code](https://code.claude.com/docs/en/skills) and [Claude.ai](https://claude.ai) that transforms prompts into polished executive slides styled to $50k strategy deck standards. Built on the [Agent Skills standard](https://agentskills.io).

![License: Apache 2.0](https://img.shields.io/badge/license-Apache%202.0-blue.svg)

---

## What It Does

Give Claude a strategic insight, dataset, or business question — and it produces a `.jsx` React artifact that looks like it came from McKinsey's Information Design team:

- **Single slides** for hero metrics, tension frameworks, or visual monoliths
- **Multi-slide decks** with keyboard navigation, narrative arc, and dot indicators
- **Data-driven layouts** that extract the single most compelling insight and build around it

The skill enforces strict design constraints: intentional asymmetry, 20% minimum negative space, monochromatic depth with a single accent color, and a 3-second readability rule. No dashboards. No startup decks. No bullet-point walls.

## Examples

| Prompt | Output |
|--------|--------|
| "Create an executive slide showing Q3 revenue exceeded forecast by 15%, driven by APAC expansion" | Hero Metric layout with governing thought, `text-8xl` metric, supporting proof cards |
| "Build a strategy deck comparing our current GTM motion vs. a PLG pivot" | Multi-slide deck with Tension layout, Three Pillars argument, and recommendation close |
| "Here's our monthly ARR data for the last 12 months — make it boardroom-ready" | Visual Monolith with CSS-rendered bar chart, highlighted inflection point, desaturated context |

## Installation

### For Claude.ai (Custom Skills)

1. Download or clone this repo
2. Upload the `executive-slide/SKILL.md` file as a custom skill in Claude.ai
3. Ask Claude to make you an executive slide — it activates automatically

### For Claude Code (Personal Skill)

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/executive-slide-skill.git

# Copy to your personal skills directory
cp -r executive-slide-skill/executive-slide ~/.claude/skills/executive-slide
```

### For Claude Code (Project Skill)

```bash
# From your project root
mkdir -p .claude/skills
cp -r path/to/executive-slide-skill/executive-slide .claude/skills/executive-slide
```

### Via Plugin Marketplace (if registered)

```
/plugin marketplace add YOUR_USERNAME/executive-slide-skill
```

## Layout Archetypes

The skill selects layouts based on **narrative energy**, not content format:

| Layout | Use When | Structure |
|--------|----------|-----------|
| **Hero Metric** | The insight is a decisive number | 60/40 weighted, massive `text-7xl`+ metric |
| **Tension** | Highlighting contrast or decision | Weighted split: Current State (muted) vs Future State (emphasized) |
| **Transformation** | Demonstrating progression | Horizontal flow with chevrons or connected steps |
| **Visual Monolith** | The chart IS the story | Single dominant card at ~80% of canvas |
| **The Argument** | Proving a thesis | Max 3 cards with variable vertical heights |

## Design System

- **Canvas:** Fixed `w-full h-[600px]` with subtle gradient background
- **Typography:** System sans-serif stack — no external font imports
- **Color:** Monochromatic slate palette + ONE accent per deck (Electric Blue, Growth Teal, Risk Amber, or Critical Rose)
- **Icons:** `lucide-react` at `strokeWidth={1.5}` for premium weight
- **Charts:** Pure CSS flex/grid bars and inline SVGs — no chart libraries needed

## How It Works

The skill gives Claude a detailed playbook for executive slide design. When you ask for a strategy slide, consulting slide, executive deck, or McKinsey-style presentation, Claude:

1. **Decodes** the single governing insight from your input
2. **Selects** the layout archetype based on narrative energy
3. **Composes** with intentional asymmetry and negative space rules
4. **Audits** against the 3-second readability test
5. **Renders** a production-ready React `.jsx` artifact

Every slide includes a governing thought (kicker + action title), source attribution, and confidentiality footer.

## Trigger Phrases

Claude activates this skill when you mention:

- "executive slide" / "strategy slide"
- "McKinsey-style slide" / "consulting slide"
- "executive deck" / "strategy deck"
- "boardroom-ready" / "partner presentation"

## Skill Spec

| Field | Value |
|-------|-------|
| **Name** | `executive-slide` |
| **Format** | Single `SKILL.md` file |
| **Output** | React `.jsx` artifacts |
| **Dependencies** | `lucide-react` (icons only) |
| **Compatibility** | Claude.ai, Claude Code, any Agent Skills-compatible tool |

## Contributing

Issues and PRs welcome. If you've found a layout pattern or design constraint that makes slides better, open a PR against the `SKILL.md`.

## License

Apache 2.0 — see [LICENSE](LICENSE) for details.

---

**Created by [Trevor James](https://github.com/YOUR_USERNAME)** — MBA candidate at Indiana University Kelley School of Business, founder of [OPAL](https://github.com/YOUR_USERNAME), and president of MBAi Club.
