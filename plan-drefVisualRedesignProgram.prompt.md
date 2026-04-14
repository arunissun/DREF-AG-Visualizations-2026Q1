## Plan: DREF Visual Redesign Program

### 1. Program Intent

This program will rebuild the analytical core of the DREF presentation so that the visuals are numerically defensible, visually coherent, and better aligned to the 2026 Q1 story. The target presentation remains PowerPoint, so every chart should be produced as a clean standalone asset that can be placed into slides without needing dashboard interaction.

The delivery model stays hybrid.

1. Python remains the source-of-truth layer for data extraction, cleaning, validation, metric definition, and Python-native chart development.
2. D3 remains part of the plan and should stay intact as the presentation-oriented rendering layer for visuals that benefit from tighter composition, richer annotation, or more bespoke storytelling.
3. PowerPoint remains the final assembly environment where narrative bullets, caveats, and slide-level commentary can sit outside the chart when that improves readability.

### 2. Core Objective

The main objective is not just to redraw the existing slides. It is to improve how the slides explain the 2026 Q1 story.

That means each visual should do four things clearly:

1. Show the 2026 Q1 value.
2. Show the immediate comparison to 2025 Q1 where relevant.
3. Show enough historical context to indicate whether the 2026 Q1 result is a step change, continuation, or anomaly.
4. Surface the intended analytical takeaway, not just the underlying numbers.

### 3. Analytical Scope And Data Rules

The default analytical scope is the DREF family drawn from `ALL_DATA`.

1. Base `Appeal Type` filter: `DREF`, `i-DREF`, `a-DREF`.
2. Exclude silent and cancelled records from the base scope unless a slide explicitly documents a different treatment.
3. Use Q1 logic consistently for comparison slides: January to March approvals only, with 2026 capped at `2026-03-31`.
4. Treat `EA`, `EAP`, and `s-EAP` as explicit slide-level exceptions, not as part of the default scope.
5. Normalize naming, dates, and numeric fields before any chart logic is built.

Supporting definitions:

1. `EA` = Emergency Appeal.
2. `EAP` = Early Action Protocol.
3. `s-EAP` = Simplified Early Action Protocol.

### 4. What Has Been Validated Already

The existing workbook structure is sufficient to support most of the redesign.

1. `ALL_DATA` contains the main variables required for slide redesign: pillar, region, weather classification, natural versus non-natural classification, hazard type, crisis categorization, approved CHF, dates, targeted people, and approval timing.
2. The current analytical deck focus is slides 2 to 10.
3. Several existing visuals are effectively static images or layout-bound objects and are better rebuilt from first principles rather than incrementally edited.
4. Two logic-sensitive areas need explicit caution:
   1. Slide 4: `crisis_categorization` is incomplete and must be reconciled with workbook logic before any final publication claim is made.
   2. Slide 7: Non-ODA classification should use workbook reference logic, most likely through the `ODA Countries` sheet, rather than an ad hoc inference.

### 5. Visual System Requirements

Python and D3 outputs must look like one family, even if they are built in different tools.

Lock the following before visual polishing begins:

1. Color system for pillars, regions, thresholds, and annotation states.
2. Typography hierarchy for titles, subtitles, axes, labels, and callouts.
3. Number formatting for CHF, percentages, counts, and durations.
4. Axis conventions and gridline treatment.
5. Annotation style for deltas, caveats, and key takeaways.
6. Slide-safe aspect ratios and export sizes for PowerPoint placement.

The visual system should prioritize presentation clarity over dashboard density.

#### 5A. Flourish-Inspired House Style

All future figures should follow a Flourish-inspired presentation standard. The goal is not to copy a specific Flourish template literally, but to adopt the same visual grammar: clear hierarchy, restrained clutter, direct labeling, and narrative-led emphasis.

Mandatory styling rules:

1. Use a clean, presentation-first layout with strong title hierarchy, short subtitle framing, and generous whitespace.
2. Prefer light backgrounds, subtle gridlines, and low-noise axes so the data carries the emphasis rather than the frame.
3. Prefer direct labels, end labels, count badges, or in-chart annotations over detached legends whenever the chart type allows it.
4. Keep palettes disciplined: one coherent set of categorical colors, one highlight color for emphasis, and one alert color for caveats or threshold breaches.
5. Use narrative annotation deliberately, similar to Flourish story-style emphasis: short takeaways, axis highlights, milestone labels, and focused callouts instead of long explanatory blocks.
6. Every chart should feel reveal-ready. Even when exported as a static PowerPoint asset, the structure should read as if it could be explained step by step.
7. Avoid decorative complexity that does not improve interpretation. If a chart element cannot justify itself analytically, remove it.

#### 5B. Visual Consistency Rules

The current prototypes exposed avoidable inconsistency. The next iteration must correct that.

1. One background standard only. Do not mix separate notebook-level style systems that make outputs look like two different decks.
2. One pillar color mapping only, used everywhere. Response and anticipatory colors must never swap between figures.
3. Legends must never collide with titles, subtitles, or plot areas.
4. Edge annotations must be positioned with sufficient chart margins so labels are never clipped.
5. If historical context is needed to interpret 2026 Q1, it should be included rather than implied.
6. Every priority figure should carry a clear analytical takeaway, not just a metric display.

### 6. Delivery Architecture

#### Python Track

Python should remain notebook-first.

Primary responsibilities:

1. Read and clean workbook data.
2. Enforce the agreed analytical scope.
3. Produce slide-level metric tables and validation extracts.
4. Recreate published deck values wherever possible.
5. Generate Python-native chart alternatives for all priority slides.
6. Export stable intermediate datasets for downstream use.

Implementation format:

1. Jupyter notebooks for data prep, data validation, exploratory analysis, and Python chart development.

#### D3 Track

The D3 track remains intact and is not being removed from the plan.

Primary responsibilities:

1. Build the more presentation-driven variants of selected slides.
2. Handle layered composition where notebook visuals are analytically correct but visually too rigid.
3. Improve chart storytelling through tighter annotation, labeling, and layout control.
4. Produce export-ready static assets and optional HTML review versions.

Recommended D3 focus slides:

1. Slide 2 for KPI plus comparative composition treatment.
2. Slide 6 for composition plus trend integration.
3. Slide 8 for ranked hazard storytelling.
4. Slide 9 for timeliness annotation and emphasis.
5. Slide 10 for timeline composition and sequencing.

Implementation format:

1. JavaScript source files for both D3-side wrangling and D3-side visual rendering.

#### PowerPoint Layer

PowerPoint remains the final narrative composition layer.

1. Charts should be exported as SVG and PNG.
2. Narrative text, caveats, and interpretation can remain outside the chart if that produces a cleaner slide.
3. The chart itself should carry the main analytical claim, but not every sentence of explanation.

### 7. Program Sequencing

The sequence should remain redesign-first, expansion-second.

1. Finalize the data contract for slides 2 to 10.
2. Lock the shared visual system across Python and D3.
3. Rebuild the existing analytical slides.
4. Validate each rebuilt slide numerically against the deck and source data.
5. Only after the existing analytical slides are approved, move into the five new figures.

This order reduces rework and prevents new exploratory visuals from distracting from the core deck rebuild.

### 8. Slide-By-Slide Redesign Brief

#### Slide 2: Headline KPI Summary

Purpose:
Present the top-level 2026 Q1 story quickly while preserving the 2025 Q1 comparator and protocol context.

Analytical requirements:

1. Total approved CHF.
2. Allocation count.
3. Supported operations.
4. Targeted people.
5. Country count.
6. Protocol context for EAP and s-EAP as an explicit contextual layer only.

Design direction:

1. Keep a headline KPI device, but make it denser and more comparative than a loose grid of cards.
2. Show 2026 Q1 values with explicit 2025 Q1 baselines, not only percent delta.
3. Pair the KPI block with a pillar composition comparison so the size story and the mix story sit together.
4. Explicitly explain the CHF versus targeted-people divergence if those metrics move in opposite directions.
5. The comparative pillar treatment should show both composition and absolute scale, either through a paired view or a longer historical comparison.

Preferred implementation split:

1. Python for validated metric generation and quick prototypes.
2. D3 for the final composition if a more controlled KPI layout is needed.

#### Slide 3: Core Q1 Comparison

Purpose:
Show how the core DREF metrics changed from 2025 Q1 to 2026 Q1 without forcing unrelated metrics into one scale.

Design direction:

1. Use a mirrored, slope, or diverging comparison format rather than a dense table replacement.
2. Preserve like-for-like reading across metrics.
3. Add enough visual structure that directionality is clear immediately.
4. Avoid any color-position ambiguity between years.
5. Add compact historical context where possible so the comparison does not feel like an isolated two-point snapshot.
6. Year-color mapping must remain fixed even when the 2026 value is lower than 2025.

Implementation note:

1. Keep this slide focused on DREF-family comparison unless a broader mixed-instrument story is intentionally chosen and documented.

#### Slide 4: Crisis Category Mix

Purpose:
Show the composition of crisis categorization over time while being explicit about data coverage limitations.

Design direction:

1. Use a stacked proportional trend as the primary device.
2. Add a secondary summary view only if it clarifies the 2026 Q1 position.
3. Make coverage caveats visible, not buried.
4. Ensure year continuity is explicit. If a year has zero values it should render as zero, not disappear.
5. Category coverage and category absence should be visually understandable so missing categories are not mistaken for zero-impact categories.

Critical condition:

1. Do not finalize this slide until crisis categorization logic is reconciled against workbook rules and exclusions.

#### Slide 5: Localization

Purpose:
Show current localization performance against target in a slide-native, easy-to-read format.

Design direction:

1. Keep the target-based framing.
2. Use a compact benchmark device such as radial gauges or bullet-style forms only if the target line remains unmistakable.
3. Preserve a clear distinction between aggregate and pillar-level results.
4. Add a direct gap-to-target expression so the reader can tell immediately whether each value is above or below target.
5. Keep pillar colors consistent with the rest of the deck.

Critical condition:

1. The current metric is not yet reproducible from raw data and must remain explicitly labeled as provisional until the logic is confirmed.

#### Slide 6: Hazard Composition

Purpose:
Explain how the allocation mix changes across weather classification and natural versus non-natural classification.

Design direction:

1. Move beyond parallel share bars if a single integrated composition plus trend view can be built cleanly.
2. Keep historical perspective so 2026 Q1 is not read in isolation.
3. Use small multiples only if they are truly easier to read than a more integrated solution.
4. If two classification views are kept, each must add distinct analytical value and carry its own legible labels or annotations.
5. Include total-value context so shares are not read without scale.

Preferred implementation split:

1. Python for data shaping and prototype structure.
2. D3 for the final treatment if a more expressive multi-layer composition is needed.

#### Slide 7: Non-ODA Allocations

Purpose:
Show both the value and the share of Non-ODA allocations in a like-for-like Q1 comparison across years.

Design direction:

1. Use a dual-axis bar-line format or a very clean two-panel alternative.
2. Keep 2026 Q1 case annotations for named countries.
3. Show the overall denominator clearly so the Non-ODA share is not abstract.
4. Rebuild this figure from first principles if necessary; correct year positioning on the x-axis is non-negotiable.
5. The visual must show both value and share without any ambiguity in time placement.

Critical condition:

1. This slide depends on clean Non-ODA logic and should not be finalized until that logic is locked.

#### Slide 8: Hazard Ranking

Purpose:
Rank the major 2026 Q1 hazard categories while preserving region composition and operation counts.

Design direction:

1. Keep ranked horizontal bars.
2. Preserve region sub-segments where they genuinely add insight.
3. Include count badges or a second metric cue so total CHF is not the only story.
4. Consider a direct signal for year-over-year change if it can be added without clutter.
5. Add a stronger cue for intensity, such as per-operation context, when a hazard has unusually high CHF with few operations.

Preferred implementation split:

1. Python for validated ranking data and prototypes.
2. D3 for the final storytelling version if region labeling, badges, or annotations need more control.

#### Slide 9: Timeliness

Purpose:
Show whether approval timing is improving, worsening, or becoming more volatile, with 2026 Q1 as the focal point.

Design direction:

1. Use a connected-dot or line-based trend that keeps 2023 to 2026 readable at a glance.
2. Add fast-track and cash-advance annotations where they strengthen interpretation.
3. Use median context where means are vulnerable to outliers, especially for `days_in_hq`.
4. Use a meaningful target band or threshold emphasis, not a background treatment that obscures the analytical message.
5. Explicitly call out the 2025 spike and the 2026 improvement if those remain the dominant story.

Preferred implementation split:

1. Python for metric derivation and validation.
2. D3 for a more refined annotation-heavy final version if needed.

#### Slide 10: Cross-Instrument Response Timeline

Purpose:
Show the sequence of approvals across countries and instruments in a crisis-response narrative.

Design direction:

1. Keep the Gantt-style timeline.
2. Make sequencing, duration, and instrument type legible without overloading the bars.
3. Use annotation to highlight same-day versus multi-day approvals where relevant.
4. Avoid placing dense labels inside short bars when outside placement is clearer.
5. Same-day approvals should be labeled in a human-readable way, not as visually awkward `0d` duration markers.
6. Crisis-start framing and approval timing must be visually consistent so the reference line does not appear to contradict the events.

Scope rule:

1. This slide can intentionally mix `EA` and `i-DREF` if the narrative is explicitly cross-instrument and the exception is documented.

Preferred implementation split:

1. Python for sequencing logic and baseline timeline output.
2. D3 for final presentation quality if label control and event framing require it.

### 9. Review And Validation Workflow

#### 9A. Review-Driven Change Directives

The current prototype review should now be treated as a formal design input, not just commentary. The following issues are mandatory for correction in the next visual iteration.

Priority corrections:

1. Slide 7 must be rebuilt because the current year positioning is broken.
2. Slide 3 must remove any year-color confusion, especially in declining metrics such as targeted people.
3. Slides 6 and 8 must resolve legend-title collisions.
4. Slide 9 must fix clipped annotations and replace the overly broad shaded background with a more meaningful threshold cue.
5. Slide 10 must move dense labels out of bars where legibility is compromised.

Cross-cutting directives:

1. Add historical context wherever the interpretation of 2026 Q1 depends on multi-year comparison.
2. Add short analytical callouts where the key conclusion is not obvious from the chart alone.
3. Use direct labeling more aggressively to match the Flourish-style storytelling approach.
4. Resolve all style mismatches between the implementation-phase notebooks and the new-figures notebook.

#### 9B. New Figures Review Directives

The new figures phase also needs to reflect the review findings.

1. Figure A should annotate the 2026 Q1 peak and clarify which regions drive the change.
2. Figure B ranking should carry an operation count or other secondary cue, and the trend panel should avoid overly smooth interpolation that implies nonexistent intermediate movement.
3. Figure C should treat tiny anticipatory values carefully so labels remain legible, and the operations variant may need an indexed-view alternative if relative change matters more than raw scale.
4. Figure D should more clearly foreground the spike-to-improvement story in approval timing.
5. Figure E must improve contrast and text legibility, especially on lighter cells.

#### 9C. Validation Workflow

Every redesigned slide must pass numeric validation before visual polishing is treated as complete.

For each slide:

1. Confirm the filter logic and slide-level scope.
2. Reproduce the underlying metric table in Python.
3. Compare Python outputs to the published deck values where the published deck has numbers.
4. Resolve discrepancies before signing off the design.
5. Document any remaining caveats directly in the notebook and, where needed, in the slide notes.

### 10. Prioritization

Execution priority should stay pragmatic.

1. Lowest-risk and fastest wins: Slides 2, 3, 5.
2. Medium complexity: Slides 8, 9, 10.
3. Highest dependency on workbook logic: Slides 4, 7.
4. Highest compositional design complexity: Slide 6.

### 11. New Figures Phase

The five new figures remain in scope, but only after the redesigned analytical slides are stable.

1. Figure A: Regional allocation evolution as a stacked area chart.
2. Figure B: Disaster-type ranking plus year-over-year trend panel.
3. Figure C: Pillar growth over time with CHF and operation count.
4. Figure D: Timeliness improvement slope chart extended back to 2022.
5. Figure E: Regional allocation heatmap with CHF and operation toggle or paired comparison view.

These figures should be treated as an expansion phase, not a prerequisite for rebuilding the current deck.

### 12. Final Deliverables

The final program should produce the following outputs:

1. Cleaned and validated processed datasets from the workbook.
2. Notebook-based Python figure versions for every redesigned slide.
3. D3-based presentation-driven versions for the selected slides where D3 adds value.
4. Slide-ready SVG and PNG exports.
5. A documented metric contract for every slide and every new figure.
6. A short record of unresolved caveats for any slide where the data logic is still provisional.

### 13. Key Decisions

1. `ALL_DATA` remains the primary source of truth wherever feasible.
2. Supporting sheets are only used when business logic cannot be cleanly recovered from raw rows.
3. The base visual scope is DREF-family only unless a slide explicitly documents an exception.
4. Python-based wrangling and Python-based visuals remain notebook-based.
5. D3-based wrangling and D3-based visuals remain part of the plan and continue to be implemented in JavaScript source files.
6. Existing slide redesigns come before the five new figures.
7. Final visual choices should optimize for PowerPoint readability, not dashboard interaction.
8. Analytical interpretation matters as much as chart construction; every chart should support a slide-level takeaway, not just display numbers.
