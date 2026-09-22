# Profit Performance & Growth Measures

This document contains the DAX measures used to analyze total profit, year-to-date performance, prior-year comparisons, and year-over-year profit growth. These measures support business profitability tracking and growth analysis in the E-Commerce Sales Dashboard.

---

## 1. Total Profit

```dax
Total Profit =
SUM('Ecommarce data'[profit_per_order])
```

**Description:** Calculates the total profit generated from all orders by summing the profit earned per order. This measure serves as the foundation for evaluating business profitability and financial performance.

---

## 2. YTD Profit

```dax
YTD Profit =
TOTALYTD(
    [Total Profit],
    'Calender Table'[Date]
)
```

**Description:** Calculates the cumulative profit from the beginning of the year up to the selected date. This measure helps track year-to-date profitability and monitor business financial growth throughout the year.

---

## 3. PYTD Profit

```dax
PYTD Profit =
CALCULATE(
    [Total Profit],
    DATESYTD(
        SAMEPERIODLASTYEAR(
            'Calender Table'[Date]
        )
    )
)
```

**Description:** Calculates the profit accumulated during the equivalent year-to-date period of the previous year. This measure enables historical profitability comparisons and supports year-over-year profit growth analysis.

---

## 4. YOY Profit Growth %

```dax
YOY Profit Growth % =
DIVIDE(
    [YTD Profit] - [PYTD Profit],
    [PYTD Profit],
    0
)
```

**Description:** Calculates the percentage change in year-to-date profit compared with the previous year's equivalent period. This measure helps evaluate profitability growth, identify financial performance changes, and understand business profit trends.

**Formula Logic:**

- Positive value: Profit growth compared with the previous year.
- Negative value: Profit decline compared with the previous year.
- Zero: No change or zero returned when the previous-year profit denominator is zero.

---

## 5. Profit Icon

```dax
Profit Icon =
VAR Positive_Icon = UNICHAR(9650)

VAR Negative_Icon = UNICHAR(9660)

VAR result =
    IF(
        [YOY Profit Growth %] >= 0,
        Positive_Icon,
        Negative_Icon
    )

RETURN result
```

**Description:** Generates a visual indicator based on the YOY Profit Growth percentage. An upward triangle (▲) represents positive or zero growth, while a downward triangle (▼) represents negative growth. This measure improves KPI readability and helps users quickly identify changes in profitability.

**Business Purpose:** Supports visual KPI indicators in the dashboard to communicate profit growth direction and highlight changes in business financial performance.
