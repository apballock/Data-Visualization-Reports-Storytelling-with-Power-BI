# Power BI – Data Visualization & Dashboard Design

**Ana Ballock** · [LinkedIn](https://linkedin.com/in/anaballock) · [GitHub](https://github.com/apballock)

---

Advanced Power BI project focused on visualization strategy, dashboard UX design, and analytical storytelling — covering chart selection logic, interactive time hierarchies, and custom tooltip architecture.

---

## Skills Demonstrated

Data storytelling · Visualization strategy · Dashboard UX design · Time-series analysis · Correlation analysis · Interactive report design · Cross-filter debugging · Business insight communication

---

## Project Structure

```text
├── Exercise 1 – Chart Selection & Visual Strategy
│   ├── Profit by Segment (Bar Chart)
│   ├── Monthly Sales Trend (Line Chart)
│   ├── Country Sales Share (Donut Chart)
│   └── Units Sold vs Profit (Scatter Plot)
├── Exercise 2 – Date Hierarchy & Drill-Down
└── Exercise 3 – Custom Tooltip Page
```

---

## Exercise 1 — Chart Selection & Executive Dashboard

Designed a four-panel executive dashboard applying deliberate chart selection logic — matching each visualization type to its analytical purpose rather than defaulting to generic visuals.

| Business Question | Visual Selected | Rationale |
|---|---|---|
| Which segment generates the most profit? | Bar Chart | Categorical comparison |
| How did sales evolve month by month? | Line Chart | Continuous time-series |
| What share of sales does each country hold? | Donut Chart | Part-to-whole contribution |
| Is there a relationship between volume and profit? | Scatter Plot | Correlation & outlier detection |

![Chart Selection Dashboard](screenshots/nivel1_ejerc1_chart_selection.png)

---

### Profit by Segment

Clustered bar chart sorted descending by Profit, surfacing a counterintuitive result: the **Enterprise** segment operated at a loss while **Government** led in profitability — despite Enterprise having significant sales activity.

Chart title written as an analytical conclusion rather than a label:
> *Government Leads Profit — Enterprise Operates at a Loss*

This framing converts the visual from a data display into an executive-ready insight.

---

### Monthly Sales Trend

Line chart plotted against the Calendar table's `MonthName` field (sorted by `MonthNumber`) to ensure chronological accuracy. The trend confirmed a strong Q4 acceleration with **October** as the peak sales month, consistent with typical end-of-year commercial patterns.

---

### Country Sales Share

Donut chart with percentage labels showing **USA as the largest contributor** to total sales. During analysis, a cross-filter interaction temporarily shifted the apparent top country to Germany — a realistic reminder that active visual selections alter aggregation context and must be accounted for when communicating findings to non-technical stakeholders.

---

### Units Sold vs Profit — Scatter Plot

Scatter plot segmented by business category, revealing that **sales volume and profitability are not correlated** in this dataset. Government clustered in the high-volume, high-profit quadrant. Enterprise landed below zero regardless of units sold — pointing to a structural pricing or cost issue independent of demand.

> *More units sold does not mean higher profit. Enterprise's losses are structural, not volumetric.*

---

## Exercise 2 — Date Hierarchy & Drill-Down Navigation

Built a three-level date hierarchy inside the Calendar table (Year → Quarter → Month) enabling users to drill through time granularities within a single visual — replacing what would otherwise require three separate charts and two additional pages.

| Level | Top Performer |
|---|---|
| Quarter | Q4 |
| Month | October |

During development, only 2014 data appeared in the hierarchy despite the dataset containing 2013 records. Root cause: a report-level filter from a prior exercise was silently restricting the full dataset. Resolved by auditing active filters — a practical example of how missing data in BI environments is often caused by filter state rather than broken relationships or incomplete sources.

**UX impact:** A single drill-down hierarchy reduces dashboard clutter, shortens time-to-insight, and supports both summary-level and granular analysis within the same view.

![Date Hierarchy Drill-Down](screenshots/nivel1_ejerc2_hierarchy.png)

---

## Exercise 3 — Custom Tooltip Page

Implemented a custom Report Page Tooltip connected to the main Segment bar chart, delivering contextual profitability and cost metrics on hover without adding visual noise to the primary dashboard surface.

### Tooltip Components

| Visual | Metric |
|---|---|
| KPI Card | Profit Margin % |
| KPI Card | Total COGS |
| Mini Chart | Sales by Product |

### Design Challenges

Custom tooltip pages in Power BI don't auto-scale to tooltip dimensions — visuals overflow boundaries and typography breaks without manual intervention. Resolved through iterative layout optimization: increased the custom page canvas, adjusted card font sizes, restructured the visual arrangement for compact rendering, and re-enabled Tooltip mode after each modification.

This is a common production challenge in enterprise dashboard development where UI/UX engineering is as critical as analytical accuracy.

### Business Insight

On hover, **Channel Partners** consistently returned the highest Profit Margin % — confirming that this segment operates with significantly greater efficiency than its sales volume alone would suggest. Lower transaction volume paired with high margin is often a signal of premium positioning or favorable cost structure.

![Custom Tooltip](screenshots/nivel1_ejerc3_custom_tooltip.png)

---

## Key Takeaways

- Chart type selection driven by analytical intent, not aesthetic preference
- Executive-ready insight titles used in place of generic chart labels
- Cross-filter behavior documented and communicated as a data literacy consideration
- Scatter plot analysis surfaced a structural profitability finding not visible in standard bar/line charts
- Drill-down hierarchy replaced three separate visuals with a single interactive component
- Custom tooltip architecture implemented with full layout optimization for production-ready rendering
