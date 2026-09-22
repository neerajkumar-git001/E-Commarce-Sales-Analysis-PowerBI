
# Sales Performance & Growth Measures

This document contains the DAX measures used to analyze total sales, year-to-date performance, prior-year comparisons, and year-over-year sales growth. These measures support business performance tracking and growth analysis in the E-Commerce Sales Dashboard.

---

## 1. Total Sales

```dax
Total sales =
SUM('Ecommarce data'[sales_per_order])
```

**Description:** Calculates the total sales revenue by summing the sales amount for each order. This measure serves as the foundation for evaluating overall business performance and sales growth.

---

## 2. YTD Sales

```dax
YTD Sale =
TOTALYTD(
    [Total sales],
    'Calender Table'[Date]
)
```

**Description:** Calculates the cumulative sales from the beginning of the year up to the selected date. This measure helps track year-to-date business performance and monitor sales growth throughout the year.

---

## 3. PYTD Sales

```dax
PYTD Sales =
CALCULATE(
    [Total sales],
    DATESYTD(
        SAMEPERIODLASTYEAR(
            'Calender Table'[Date]
        )
    )
)
```

**Description:** Calculates the sales accumulated during the equivalent year-to-date period of the previous year. This measure enables historical performance comparisons and supports year-over-year sales growth analysis.

---

## 4. YOY Sales Growth %

```dax
YOY Sales Growth % =
DIVIDE(
    [YTD Sale] - [PYTD Sales],
    [PYTD Sales],
    0
)
```

**Description:** Calculates the percentage change in year-to-date sales compared with the previous year's equivalent period. This measure helps evaluate business growth, identify sales performance changes, and understand year-over-year revenue trends.

**Formula Logic:**

- Positive value: Sales growth compared with the previous year.
- Negative value: Sales decline compared with the previous year.
- Zero: No change or zero returned when the previous-year sales denominator is zero.

---

## 5. Sales Icon

```dax
Sales Icon =
VAR Positive_Icon = UNICHAR(9650)

VAR Negative_Icon = UNICHAR(9660)

VAR result =
    IF(
        [YOY Sales Growth %] >= 0,
        Positive_Icon,
        Negative_Icon
    )

RETURN result
```

**Description:** Generates a visual indicator based on the YOY Sales Growth percentage. An upward triangle (▲) represents positive or zero growth, while a downward triangle (▼) represents negative growth. This measure improves KPI readability and helps users quickly identify sales performance direction.

**Business Purpose:** Supports visual KPI indicators in the dashboard to communicate sales growth direction and highlight changes in business performance.
