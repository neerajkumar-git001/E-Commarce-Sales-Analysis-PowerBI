# Orders Performance & Growth Measures

This document contains the DAX measures used to analyze total orders, year-to-date performance, prior-year comparisons, and year-over-year order growth. These measures support business growth tracking and order volume analysis in the E-Commerce Sales Dashboard.

---

## 1. Total Orders

```dax
Total Orders =
DISTINCTCOUNT('Ecommarce data'[order_id])
```

**Description:** Calculates the total number of unique orders using the order ID. This measure helps evaluate business activity, track order volume, and monitor overall growth in customer purchases.

---

## 2. YTD Orders

```dax
YTD Orders =
TOTALYTD(
    [Total Orders],
    'Calender Table'[Date]
)
```

**Description:** Calculates the cumulative number of unique orders from the beginning of the year up to the selected date. This measure helps track year-to-date order performance and monitor business growth throughout the year.

---

## 3. PYTD Orders

```dax
PYTD Orders =
CALCULATE(
    [Total Orders],
    DATESYTD(
        SAMEPERIODLASTYEAR(
            'Calender Table'[Date]
        )
    )
)
```

**Description:** Calculates the number of unique orders during the equivalent year-to-date period of the previous year. This measure enables historical order volume comparisons and supports year-over-year order growth analysis.

---

## 4. YOY Order Growth %

```dax
YOY Order Growth % =
DIVIDE(
    [YTD Orders] - [PYTD Orders],
    [PYTD Orders],
    0
)
```

**Description:** Calculates the percentage change in year-to-date orders compared with the previous year's equivalent period. This measure helps evaluate changes in order volume, identify growth trends, and understand customer purchasing activity.

**Formula Logic:**

- Positive value: Order growth compared with the previous year.
- Negative value: Order decline compared with the previous year.
- Zero: No change or zero returned when the previous-year order denominator is zero.

---

## 5. Order Icon

```dax
Order Icon =
VAR Positive_Icon = UNICHAR(9650)

VAR Negative_Icon = UNICHAR(9660)

VAR result =
    IF(
        [YOY Order Growth %] >= 0,
        Positive_Icon,
        Negative_Icon
    )

RETURN result
```

**Description:** Generates a visual indicator based on the YOY Order Growth percentage. An upward triangle (▲) represents positive or zero growth, while a downward triangle (▼) represents negative growth. This measure improves KPI readability and helps users quickly identify changes in order volume.

**Business Purpose:** Supports visual KPI indicators in the dashboard to communicate order growth direction and highlight changes in business performance.
