# Profit Margin Performance & Growth Measures

This document contains the DAX measures used to analyze profit margin, year-to-date profitability, prior-year comparisons, and year-over-year profit margin growth. These measures support business profitability tracking and growth analysis in the E-Commerce Sales Dashboard.

---

## 1. Profit Margin %

```dax
Profit Margin % =
DIVIDE(
    [Total Profit],
    [Total sales],
    0
)
```

**Description:** Calculates the profit margin percentage by dividing total profit by total sales. This measure evaluates how efficiently the business converts sales revenue into profit and supports profitability analysis.

---

## 2. YTD Profit Margin %

```dax
YTD Profit Margin % =
DIVIDE(
    [YTD Profit],
    [YTD Sale],
    0
)
```

**Description:** Calculates the year-to-date profit margin by dividing cumulative profit by cumulative sales. This measure helps track profitability performance and monitor changes in business margins throughout the year.

---

## 3. PYTD Profit Margin %

```dax
PYTD Profit Margin % =
DIVIDE(
    [PYTD Profit],
    [PYTD Sales],
    0
)
```

**Description:** Calculates the profit margin for the equivalent year-to-date period of the previous year. This measure enables historical profitability comparisons and supports year-over-year margin analysis.

---

## 4. YOY Profit Margin Growth %

```dax
YOY Profit Margin Growth % =
DIVIDE(
    [YTD Profit Margin %] - [PYTD Profit Margin %],
    [PYTD Profit Margin %],
    0
)
```

**Description:** Calculates the percentage change in year-to-date profit margin compared with the previous year's equivalent period. This measure helps evaluate changes in profitability efficiency and identify business margin growth or decline.

**Formula Logic:**

- Positive value: Profit margin increased compared with the previous year.
- Negative value: Profit margin decreased compared with the previous year.
- Zero: No change or zero returned when the previous-year profit margin denominator is zero.

---

## 5. Profit Margin Icon

```dax
Profit Margin Icon =
VAR Positive_Icon = UNICHAR(9650)

VAR Negative_Icon = UNICHAR(9660)

VAR result =
    IF(
        [YOY Profit Margin Growth %] >= 0,
        Positive_Icon,
        Negative_Icon
    )

RETURN result
```

**Description:** Generates a visual indicator based on the YOY Profit Margin Growth percentage. An upward triangle (▲) represents positive or zero margin growth, while a downward triangle (▼) represents negative margin growth. This measure improves KPI readability and helps users quickly identify changes in profitability efficiency.

**Business Purpose:** Supports visual KPI indicators in the dashboard to communicate profit margin growth direction and highlight changes in business profitability.
