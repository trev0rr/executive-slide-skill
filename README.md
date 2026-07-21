# Executive Slide Generator

**Management-consulting-grade slides and decks, generated as React artifacts by Claude.**

An Agent Skill for [Claude Code](https://code.claude.com/docs/en/skills) and [Claude.ai](https://claude.ai) that produces `.jsx` slide decks to MBB consulting-academy standards: pyramid-structured storylines, action titles, Chart.js charts with labeled axes and sources, and flat WSJ-style layouts. Built on the [Agent Skills standard](https://agentskills.io).

![License: Apache 2.0](https://img.shields.io/badge/license-Apache%202.0-blue.svg)

---

## What It Does

Give Claude a strategic insight, dataset, or business question — and it storylines, plans, and renders a consulting deck:

- **Storyline first**: governing thought, MECE argument branches, and an action-title list that passes the headline-flow test before any slide is designed
- **Per-slide planning**: message, evidence, layout pattern, and chart type declared and checked against hard rules before rendering
- **Real charts**: every chart is Chart.js — correct type for the comparison, labeled axes and units, benchmark lines labeled on the chart, sources cited
- **Executive copy**: a mandatory humanizer pass strips AI-isms and filler; titles are complete "so what" sentences
- **Hard self-check**: a per-slide checklist (fonts, sources, chart standards, palette roles) runs before anything is delivered

## Architecture

```
executive-slide/
  SKILL.md                 # Hard rules, workflow, worked examples, self-check
  reference/
    storylining.md         # Pyramid Principle, MECE trees, deck types, headline-flow test
    layout.md              # 1280x720 canvas, grid, title block, 9 layout patterns
    charts.md              # Chart selection matrix, labeling rules, Chart.js patterns
    typography.md          # Integer type scale (15px floor), palette roles
    language.md            # Action-title craft, copy rules, humanizer pass
```

SKILL.md requires the model to read all five reference files before building anything.

## The Standard

- **Flat consulting style**: white background, brand-color action title with a thin rule, aligned columns, ≥20% whitespace — no cards, shadows, or gradients
- **Action titles**: every slide title is a complete sentence stating the conclusion ("50% annual growth with declining profitability is unsustainable…"), never a label ("Growth Trends")
- **Pyramid + MECE**: conclusion first; deck titles alone tell the complete story; 4+ slide decks get a title slide and executive summary automatically
- **Chart discipline**: chart type matched to the comparison (component/item/time-series/frequency/correlation/waterfall), axes labeled horizontally with units, sources on every slide
- **Typography**: integer sizes from a fixed scale, nothing below 15px (11pt) anywhere — including inside charts
- **Palette roles**: primary / secondary / highlight brand colors with assigned jobs, greyscale for context; brand kits adopted when provided, maroon fallback otherwise

## Installation

### For Claude Code (Personal Skill)

```bash
git clone https://github.com/YOUR_USERNAME/executive-slide-skill.git
cp -r executive-slide-skill/executive-slide ~/.claude/skills/executive-slide
```

### For Claude Code (Project Skill)

```bash
mkdir -p .claude/skills
cp -r path/to/executive-slide-skill/executive-slide .claude/skills/executive-slide
```

### For Claude.ai (Custom Skills)

Upload the `executive-slide/` folder (SKILL.md + reference files) as a custom skill.

## Trigger Phrases

- "executive slide" / "strategy slide" / "consulting slide" / "MBB-style slide"
- "executive deck" / "strategy deck" / "board deck"
- "boardroom-ready" / "partner presentation"

## Skill Spec

| Field | Value |
|-------|-------|
| **Name** | `executive-slide` |
| **Format** | `SKILL.md` + 5 reference files |
| **Output** | React `.jsx` artifacts (1280×720 stage, deck shell with keyboard nav) |
| **Dependencies** | `chart.js` (charts), `lucide-react` (icons) |
| **Compatibility** | Claude.ai, Claude Code, any Agent Skills-compatible tool |

## Contributing

Issues and PRs welcome. If you've found a layout pattern or rule that makes slides better, open a PR.

## License

Apache 2.0 — see [LICENSE](LICENSE) for details.

---

**Created by [Trevor James](https://github.com/YOUR_USERNAME)** — MBA candidate at Indiana University Kelley School of Business, founder of OPAL, and president of MBAi Club.
