# Charts — Selection, Labeling, and Chart.js Implementation

Charts convey relationships among data points and make data concrete — but only when the reader can decode them without help. Every chart must survive the stand-alone test: correct type, labeled axes, units, sources.

## 1. The mandate

**Every chart is a real chart object.** In web artifacts that means Chart.js; in `.pptx` output it means native PowerPoint charts via the python-pptx chart API (`add_chart`). No CSS-flex "bars," no hand-drawn SVG charts, no chart screenshots, no `<img>` placeholders, no ASCII charts. If a slide plan calls for a chart, it calls for a chart config. All selection, labeling, and styling rules in this file apply to both renderers.

Implementation pattern (React artifact):

```jsx
import { useEffect, useRef } from "react";
import Chart from "chart.js/auto";

function SlideChart({ config }) {
  const canvasRef = useRef(null);
  useEffect(() => {
    const chart = new Chart(canvasRef.current, config);
    return () => chart.destroy();
  }, []);
  return <canvas ref={canvasRef} />;
}
```

- Always destroy on cleanup (prevents duplicate renders on deck navigation).
- Set `options.responsive = true`, `maintainAspectRatio = false`, and size the chart with a wrapper `<div>` of fixed height.
- Set `options.animation = false` — slides are documents, not dashboards.
- Wrap each chart in its own component so remounting on slide change re-creates it cleanly.

## 2. Choosing the chart type

Match the chart to the **comparison in the action title**, using the trigger words:

| Comparison | Trigger words in the message | Chart |
|---|---|---|
| **Component** (percentage of a total) | "share," "percentage of total," "accounted for X percent" | Stacked bar (preferred) or pie; 100% stacked bar for share shifts over time |
| **Item** (ranking items) | "larger than," "smaller than," "equal," "most," "least" | Horizontal bar, sorted by value |
| **Time series** (change over time) | "change," "grow," "rise," "decline," "increase," "fluctuate" | Vertical column (few periods) or line (many periods); combo bar + line for two measures |
| **Frequency** (items within ranges) | "X to Y range," "concentration," "frequency," "distribution" | Histogram (vertical columns over bins) |
| **Correlation** (between variables) | "related to," "increases with," "changes with," "varies" | Scatter (`type: "scatter"`), or paired horizontal bars for few items |
| **Waterfall** (build-up / break-down) | "build-up," "break-down," "bridge," "contribution to change" | Floating columns via Chart.js `[start, end]` bar values |

Decision discipline: one chart, one comparison. If the message contains two comparisons, either pick the one the action title asserts or use two small charts side by side — never one overloaded chart.

## 3. MBB exemplar patterns

**Combo bar + line (growth vs. margin).** Revenue as columns (primary brand color, `yAxisID: "y"`), margin % as a black line with point markers (`type: "line"`, `yAxisID: "y1"`). Data labels above each column and at each line point. Callout for the growth rate (e.g., "48% CAGR") as an annotation near a drawn trend arrow. This is the classic "growth is unsustainable" slide.

**Stacked bar with period comparison.** Two or three periods as stacked columns (core segment grey, new segment primary color), totals labeled above each column, CAGR/growth annotations between columns. Use for "where growth comes from."

**Benchmark line.** A horizontal dashed comparison line across a bar chart (industry average, target, break-even), **labeled directly on the chart** ("Industry average $3M") — implemented as a second dataset: `{ type: "line", data: Array(n).fill(value), borderDash: [8, 6], pointRadius: 0, borderColor: <secondary or grey> }` with a label annotation, not a legend entry.

**Waterfall.** Bars with `data: [[0, 176], [176, 257], ...]` (floating bars), grey for intermediate steps, primary color for start/end totals, connector expressed by the floating positions. Label each bar with its delta.

## 4. Graphic display rules (non-negotiable)

These override any minimalist instinct. A chart missing any of these fails review:

1. **Chart title describes the comparison** — "Shampoo Sales by Location," not "Sales Data." Rendered as slide text above the canvas (16–18px bold uppercase, brand color), not via Chart.js `title` (better typographic control).
2. **Both axes labeled, labels horizontal.** Never rotate axis labels; shorten category names or flip to horizontal bars instead.
3. **Units on every numeric scale** — "$M," "%," "Moves (Millions)." Put the unit in the axis title or immediately above the axis.
4. **Data labels with units where they don't clutter** — label the bars directly ("$3.9M") when there are few; rely on the axis when there are many. When bars are labeled directly, the y-axis grid may be suppressed.
5. **Comparison/average/target lines drawn and labeled on the chart itself** — never only in a legend.
6. **Source cited** — the slide's footer source line names the data source and the analysis owner (e.g., "Source: Product line financials; Kelley analysis").

Additional rules:
- Round numbers where possible; verify sums and percentages tie out (stacks add to totals; shares add to 100%).
- No legends when direct series labeling works (label the last point of each line, or label bars). If a legend is unavoidable, position it bottom, 15px font.
- Start bar-chart value axes at zero. Line charts may truncate the axis only when the delta is the story — and must then label every point.

## 5. Chart styling (color and type)

Colors follow the palette roles (typography.md §3):

- **Focal series** → primary brand color
- **Comparison series** → secondary brand color
- **Context/history series** → greys (`#B0B0B0`, `#8C8C8C`, `#D9D9D9`)
- **Callout annotations** → highlight color (only if a highlight color exists in the brand kit)
- Never more than 3 non-grey colors on one chart. A chart where every series has its own bright color is a rainbow chart — an automatic failure.

Typography inside charts — Chart.js defaults are 12px and violate the type floor. Set globally per chart:

```js
options: {
  animation: false,
  responsive: true,
  maintainAspectRatio: false,
  plugins: { legend: { display: false } },
  scales: {
    x: { ticks: { font: { size: 15 }, color: "#595959" }, grid: { display: false } },
    y: { ticks: { font: { size: 15 }, color: "#595959" },
         title: { display: true, text: "USD M", font: { size: 15 } },
         grid: { color: "#E8E8E8" } }
  }
}
```

- All chart text ≥15px, integer sizes only, grey `#595959` (or near-black for emphasis labels).
- Flat fills only: no gradients, no 3D, no rounded bars beyond `borderRadius: 2`, no shadows.
- Gridlines: light grey `#E8E8E8`, horizontal only, and only when values aren't directly labeled. Axis line thin grey.
- Data labels: render as positioned HTML/JSX over the chart wrapper or via an inline plugin; keep 15–16px, bold for the focal figure.

## 6. When NOT to chart

- A single number is the message → big-number layout (layout.md §5.7), not a one-bar chart.
- Precise line-item lookup is the point → table (layout.md §5.3). Tables show lots of information but convey relationships poorly — chart the relationship, table the reference detail (usually in the appendix).
- A concept/framework (no quantities) → concept visual (layout.md §5.6). Never fake a chart with invented numbers.
- If the user provided no data and none can be reasonably illustrated, do not invent a chart. Illustrative numbers are allowed only when clearly labeled "Illustrative" above the chart — and only when the user asked for a mock-up.
