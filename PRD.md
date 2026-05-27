# Student Reading Progress Dashboard — PRD

Product Manager: Desherae Frost

Scrum Team: Moorhen

> Metric and data-point definitions are not defined in this PRD. They live in the companion metrics spreadsheet: **[Student Progress Dashboard — Metrics, link TBD]**.

## Overview

Give district leaders self-serve visibility into K-2 reading growth across their district, drilling from district to school to grade to individual student. The dashboard shows where students started, where they are now, where they are projected to finish the year, and how that compares to grade-level targets, with the headline framed as months of growth.

A validated prototype exists ([live prototype](https://chris-geiser.github.io/student-progress-dashboard/)). This PRD scopes the production build on real student data.

### Why

District leaders currently rely on the Ignite partnerships team to assemble and interpret progress reporting. That is slow, does not scale, and keeps our impact data one step removed from the people making renewal and expansion decisions. A self-serve dashboard puts growth, projections, and at-risk students directly in front of admins, coordinators, and principals. It surfaces the "months of growth" story that differentiates Ignite, and it gives the field a durable artifact for renewal conversations.

## Goals & Success Metrics

Goals:

  - Playbook goal:
      - Support renewals and expansion by making Ignite's impact visible and self-serve for district decision-makers.
  - Product/Feature goals:
      - District leaders can see growth and year-end projections without partnerships-team involvement.
      - Users can quickly identify the students and grades that need attention.
      - The product communicates projected year-end outcomes in plain language (months of growth, WCPM, high-frequency words).

Success Metrics:

  - Admin activation rate (% of eligible district/school admins who view the dashboard) above `[TBD]`%.
  - Weekly active admins above `[TBD]`.
  - Reduction in partnerships-team reporting requests by `[TBD]`%.
  - `[TBD]` Correlation between dashboard usage and renewal rate (directional, longer horizon).

## Target Users

|  |  |  |
| :-: | :-: | :-: |
| Role | Description | Goals / Pain Points |
| District / System Admin | Oversees reading outcomes across all schools in the district. Controls budget and renewal decisions. | Needs a defensible, at-a-glance view of district-wide growth and projected outcomes. Today depends on partnerships for this. |
| Principal | Accountable for outcomes at one school across its grades. | Needs to compare grades, spot grades trending below target, and see projected year-end performance. |
| Literacy Coordinator | Supports instruction and intervention across schools or grades. | Needs to identify individual students who are below target or have not yet mastered foundational skills so support can be targeted. |

## User Stories + Requirements

As a district admin, I want a district overview so that I can see growth and year-end projections across all my schools at a glance.

1. Provide three drill-down views with no page reload: District, School, Grade (student-level). Back navigation labeled with the parent's name.
2. Show three projected year-end summary cards at every view (months of growth, words correct per minute, high-frequency words). Scope is all students aggregated at district and school, and grade-specific at the grade view. Each card shows the projected value, a "by year-end" subtitle, and a week-over-week trend.
3. Show a plain-language growth insight statement at the top of the district and school views, aggregated across all students (K-2).

As a principal, I want per-school and per-grade charts so that I can compare units and see projected outcomes.

4. On the district view, show one card per school; on the school view, show one card per grade. Each card carries three charts: months of growth, WCPM, and high-frequency words.
5. Each chart shows start, current, and projected positions, the grade-level target, and the status (on track vs. below target) by color.

As a literacy coordinator, I want a student-level table so that I can find students who need attention.

6. On the grade view, show a sortable student table with a metric toggle (WCPM, high-frequency words, phonological awareness, letter naming fluency; WCPM default). Columns: Student, Teacher, Start, Current, progress chart, Growth, Projected EOY, vs. EOY target.
7. Identify students who mastered a foundational metric at initial assessment and surface them distinctly rather than as a score.

Cross-cutting requirements:

8. Surface open seats and a "Fill Seats" call-to-action in the district and school headers when seats are available; show an "all seats filled" state otherwise. CTA destination `[TBD]`.
9. Refresh data at the top of every hour and tell users the page does not auto-refresh.
10. Support responsive layouts (desktop, tablet, mobile), dark mode, and meet accessibility standards (see Design Brief).

All metric formulas, inputs, and data lineage are specified in the companion metrics spreadsheet, not here.

## Maintenance Expectations

1. Partnerships: open seats and the "Fill Seats" CTA feed enrollment conversations. Partnerships may need to follow up on seat-fill requests and use the dashboard in renewal discussions.
2. CX (OAs, Tech Support, LSPs): Tech Support will field questions about data accuracy, refresh timing, and access. A data-discrepancy escalation path is needed.
3. Tutors / TOE: no direct impact expected; the dashboard is reporting-only.
4. Engineering: owns the hourly data pipeline and the source-system integration. Needs an on-call path for failed syncs or stale data, and clear ownership of the metric calculations (see Open Questions).

## Out of Scope

  - Write actions of any kind (editing rosters, scores, targets).
  - Export and print.
  - Automated push of summaries to external destinations (e.g., a Google Sheet / ProdEng-style digest).
  - Authentication and authorization design (assumes the existing platform's access model).
  - Real-time data (hourly refresh only).
  - Time-period selector / historical playback.
  - Native mobile apps.

## User Flows / UX Notes

  - Primary flow: District overview, click a school, click a grade, scan or sort the student table, drill into a student's metric via the toggle. Back button returns up one level.
  - Reference: [live prototype](https://chris-geiser.github.io/student-progress-dashboard/) demonstrates the information architecture, interaction model, and metric logic.
  - Visual design will be evolved to the Ignite brand system via the companion Design Brief. Figma link `[TBD]`.

## Risks

|  |  |  |
| :-: | :-: | :-: |
| Risk | Impact | Mitigation |
| Cross-grade aggregate values mix different grade targets (e.g., K WCPM target 10 vs. 2nd grade 90) | Admins may misread a district WCPM average without grade context | Lead with months of growth (grade-agnostic); keep absolute values for drill-down; revisit normalization if confusing in pilot |
| "Months of growth" formula is not yet finalized | Headline metric could shift after build | Data team to define and own the formula before development locks (see Open Questions) |
| Real data source(s) and lineage undefined | Blocks the data pipeline and the metrics spreadsheet | Confirm source systems early; lineage column in the spreadsheet is marked TBD until then |
| Aggressive timeline (full production by 7/31/2026) | Scope or quality risk | Phase ruthlessly; pilot with one district before beta |
| Week-over-week trend has no real history source | Trend could mislead if shipped without real data | Treat trend as gated until a real time-series source exists |

## Milestones / Timeline

|  |  |  |  |
| :-: | :-: | :-: | :-: |
| Phase | Deliverable | Owner | Date |
| Refinement | Research, data-source confirmation, metric definitions, design direction | PM + Design + Data | `[TBD]` |
| Handoff | Kickoff, tickets | PM + Eng | `[TBD]` |
| Execution | Development | Eng | `[TBD]` |
| Pilot | 1 pilot district | PM | `[TBD]` |
| Beta | `[TBD]` beta districts | PM | `[TBD]` |
| GA | All | All | 07/31/2026 |

## Open Questions and Assumptions

|  |  |  |  |  |
| :-: | :-: | :-: | :-: | :-: |
| Assumption / Question | Priority | How to Investigate | Answer | Status |
| What is the production source system for student scores (SIS, assessment platform, vendor)? | P0 | Eng + Data discovery | | To Do |
| What is the finalized "months of growth" formula? | P0 | Data team defines and owns | | To Do |
| What is the source of grade-level targets/benchmarks (e.g., assessment framework)? | P0 | Data team | | To Do |
| Where does the "Fill Seats" CTA route (form, email, partnerships handoff)? | P1 | PM + Partnerships | | To Do |
| Is there a real week-over-week history to power the trend indicator? | P1 | Data team | | To Do |
| Does the existing platform auth model cover district/school/grade access scoping? | P1 | Eng | | To Do |
| Do admins want absolute values or normalized "% of target" on cross-grade aggregates? | P2 | Pilot feedback | | To Do |
