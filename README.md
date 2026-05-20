# Level 1 — Chart Selection & Advanced Visuals

## Analytical Skills Demonstrated

- Data storytelling
- Visualization strategy
- Dashboard UX design
- Cross-filter debugging
- Time-series analysis
- Correlation analysis
- Interactive report design
- Business insight communication

---

# Exercise 1 — Choosing the Right Chart

## Business Goal

This exercise focused on one of the most important dashboard design skills in Power BI: selecting the appropriate visualization for the business question being analyzed.

Instead of building visuals mechanically, the objective was to understand the analytical purpose behind each chart type and how different visual structures influence interpretation and decision-making.

| Business Need            | Recommended Visual |
| ------------------------ | ------------------ |
| Compare categories       | Bar Chart          |
| Analyze trends over time | Line Chart         |
| Show proportions         | Donut Chart        |
| Analyze correlation      | Scatter Plot       |

The final page was designed as a mini executive dashboard named **Chart Selection**, combining four analytical perspectives into a single report view.

---

## Chart 1 — Profit by Segment (Bar Chart)

### Business Question

> Which business segment generates the most profit?

### Visual Choice

A **Clustered Bar Chart** was selected because bar charts are highly effective for comparing categorical values side by side.

### Configuration

| Area   | Field   |
| ------ | -------- |
| Y Axis | Segment  |
| X Axis | Profit   |

The chart was sorted descending by Profit.

### Key Insight

The analysis revealed an unexpected result:

- The **Enterprise** segment operated at a loss
- The **Government** segment generated the highest positive profit

This immediately highlighted an important business principle:

> High sales volume does not automatically translate into profitability.

To strengthen executive storytelling, the chart title was intentionally written as an insight rather than a generic label:

> **Government Leads Profit — Enterprise Operates at a Loss**

This transforms the visual from a simple chart into an analytical conclusion.

---

## Chart 2 — Monthly Sales Trend (Line Chart)

### Business Question

> How did sales evolve month by month?

### Visual Choice

A **Line Chart** was selected because continuous time-series analysis is best represented through trend lines.

### Configuration

| Area   | Field     |
| ------ | --------- |
| X Axis | MonthName |
| Y Axis | Sales     |

The Calendar table created previously ensured months appeared in proper chronological order.

### Key Insight

The trend analysis revealed strong sales acceleration during Q4.

October showed the highest sales peak, confirming a typical end-of-year commercial growth pattern.

Suggested storytelling title:

> **Sales Peak in Q4 — Strongest Commercial Period**

---

## Chart 3 — Country Sales Share (Donut Chart)

### Business Question

> What percentage of total sales does each country represent?

### Visual Choice

A **Donut Chart** was selected because the objective was to analyze contribution to the total.

### Configuration

| Area   | Field   |
| ------ | ------- |
| Legend | Country |
| Values | Sales   |

Detail labels were configured to display percentages.

### Important Learning Moment — Cross Filtering

At one point during the analysis, Germany briefly appeared as the largest sales contributor.

After clearing the selection from another visual, the values changed and the USA returned to the top position.

This behavior occurred because of Power BI’s cross-filtering interaction between visuals.

### Key Insight

Final validated result:

> USA represents the largest percentage of total sales.

This became an important analytical lesson because visual interactions can temporarily alter conclusions if report consumers are not attentive to active filters and selections.

---

## Chart 4 — Units Sold vs Profit (Scatter Plot)

### Business Question

> Is there a relationship between units sold and profit?

### Visual Choice

A **Scatter Plot** was selected because it is ideal for identifying correlations, clusters, and outliers.

### Configuration

| Area   | Field      |
| ------ | ---------- |
| X Axis | Units Sold |
| Y Axis | Profit     |
| Legend | Segment    |

### Key Insight

The scatter plot generated one of the strongest analytical findings of the exercise.

Observations included:

- Government appeared with both high sales volume and high profitability
- Enterprise appeared below zero with negative profitability
- Other segments clustered within moderate performance ranges

### Business Interpretation

> More units sold does not necessarily mean higher profit.

The Enterprise segment demonstrated structural profitability issues independent of sales volume, suggesting possible pricing or operational cost inefficiencies.

README insight:

> Government leads in both volume and profitability, while Enterprise generates losses regardless of sales volume — indicating a structural pricing or cost issue within that segment.

This type of insight is commonly expected from executive dashboards and analytical reporting environments.

---

## Problems Encountered & Solutions

| Problem | Cause | Solution |
|---|---|---|
| Germany briefly appeared as top sales country | Cross-filter interaction between visuals | Cleared visual selection to restore full dataset |
| Scatter plot interpretation became confusing | Multiple clusters overlapped visually | Used segment legend to separate patterns |
| Enterprise negative profit initially seemed incorrect | Assumption that high sales always imply positive profit | Validated dataset behavior and confirmed intended loss-making scenario |

---

## README Answers

### Which chart was hardest to configure and why?

The scatter plot was the most challenging because correlation analysis requires interpreting both axes simultaneously while also identifying clusters, outliers, and segment behaviors.

### In the scatter plot, do segments with more units sold always generate higher profit?

No. The Enterprise segment generated negative profit despite significant sales volume, demonstrating that higher volume does not guarantee profitability.

### What percentage of total sales does the USA represent?

The USA represents the largest share of total sales in the donut chart analysis.

---

## Files Generated

| File | Description |
|---|---|
| `nivel1_ejerc1_chart_selection.png` | Dashboard containing all four visualizations |

---

# Exercise 2 — Date Hierarchy & Drill-Down

## Business Goal

The objective of this exercise was to create an interactive time hierarchy allowing users to navigate dynamically between:

- Year
- Quarter
- Month

Instead of building separate visuals for each granularity level.

This is considered a professional Power BI modeling practice because it improves user experience, reduces dashboard clutter, and enables more flexible exploratory analysis.

---

## Building the Date Hierarchy

Inside the Calendar table, a hierarchy named **Date Hierarchy** was created with the following structure:

| Level | Field |
|---|---|
| 1 | Year |
| 2 | Quarter |
| 3 | MonthName |

---

## Important Learning Moment — Missing Years

Initially, only the year 2014 appeared in the visual.

This created confusion because the dataset also contained records from 2013.

### Root Cause

The report-level filter created during the previous exercise was still active and restricting the entire report to 2014 only.

This became a realistic business intelligence debugging scenario:

> Sometimes missing data is caused by hidden filters rather than broken relationships or incomplete datasets.

After validating the relationships and testing drill-down behavior, the hierarchy functioned correctly.

---

## Drill-Down Analysis

Using the drill controls inside the visual:

- Year expanded into Quarter
- Quarter expanded into Month

The strongest sales period identified was:

| Level | Top Performer |
|---|---|
| Quarter | Q4 |
| Month | October |

### Business Insight

Sales accelerated significantly toward the end of the year, peaking in October before stabilizing.

This pattern strongly suggests seasonal commercial behavior.

---

## UX & Dashboard Design Insight

One hierarchy replaced what otherwise would require:

- One yearly chart
- One quarterly chart
- One monthly chart

This dramatically improves dashboard usability because users can explore multiple time granularities interactively without navigating across multiple pages or visuals.

---

## Problems Encountered & Solutions

| Problem | Cause | Solution |
|---|---|---|
| Only one year appeared in the hierarchy | Existing report-level filter restricted data to 2014 | Validated filters and tested drill-down behavior |
| Difficulty locating Data View | UI navigation confusion | Identified the correct Power BI side-panel icon |
| Concern that hierarchy was incomplete | Drill-down was not expanded | Used the expand-all drill functionality |

---

## README Answers

### Which quarter has the highest sales?

Q4 generated the highest sales.

### Which month within that quarter performs best?

October was the top-performing month.

### How does drill-down improve UX compared to having three separate charts?

Drill-down enables users to navigate multiple time granularities inside a single visual, reducing dashboard clutter while creating a more interactive analytical experience.

---

## Files Generated

| File | Description |
|---|---|
| `nivel1_ejerc2_hierarchy.png` | Month-level drill-down visualization |

---

# Exercise 3 — Custom Tooltip Page

## Business Goal

This exercise introduced one of the most professional dashboard design techniques available in Power BI:

> Custom Tooltip Pages

Instead of overcrowding dashboards with excessive visuals, tooltip pages provide contextual details only when users hover over specific report elements.

This keeps dashboards visually clean while still supporting deeper analytical exploration.

---

## Building the Tooltip Page

A dedicated page named **Tooltip Detail** was created and configured as:

| Setting | Value |
|---|---|
| Page Type | Tooltip |
| Tooltip Mode | Enabled |

The page automatically resized to tooltip dimensions.

---

## Tooltip Components

The tooltip included:

| Visual | Purpose |
|---|---|
| Profit Margin % Card | Profitability analysis |
| Total COGS Card | Cost analysis |
| Small Sales by Product Chart | Product-level breakdown |

---

## Major Learning Moment — Tooltip Formatting

This exercise introduced one of the most common real-world Power BI design challenges:

### Manual Tooltip Layout Design

Initially:

- Visuals were oversized
- Cards overflowed outside the page boundaries
- Text became difficult to read after resizing

### Root Cause

Power BI does not automatically adapt visual layouts to tooltip dimensions.

As a result, manual formatting adjustments became necessary.

### Solution Applied

Several layout optimizations were implemented:

- Increased custom tooltip page dimensions
- Reduced card font sizes
- Rearranged visuals into a compact layout
- Re-enabled tooltip mode after customization

This reinforced an important professional lesson:

> Dashboard development is not only analytics — it also involves UI/UX engineering and layout optimization.

---

## Applying the Tooltip

The tooltip page was connected to the main Segment chart through:

| Setting | Value |
|---|---|
| Tooltip Type | Report Page |
| Tooltip Page | Tooltip Detail |

Hovering over the bars dynamically updated the tooltip content based on the selected segment.

---

## Key Business Insight

Tooltip analysis revealed:

> Channel Partners had the highest Profit Margin percentage.

This reinforced earlier profitability findings from previous exercises.

### Business Interpretation

Despite lower sales volume, Channel Partners operated with significantly higher efficiency and profitability.

---

## Problems Encountered & Solutions

| Problem | Cause | Solution |
|---|---|---|
| Visuals exceeded tooltip boundaries | Tooltip pages use small dimensions by default | Increased custom page size |
| Card text became unreadable | Font scaling did not adjust automatically | Reduced font sizes manually |
| Formatting options were difficult to locate | Power BI UI organization | Explored formatting sections systematically |
| Tooltip behavior broke after resizing | Tooltip mode was disabled during customization | Re-enabled Tooltip page mode |

---

## README Answers

### Which segment has the highest Profit Margin % when hovering?

Channel Partners.

### How can custom tooltips replace an extra report page?

Custom tooltips provide contextual details dynamically on hover, reducing dashboard clutter and minimizing the need for additional drill-through or supporting report pages.

---

## Files Generated

| File | Description |
|---|---|
| `nivel1_ejerc3_custom_tooltip.png` | Main visual displaying custom tooltip interactions |
