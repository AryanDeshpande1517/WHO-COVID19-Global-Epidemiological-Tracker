# 📊 DAX Measures Documentation
This document outlines the DAX measures used in the **WHO COVID-19 Global Epidemiological Tracker** project.

The measures are grouped into:

- Time Intelligence  
- Core Epidemiological Metrics  
- Rolling Averages & Smoothing  
- Healthcare & Severity Metrics  
- Vaccination Intelligence  

## 📅 Time Intelligence

### Master Calendar
Creates a dedicated date table for consistent time-series modeling.

```DAX
Master Calendar = 
CALENDAR(
    DATE(2020, 1, 1), 
    DATE(2025, 12, 31)
)
```

### Quarter
Generates quarter labels (Q1–Q4) for time-based aggregation.

```DAX
Quarter = "Q" & QUARTER('Master Calendar'[Date])
```

## 🦠 Core Epidemiological Metrics

### Total Confirmed Cases
Aggregates total reported confirmed cases.

```DAX
Total Confirmed Cases = 
SUM('WHO_Cases'[New_cases])
```

### Total Deaths
Aggregates total reported deaths.

```DAX
Total Deaths = 
SUM('WHO_Cases'[New_deaths])
```

### Case Fatality Rate
Measures mortality ratio relative to confirmed infections.

```DAX
Case Fatality Rate = 
DIVIDE([Total Deaths], [Total Confirmed Cases], 0)
```

### Recovery Rate
Estimates survival ratio complementing fatality rate.

```DAX
Recovery Rate = 
1 - [Case Fatality Rate]
```

## 📈 Rolling Averages & Smoothing

### New Cases (Smooth)
Raw case aggregation used for baseline trend comparison.

```DAX
New Cases (Smooth) = 
SUM('WHO_Cases'[New_cases])
```

### New Cases (7-Day Avg)
Calculates 7-day rolling average to smooth reporting volatility.

```DAX
New Cases (7-Day Avg) = 
AVERAGEX(
    DATESINPERIOD(
        'Master Calendar'[Date], 
        LASTDATE('Master Calendar'[Date]), 
        -7, 
        DAY
    ),
    CALCULATE(SUM('WHO_Cases'[New_cases]))
)
```

### New Deaths (7-Day Avg)
7-day smoothed mortality trend.

```DAX
New Deaths (7-Day Avg) = 
AVERAGEX(
    DATESINPERIOD(
        'Master Calendar'[Date], 
        LASTDATE('Master Calendar'[Date]), 
        -7, 
        DAY
    ),
    CALCULATE(SUM('WHO_Cases'[New_deaths]))
)
```

## 🏥 Healthcare & Severity Metrics

### Weekly Hospital Admissions
Measures weekly new hospital admissions.

```DAX
Weekly Hospital Admissions = 
SUM('WHO_Hospitals'[Covid_new_hospitalizations_last_7days])
```

### Weekly ICU Admissions
Tracks ICU burden across regions.

```DAX
Weekly ICU Admissions = 
SUM('WHO_Hospitals'[Covid_new_icu_admissions_last_7days])
```

## 💉 Vaccination Intelligence

### Total Vaccinated
Aggregates cumulative vaccinated individuals (first dose).

```DAX
Total Vaccinated = 
SUMX(
    VALUES('WHO_Vax'[COUNTRY]), 
    CALCULATE(MAX('WHO_Vax'[COVID_VACCINE_ADM_1D]))
)
```

### People Vaccinated (1 Dose)
Country-level vaccination aggregation.

```DAX
People Vaccinated (1 Dose) = 
SUMX(
    VALUES('WHO_Vax'[COUNTRY]), 
    CALCULATE(MAX('WHO_Vax'[COVID_VACCINE_ADM_1D]))
)
```

### Total Population
Extracts country population reference for rate calculations.

```DAX
Total Population = 
MAX('WHO_Vax'[POPULATION])
```

### Vaccination Rate %
Average vaccination coverage percentage.

```DAX
Vax Rate % = 
AVERAGEX(
    VALUES('WHO_Vax'[COUNTRY]), 
    CALCULATE(MAX('WHO_Vax'[COVID_VACCINE_COV_1D]))
)
```

### Global Vaccination Rate %
Global coverage across historical records.

```DAX
Global Vax Rate % = 
AVERAGEX(
    VALUES('WHO_Vax_Historical'[COUNTRY]), 
    CALCULATE(MAX('WHO_Vax_Historical'[COVID_VACCINE_COV_TOT_CPS]))
)
```

### Total Doses Administered
Cumulative administered doses globally.

```DAX
Total Doses Administered = 
SUMX(
    VALUES('WHO_Vax_Historical'[COUNTRY]), 
    CALCULATE(MAX('WHO_Vax_Historical'[COVID_VACCINE_ADM_TOT_DOSES]))
)
```

### Total Fully Vaccinated
Fully vaccinated individuals (complete primary series).

```DAX
Total Fully Vaccinated = 
SUMX(
    VALUES('WHO_Vax_Historical'[COUNTRY]), 
    CALCULATE(MAX('WHO_Vax_Historical'[COVID_VACCINE_ADM_TOT_CPS]))
)
```

### Total People Vaccinated
Total individuals receiving at least one dose.

```DAX
Total People Vaccinated = 
SUMX(
    VALUES('WHO_Vax_Historical'[COUNTRY]), 
    CALCULATE(MAX('WHO_Vax_Historical'[COVID_VACCINE_ADM_TOT_A1D]))
)
```

## 📌 Notes

- A dedicated calendar table ensures proper time intelligence modeling.
- Rolling averages are used to smooth reporting irregularities.
- `SUMX` with `VALUES` ensures country-level deduplication for cumulative metrics.
- Measures were iteratively refined during dashboard development.
- The final model reflects validated measures actively used in visuals.