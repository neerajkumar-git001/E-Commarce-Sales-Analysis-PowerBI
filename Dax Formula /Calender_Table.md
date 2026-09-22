
# Calendar Table Measures

This document contains the DAX calculated table and calculated columns used to create the Calendar table. The table serves as the primary date dimension for enabling time intelligence calculations, filtering, and business growth trend analysis across the report.

---

## 1. Calendar Table

```dax
Calender Table =
CALENDAR(
    MIN('Ecommarce data'[order_date]),
    MAX('Ecommarce data'[order_date])
)
```

**Description:** Creates a continuous calendar table from the minimum to the maximum order date in the E-Commerce dataset, providing a structured date dimension for time-based analysis and business growth tracking.

---

## 2. Year

```dax
Year =
YEAR('Calender Table'[Date])
```

**Description:** Extracts the year from each date to support annual sales comparisons, year-over-year growth analysis, and yearly business performance reporting.

---

## 3. Month Number

```dax
Month No =
MONTH('Calender Table'[Date])
```

**Description:** Extracts the numeric month (1–12) to support chronological sorting, monthly filtering, and accurate sales growth trend analysis.

---

## 4. Month Name

```dax
Month name =
FORMAT('Calender Table'[Date], "mmm")
```

**Description:** Converts each date into an abbreviated month name (e.g., Jan, Feb, Mar) to improve dashboard readability and support monthly sales performance and business growth trend reporting.

**Power BI Tip:** Sort `Month name` by `Month No` to display months in chronological order instead of alphabetical order.
