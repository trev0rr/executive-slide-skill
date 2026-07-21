# Layout — Canvas, Grid, and Slide Patterns

The visual standard is the flat consulting page: white background, colored action title with a thin rule, structured columns, generous whitespace, everything aligned. "WSJ look rather than USA Today" — substance over style. **No cards, no drop shadows, no gradients, no rounded containers, no background textures.** Structure is expressed with alignment, whitespace, thin rules, and type weight — never with boxes and shadows.

## 1. Canvas

- Fixed **1280 × 720 px** (16:9). All sizes below assume this canvas; scale proportionally only if the artifact viewport demands it (transform-scale the whole slide, never re-derive font sizes).
- Background: pure white `#FFFFFF`. Title slides may use the primary brand color as a full-bleed background with white text — body slides never do.

## 2. Page grid and margins

- Margins: **64px** left and right, **48px** top, **40px** bottom. Content never touches the canvas edge ("leave a small margin around your slide").
- Column gutter: **40px**. Two-column splits sit on the grid: 50/50, 55/45, or 60/40 of the content width. Symmetric layouts are normal and correct — use asymmetry only when one side genuinely carries more content (e.g., a dominant chart).
- Everything aligns: column tops align, baselines of parallel elements align, left edges of stacked blocks align. Misalignment reads as carelessness before anyone reads a word.
- **≥20% of the slide stays empty.** If a slide is crowded: cut text, merge points, or split the slide. Never shrink fonts or margins to fit.

## 3. Title block (every body slide)

- **Action title**: top-left, starting at the top margin. Primary brand color, bold, 28px, left-aligned, maximum 2 lines, wrapping cleanly (no orphan word on line 2). May span up to ~85% of content width.
- **Rule**: a 2px horizontal rule in the primary brand color, directly below the title (12–16px gap), running the **full content width** (margin to margin).
- **32px minimum gap** between the rule and the body region.
- No kickers, no eyebrow labels, no slide-number-in-title. The action title carries the message alone.

## 4. Footer zone (every body slide)

- **Bottom-left**: source line — `Source: <actual sources>; <who did the analysis> analysis` — 15px, grey `#8C8C8C`. Sources are real attributions for the claims on THIS slide (see charts.md §4). Notes (`Note: …`) go on a line above the source in the same style.
- **Bottom-right**: page number, 15px grey.
- Never add confidentiality stamps, draft watermarks, or firm logos unless the user asks.
- **House templates**: if the deck matches an existing branded template, reproduce that template's footer exactly (wordmark position, internal/date line) instead of this default — and when its design language has no source-line convention, put provenance in the slide content where a claim needs it rather than inventing a footer element the template doesn't have.

## 5. Layout patterns

Choose the pattern that fits the slide's message. Name the chosen pattern in the slide plan.

### 5.1 Chart + evidence column (the workhorse)
55–60% width chart panel left, evidence column right, 40px gutter. Chart panel: centered chart heading (16–18px bold, uppercase, brand color) above the Chart.js canvas; axis unit label top-left of the chart. Evidence column: an uppercase heading (e.g., "THE LAST FOUR YEARS"), then 3–5 stacked evidence blocks — each a **bold near-black mini-header** (a metric or claim, e.g., "48% CAGR") followed by 1–2 lines of 16px grey explanation. Optionally ends with a small arrow/divider and a forward-looking block ("THE NEXT FIVE YEARS"). Use when a chart proves the title and discrete facts support it. Flip sides if the story reads better chart-right.

### 5.2 Icon-row list
Full-width stack of 3–5 rows. Each row: thin-line icon (~40px, 1.5px stroke, brand color) at far left, then a **bold brand-color label** (2–4 words, may break over two lines), then the 16px grey description filling the rest of the width. Generous, even vertical spacing (rows breathe — roughly 90–120px apart). Use for principles, criteria, lifecycle stages, key concepts. One icon per row maximum; icons are row markers, not decoration.

### 5.3 Column comparison table
2–4 columns with **uppercase brand-color column headers**, rows separated by thin (1px) light-grey or brand-color horizontal rules. Optional row-label column at left (bold near-black, with an optional icon). Cells are short phrases, 16px, center- or left-aligned consistently. Use for option comparisons, deck-type/framework taxonomies, persuasive-vs-informative contrasts. This is a layout of aligned text — never a spreadsheet grid with visible cell borders.

### 5.4 Pillar tree
A single root element top-center (icon + italic bold label, e.g., "PROFITABLE GROWTH STRATEGY"), thin grey connector lines branching down to 3 pillars. Each pillar: icon, **uppercase italic pillar label** (brand color for the emphasized pillar, grey for the others), then 3–4 short supporting points with key phrases bolded. Use for strategy frameworks — the classic three-pillars slide. De-emphasize non-focal pillars with grey; emphasize one with the brand color if the story has a focus.

### 5.5 Horizontal roadmap (Gantt)
Left rail: swimlane labels (icon + uppercase grey label, one per workstream). Body: horizontal chevron/arrow bars per workstream positioned against a time axis (quarters/months) along the bottom, with thin vertical gridlines per period. Bars: primary brand color for the focal workstream, greys for others, black for the program-management bar spanning the full width at the bottom. Bar labels in white inside the bars; side annotations in italic grey attached with a brace where detail matters. Use for timelines, implementation plans, phased rollouts.

### 5.6 Full-width framework / matrix
A single organizing visual filling the content area: a selection matrix (columns = categories with red headers, rows = definition/example/trigger words), a 2×2, a concept diagram (flow, forces, structure). Text within the framework follows the normal type scale. Use when the framework itself is the message. Concept-visual vocabulary: flow (linear chevrons, vertical build, circular cycle), interaction (forces-at-work arrows, balance, penetration), structure (org tree, parts-of-whole, segmentation 2×2).

### 5.7 Big-number rows
3–5 rows, each: a **large brand-color figure** (40px, e.g., "1-6-6", "$4.6B", "48%") in a fixed-width left column, right-aligned, with the 16px grey explanation to its right, vertically centered. Use for rules, key stats, or a handful of headline metrics. For a single dominant metric, one 64px figure with a one-line explanation and supporting context below.

### 5.8 Title slide
Deck title large and centered or top-left (40px+ bold), tagline/subtitle below in grey, client name + date lower area. Either white with brand-color title, or full-bleed primary brand color with white text. No charts, no bullets.

### 5.9 Executive summary slide
Action title = the governing thought. Body: the 2–4 MECE supporting arguments as a vertical list — each a bold one-line claim (18px near-black) plus one 16px grey supporting sentence — in the order the deck proves them. Optionally pattern 5.7 if the arguments are metric-led. This slide must work as the only slide anyone reads.

## 6. Emphasis devices

Highlight key points with (in order of preference): **bold**, brand color, enlarged font from the approved scale, a drawn circle/ellipse around a chart figure, or a labeled callout ellipse (e.g., "48% CAGR" on an arrow). Use at most one or two devices per slide — emphasis everywhere is emphasis nowhere. De-emphasis is a tool: grey out the non-focal pillars, series, and columns so the focal element wins.

## 7. Density and text limits

- One idea per slide. Max ~6 supporting points, ~8 words per point (see storylining.md §9).
- Prefer visual + short annotations over prose paragraphs. Avoid all-text slides; when unavoidable (e.g., a situation-summary), keep to two columns of short bullets and never two such slides in a row.
- Numbers: round where possible, always show units, and make sure figures tie out across slides (the same metric never appears with two values).
- Detail, calculations, raw data → appendix slides, never crammed into body slides.
