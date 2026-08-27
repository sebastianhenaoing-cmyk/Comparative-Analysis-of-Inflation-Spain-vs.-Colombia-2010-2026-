# Comparative Analysis of Inflation: Spain vs. Colombia (2010–2026)

An exploratory analysis comparing consumer price index (CPI) and accumulated inflation dynamics between Spain and Colombia using official national statistics. This project focuses on evaluating national-level price trends and broad expenditure categories to highlight structural economic differences and recent inflationary pressures across both countries.

## Data Sources

* **Spain CPI Data:** Instituto Nacional de Estadística (INE) — Consumer Price Index series by COICOP division (`CP0` / `CP00` general classification).
* **Colombia CPI Data:** Departamento Administrativo Nacional de Estadística (DANE) — Índice de Precios al Consumidor.
* **Period analyzed:** 2010–2026.

## Tools

* **Power BI Desktop** (Power Query for ETL, DAX for custom measures).
* **DAX Engine** for dynamically filtered inflation calculations.

## Methodology

### Data Cleaning & Modeling (Power Query & DAX)
* Filtered raw data to isolate overall CPI indicators (`CP0` / `CP00` expenditure divisions) from granular sub-categories to prevent aggregation errors in average calculations.
* Resolved country-specific locale and date formatting conflicts during source ingestion.
* Applied a star-schema data architecture: a central fact table (`Fact_Indices`) linked to a dedicated date dimension (`Dim_Calendario`).

### Standardized Base Year Reindexing (Base 2015)
* To ensure accurate multi-country comparisons, historical CPI series were re-indexed to a common reference year (**Base 2015 = 100**).
* **Formula:**  
  $$\text{Reindexed CPI}_{t} = \left( \frac{\text{Raw CPI}_{t}}{\text{Average CPI}_{2015}} \right) \times 100$$
* This standardization eliminates baseline discrepancies between INE and DANE datasets, allowing direct comparison of price growth trajectories over time.

### Inflation Calculations & DAX Formulas
To measure price variations across different time horizons, three key inflation indicators were engineered in DAX:

* **1. Accumulated Inflation (Period-to-Date):**  
  Measures total price percentage change between the target period (e.g., July 2026) and the baseline period (e.g., December 2025).  
  $$\text{Accumulated Inflation} = \frac{\text{CPI}_{\text{Current Period}} - \text{CPI}_{\text{Baseline Period}}}{\text{CPI}_{\text{Baseline Period}}}$$

* **2. Annual Inflation (YoY):**  
  Measures year-over-year price change for any given month relative to the same month of the previous year.  
  $$\text{Annual Inflation (YoY)} = \frac{\text{CPI}_{t} - \text{CPI}_{t-12}}{\text{CPI}_{t-12}}$$

* **3. Category-Specific Inflation Rate:**  
  Calculates the localized price variance within specific COICOP spending divisions (Food, Housing, Transport, etc.) over selected annual windows.

### Dashboard & UX Design
* Applied an **Executive Dark Mode** layout featuring brand-aligned color coding (Red for Spain, Gold `#FCD116` for Colombia).
* Standardized custom multi-card components to display high-level KPIs alongside granular category breakdowns without visual clutter.

## Key Findings

* **Divergent Cumulative Pressure:** Colombia shows higher cumulative inflation rates compared to Spain over recent comparative intervals (e.g., ~4.94% vs. ~2.58% in the analyzed baseline window).
* **Historical Trajectory:** While both countries experienced inflationary spikes post-2020, Colombia's baseline index shows a steeper long-term slope compared to Spain’s lower-volatility trend.
* **Category Drivers:** Expenditure breakdowns reveal that essential goods—such as Housing, Utilities, and Food—serve as the main drivers of price inflation in both markets, though with varying levels of intensity.

## Dashboard

* 🔗 *[Link to interactive Power BI report]*

## Limitations

* **Reporting Timelines:** Minor release lags between INE and DANE create slight variations in the latest monthly data availability.
* **Basket Weighting Differences:** While both datasets follow standard COICOP divisions, national consumption weights differ slightly between European and Latin American methodological standards.
