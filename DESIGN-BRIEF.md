# Design Brief: Student Reading Progress Dashboard

Product Manager: Desherae Frost

Scrum Team: Moorhen

Preferred PM review due date: [TBD]

Preferred 3 amigos due date: [TBD]

## Overview

We are evolving a validated functional prototype of the K-2 reading-progress dashboard into a production UI built on the Ignite brand system. The information architecture, interaction model, and metric logic are settled; this work is about making it look and feel like Ignite and meet our production design and accessibility standards.

Reference: [live prototype](https://chris-geiser.github.io/student-progress-dashboard/).

## Why

District leaders need a self-serve view of reading growth that reads as an Ignite product, not a wireframe. The prototype proved the structure (district to school to grade to student) and the metric storytelling (start, current, projected, target, months of growth). It now needs the brand layer and the polish required for something we put in front of customers.

1. The prototype uses a neutral, system-font palette that does not reflect the Ignite brand.
2. Status, projection, and emphasis colors were chosen functionally and need to map to Ignite's design tokens, including accessible contrast in both light and dark mode.

We will keep the existing layout and interaction model unless there is a strong reason to change it; the focus is restyling to the design system, not redesigning the IA.

### Why is this restyle important

  - First impression and trust: this is a renewal- and expansion-facing surface, so it has to look like a finished Ignite product.
  - Brand consistency: it should match our other tools (type, color, spacing, components).
  - Accessibility: status is currently carried heavily by color (green on-track / red below); we need redundant cues and verified contrast to meet WCAG 2.1 AA.
  - Foundation for future work: a token-based, component-based build makes later features (exports, additional metrics) faster to ship.

## Target Users

|  |  |  |
| :-: | :-: | :-: |
| Role | Description | Goals / Pain Points |
| District / System Admin | Oversees outcomes across all schools; owns budget and renewals. | Needs an at-a-glance, trustworthy district view. Reads the dashboard on desktop, occasionally on tablet. |
| Principal | Accountable for one school across its grades. | Compares grades, spots units below target. Needs clear hierarchy between school summary and per-grade detail. |
| Literacy Coordinator | Targets instruction and intervention. | Scans student tables to find below-target and not-yet-mastered students. Needs legible dense data. |

## Design Needs

Walk each surface and restyle to the Ignite design system (type, color, spacing, elevation, components). Apply real brand tokens in place of the prototype's functional values; keep behavior the same unless flagged.

1. In the District and School views (header):
    1. Restyle the view title, the counts subtitle bar, and the top-right open-seats block (count plus "Fill Seats" button, or "all seats filled" text). The "Fill Seats" button should use the Ignite primary/action button component.
2. In the District and School views (growth insight statement):
    1. Restyle the callout that summarizes all-student growth ("Your students have made N months of progress..."). The key figures sit in inline pills today; map these to a brand treatment for emphasized inline stats.
3. In all views (three projected metric cards):
    1. Restyle the summary cards (Projected months of growth, Projected WCPM, Projected HFW), including the value, the "by year-end" subtitle, and the green "+N since last week" trend line. Map the trend's positive color to the brand's success token.
4. In the District and School views (aggregate charts):
    1. Restyle the per-school / per-grade charts. Each has a track, a status-colored fill, a diagonal projected-growth slash, a target tick with a target value pill below it, journey pills (Start, Current, Projected) with status-colored strokes, and a centered notes block. Define brand treatments for: the status colors (on-track / below target), the projected-growth slash pattern, the pills, and the notes block.
5. In the Grade view (student table):
    1. Restyle the sortable table, the metric toggle (pill buttons on desktop, dropdown on mobile), the legend, the inline per-student bar (start dot, fill, projected slash, target tick), the signed growth and delta values, the projected-EOY dot, and the "Mastered at initial assessment" row treatment.
6. Responsive behavior:
    1. Confirm and refine the breakpoints (3-up to 2-up to 1-up cards; table horizontal scroll with a sticky Student column; stacked headers on mobile).
7. Dark mode:
    1. Provide brand-aligned dark-mode tokens; the prototype follows system preference with no toggle.
8. Data-freshness footer:
    1. Restyle the bottom note ("Data updates at the top of every hour... Refresh the page to see new data.").

**Note:**

  - Status currently relies on color alone (green / red). I do not think color-only is acceptable for accessibility; please add a redundant cue (icon, label, or pattern) for on-track vs. below target.
  - On the aggregate charts, the journey pills can collide when values are close; the prototype hides lower-priority pills (Start and Projected win). A brand-native solution for crowded labels would be welcome.
  - Cross-grade aggregate values (e.g., a district WCPM average) mix different grade targets. The visual should not imply a single shared benchmark; lean on months of growth as the grade-agnostic headline.
  - Keep the IA and drill-down model; this is a restyle, not a redesign.

## Additional Requirements

1. Deliver the design as Ignite design-system tokens and components (type scale, color, spacing, radius, elevation, buttons, cards, table, chips/pills) so engineering builds against the system, not one-off values.
2. Specify both light and dark mode for every token used.
3. Provide accessibility annotations: contrast ratios, focus states, keyboard navigation for the table and toggle, and the non-color status cue.
4. Provide redlines/specs for the custom chart elements (bar, fill, projected slash, target tick and pill, journey pills, notes block) since these are not standard components.
5. Metric and data definitions are owned in the companion metrics spreadsheet; designers do not need to define calculations, only how each value is displayed.
