# Typography and Color

One consistent type and color code throughout the deck. The fastest way to look amateur is three slides with three different font sizes for the same element.

## 1. The type scale (the only allowed sizes)

Canvas is 1280×720px, where 1pt ≈ 1.33px. The floor is **11pt = 15px: no text anywhere on a slide — including inside Chart.js options — may be smaller than 15px**, and every size must come from this scale. No fractional sizes, no arbitrary values, no off-scale one-offs.

| Token | Size | Weight / style | Used for |
|---|---|---|---|
| `display` | 64px | Bold | Single hero metric (one per slide, rare) |
| `big-number` | 40px | Bold | Big-number rows; title-slide deck title |
| `title` | 28px | Bold | Action title (every body slide) |
| `section` | 18px | Bold, may be uppercase | Column/section headers, chart headings, pillar labels, exec-summary claims |
| `body` | 16px | Regular (bold for mini-headers) | All body text, bullets, evidence blocks, table cells |
| `caption` | 15px | Regular | Chart axis labels/ticks, data labels, footnotes, source line, page number |

Line heights: 1.25 for titles, 1.4–1.5 for body. Text blocks max ~2 lines; no widows/orphans on titles.

## 2. Font rules

- System sans-serif stack: `-apple-system, "Segoe UI", Helvetica, Arial, sans-serif`. Never import external fonts.
- Hierarchy via **weight and color**, not via extra sizes: bold near-black mini-headers over regular grey body is the standard evidence-block pattern.
- Italics only for quotes, notes, and pillar-style labels. No letter-spaced all-caps body text; uppercase is reserved for short section headers.
- Numbers in metrics use `font-variant-numeric: tabular-nums`.

## 3. Color system — palette roles

Every color on a slide must map to an assigned role. **No decorative color. No rainbow charts.** If a color can't be named by its role, remove it.

### Fixed neutrals (every deck)

| Role | Color |
|---|---|
| Background | `#FFFFFF` |
| Emphasis text / mini-headers | `#1A1A1A` |
| Body text | `#595959` |
| De-emphasis, context series, disabled pillars | `#B0B0B0` (light) / `#8C8C8C` (mid) |
| Rules, gridlines | `#E8E8E8` (light) or brand primary (title rule) |

### Brand palette (role-assigned)

When the user provides a brand kit or brand colors, map them to roles:

| Role | Assignment | Used for |
|---|---|---|
| **Primary** | The dominant brand color (darkened toward ~`#333`-level luminance if too bright for text) | Action titles, title rule, section headers, focal data series, focal pillar, emphasis figures |
| **Secondary** | The second brand color | Comparison data series, secondary section accents |
| **Highlight** (optional) | A third, brighter brand color | Callout annotations and highlight ellipses ONLY — never body text, never a whole series |

Fallback when no brand is provided: **maroon `#7A1F1F` as primary**, greyscale for everything else (no secondary, no highlight). Tints of the primary (e.g., 20–40% opacity) may serve as the comparison-series color when no secondary exists.

Rules:
- Same palette on every slide of the deck. Never switch accent colors between slides.
- Primary must pass contrast on white for 28px bold text; if the brand primary is too light, darken it and note that in the slide plan.
- Text is only ever: near-black, body grey, de-emphasis grey, white (on primary background), or primary (titles/headers). Body copy is never in brand colors.

## 4. Enforcement notes

- Chart.js defaults (12px ticks, legend text) violate the floor — every chart config must set fonts explicitly (see charts.md §5).
- Tailwind users: `text-xs` (12px) and `text-sm` (14px) are **banned**. Use arbitrary-value classes that match the scale exactly: `text-[15px] text-[16px] text-[18px] text-[28px] text-[40px] text-[64px]`.
- Scaling the slide to fit a viewport must be done by transform-scaling the whole 1280×720 canvas — never by shrinking individual font sizes.
