# Power BI – Enterprise Data Analytics

**Ana Ballock** · [LinkedIn](https://linkedin.com/in/anaballock) · [GitHub](https://github.com/apballock)

---

End-to-end Power BI project built on a live MySQL source, covering the full analytics stack: ETL, relational modeling, DAX semantic layer, and multi-scope filter architecture.

**Stack:** Power BI Desktop · MySQL · DAX · Power Query M

**Model:** 2 fact/dimension tables · 1 Calendar dimension · 10+ DAX measures · Live database connection · Time intelligence enabled

---

## Project Structure

```
├── Level 1 – Connectors & Power Query
│   ├── MySQL Live Connection
│   ├── ETL & Custom Column Transformations
│   └── Calendar Table (DAX)
├── Level 2 – Advanced DAX
│   ├── RELATED() – Cross-table enrichment
│   ├── SUMX / AVERAGEX – Iterator functions
│   └── Centralized Measures Table
└── Level 3 – Filters & CROSSFILTER
    ├── CROSSFILTER – Bidirectional filtering
    └── Visual / Page / Report filter scopes
```

---

## Level 1 – Connectors & Power Query

### MySQL Live Connection

Replaced static flat files with a direct connection to a local MySQL database (`sales_db`), integrating the `products` and `products` tables into Power BI via MySQL Connector/NET. This establishes a production-style data source pattern where the model refreshes against the database rather than a snapshot.

![MySQL Connector](screenshots/nivel1_ejerc1_mysql_connector.png)

---

### ETL & Custom Column Transformations

Built a revenue classification column in Power Query M, segmenting transactions into High / Medium / Low tiers based on sales thresholds. During data profiling, caught a silent upstream quality issue — a leading whitespace in a column name — that was silently invalidating downstream logic. Resolved before applying the classification.

**Finding:** Polarized revenue distribution with strong high-end concentration and significant low-value volume — a signal for mid-market strategy development.

![Custom Column](screenshots/nivel1_ejerc2_custom_column.png)

---

### Calendar Table

Built a dedicated Calendar dimension using `CALENDAR()` and `ADDCOLUMNS()`, covering 2013–2014 with Year, Month Number, Month Name, Quarter, and Day of Week attributes. Linked to `financials[Date]` and configured `MonthName` to sort by `MonthNumber` for correct chronological rendering.

```dax
Calendar =
ADDCOLUMNS(
    CALENDAR(DATE(2013,1,1), DATE(2014,12,31)),
    "Year",        YEAR([Date]),
    "MonthNumber", MONTH([Date]),
    "MonthName",   FORMAT([Date], "MMMM"),
    "Quarter",     "Q" & FORMAT(QUARTER([Date]), "0"),
    "DayOfWeek",   FORMAT([Date], "dddd")
)
```

A dedicated Calendar table is a hard requirement for reliable time intelligence — without it, DAX functions like YoY and rolling averages produce incorrect results under filter context changes.

![Calendar Table](screenshots/nivel1_ejerc3_calendar_table.png)

---

## Level 2 – Advanced DAX

### RELATED() – Cross-Table Enrichment

Enriched the `sales` fact table with product attributes from the `products` dimension using `RELATED()`, keeping the model normalized rather than denormalizing the source data. Derived Product Name, Unit Price, and Total Revenue as calculated columns via the existing `product_id` relationship.

```dax
Product Name  = RELATED('sales_db products'[product_name])
Unit Price    = RELATED('sales_db products'[unit_price])
Total Revenue = 'sales_db sales'[units_sold] * 'sales_db sales'[Unit Price]
```

**Finding:** *Paseo* ranked first in total revenue, driven by a combination of unit price and transaction volume.

![RELATED Chart](screenshots/nivel2_ejerc1_related.png)

---

### SUMX / AVERAGEX – Iterator Functions

Implemented dynamic revenue aggregation using `SUMX()` and `AVERAGEX()`, evaluating `units_sold × unit_price` row-by-row across the `sales` table via `RELATED()` — the correct pattern when calculation operands live in different tables.

```dax
Total Revenue SUMX =
SUMX(
    'sales_db sales',
    'sales_db sales'[units_sold] * RELATED('sales_db products'[unit_price])
)

Avg Revenue per Sale =
AVERAGEX(
    'sales_db sales',
    'sales_db sales'[units_sold] * RELATED('sales_db products'[unit_price])
)
```

Built a Country × Category revenue matrix alongside a KPI card (Avg Revenue per Sale: **3.04K**).

**Finding:** Spain + Bikes produced the highest revenue combination, driven by unit price premium and transaction density.

![SUMX Matrix](screenshots/nivel2_ejerc2_sumx.png)

---

### Centralized Measures Table

Consolidated all DAX measures into a single `_Measures` table (underscore prefix pins it to the top of the Data pane), keeping the semantic layer discoverable and maintainable as the model scales. Covers revenue, margin, COGS, and CROSSFILTER-based measures.

Scattered measures across multiple tables are a common source of technical debt in Power BI projects — this structure prevents that from the start.

![Measures Table](screenshots/nivel2_ejerc3_measures_table.png)

---

## Level 3 – Filters & CROSSFILTER

### CROSSFILTER – Dynamic Filter Direction

Used `CROSSFILTER()` inside `CALCULATE()` to temporarily activate bidirectional filtering between `sales` and `products`, enabling a count of products with actual sales activity — a metric the default single-direction topology cannot produce.

```dax
Products with Sales =
CALCULATE(
    COUNTROWS('sales_db products'),
    CROSSFILTER(
        'sales_db sales'[product_id],
        'sales_db products'[product_id],
        BOTH
    )
)
```

**Finding:** All 5 catalog products registered sales — no inactive inventory. Bikes led in total units sold.

![CROSSFILTER](screenshots/nivel3_ejerc1_crossfilter.png)

---

### Multi-Scope Filter Architecture

Applied Power BI's three filter scopes independently to demonstrate how enterprise dashboards layer analytical constraints without duplicating datasets.

| Scope | Filter Applied | Reach |
|---|---|---|
| Visual | Sales > 500,000 | Single chart |
| Page | Country ∈ {USA, Canada, France} | All visuals on the page |
| Report | Year = 2014 | All pages in the report |

This hierarchy lets analysts enforce global reporting standards (report scope), build audience-specific pages (page scope), and surface focused KPIs (visual scope) — all within the same `.pbix` file.

![Filters](screenshots/nivel3_ejerc2_filters.png)

---

## Summary

| Area | Highlights |
|---|---|
| Data Source | Live MySQL connection, no flat files |
| ETL | Power Query M, data quality catch during profiling |
| Modeling | Normalized star schema, Calendar dimension, DAX semantic layer |
| DAX | RELATED, SUMX, AVERAGEX, CROSSFILTER, centralized measures |
| Filtering | Visual / Page / Report scope architecture |
| Business Output | Revenue segmentation, top-product ranking, geographic breakdown |
