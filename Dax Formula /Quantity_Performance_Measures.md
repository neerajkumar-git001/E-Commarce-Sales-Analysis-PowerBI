# Quantity Performance & Growth Measures

This document contains the DAX measures used to analyze total quantity, year-to-date performance, prior-year comparisons, and year-over-year quantity growth. These measures support business growth tracking and sales volume analysis in the E-Commerce Sales Dashboard.

---

## 1. Total Quantity

```dax
Total Quantity = 
SUM('Ecommarce data'[order_quantity])
```

**Description:** Calculates the total quantity of products sold by summing the quantity for each order. This measure serves as the foundation for evaluating sales volume and business growth.

---

## 2. YTD Quantity

```dax
YTD Quantity =
TOTALYTD(
    [Total Quantity],
    'Calender Table'[Date]
)
```

**Description:** Calculates the cumulative quantity sold from the beginning of the year up to the selected date. This measure helps track year-to-date sales volume and monitor business growth throughout the year.

---

## 3. PYTD Quantity

```dax
PYTD Quantity =
CALCULATE(
    [Total Quantity],
    DATESYTD(
        SAMEPERIODLASTYEAR(
            'Calender Table'[Date]
        )
    )
)
```

**Description:** Calculates the quantity sold during the equivalent year-to-date period of the previous year. This measure enables historical volume comparisons and supports year-over-year quantity growth analysis.

---

## 4. YOY Quantity Growth %

```dax
YOY Quantity Growth % =
DIVIDE(
    [YTD Quantity] - [PYTD Quantity],
    [PYTD Quantity],
    0
)
```

**Description:** Calculates the percentage change in year-to-date quantity compared with the previous year's equivalent period. This measure helps evaluate changes in sales volume, identify growth trends, and understand product demand.

**Formula Logic:**

- Positive value: Quantity growth compared with the previous year.
- Negative value: Quantity decline compared with the previous year.
- Zero: No change or zero returned when the previous-year quantity denominator is zero.

---

## 5. Quantity Icon

```dax
Quantity Icon =
VAR Positive_Icon = UNICHAR(9650)

VAR Negative_Icon = UNICHAR(9660)

VAR result =
    IF(
        [YOY Quantity Growth %] >= 0,
        Positive_Icon,
        Negative_Icon
    )

RETURN result
```

**Description:** Generates a visual indicator based on the YOY Quantity Growth percentage. An upward triangle (▲) represents positive or zero growth, while a downward triangle (▼) represents negative growth. This measure improves KPI readability and helps users quickly identify changes in sales volume.

**Business Purpose:** Supports visual KPI indicators in the dashboard to communicate quantity growth direction and highlight changes in product sales volume.
