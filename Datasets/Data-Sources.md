# 📂 Data Sources Documentation
This document outlines the official datasets used in the **WHO COVID-19 Global Epidemiological Tracker** project.

All data was obtained directly from the World Health Organization (WHO) COVID-19 Data Portal.

## 🌍 Primary Data Source

**WHO COVID-19 Data Portal**  
https://data.who.int/dashboards/covid19/data  

The WHO portal provides globally reported COVID-19 statistics submitted by Member States.

## 📊 Datasets Used

Multiple downloadable datasets were integrated into this project, including:

1. **Confirmed Cases and Deaths**
   - Daily / weekly reported new cases
   - Daily / weekly reported new deaths
   - Country-level reporting

2. **Hospital & ICU Admissions**
   - Weekly new hospitalizations
   - Weekly new ICU admissions
   - Healthcare burden indicators

3. **Vaccination Data**
   - Total doses administered
   - First dose coverage
   - Complete primary series coverage
   - Historical vaccination progression

4. **Population & Coverage Metrics**
   - Country population reference
   - Vaccination coverage percentages

## 🧠 Data Interpretation Notes

- WHO reporting transitioned from daily to weekly reporting in August 2023.
- Some countries report intermittently or retrospectively adjust data.
- Hospital and ICU data availability varies by country.
- Vaccination data reflects official national submissions to WHO.
- Case Fatality Rate is calculated using confirmed reported cases and deaths, not estimated infections.

Rolling averages are used within the dashboard to smooth reporting volatility.

## ⚖️ Licensing & Usage

Data is sourced directly from the WHO public data portal.

WHO data is provided for:
- Public health monitoring
- Research
- Educational use
- Analytical interpretation

Raw datasets are **not redistributed** in this repository.

To reproduce this project:

1. Download datasets directly from the WHO portal.
2. Load into Power BI.
3. Apply transformations and measures as documented in the `Scripts/` directory.

## 📌 Disclaimer

This dashboard is intended for educational and analytical purposes only.

All data rights belong to:
**World Health Organization (WHO)**

Interpretations and visualizations are independently created and do not represent official WHO policy statements.