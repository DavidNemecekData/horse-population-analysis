# Data Directory: Equine Population Datasets

This directory contains the datasets used for the analysis of horse population evolution in the Czech Republic. The project works with historical time series ranging from 1921 to 2025, with forecasted values extending to 2050.

## 📂 Dataset Sources
The data is compiled from two primary official sources:
1.  **Czech Statistical Office (CSO / ČSÚ):** Historical census data (1921–2001).
2.  **Central Register of Horses (ÚEK):** Comprehensive mandatory registration data (2002–2025).

---

## 📄 File Descriptions

### 1. raw.csv
This is the original dataset as retrieved from official records. 
*   **Status:** Unprocessed.
*   **Integrity:** Contains approximately **15% missing values (NaN)**, specifically during the inter-war period and World War II (1928–1945).
*   **Columns:** `year`, `horse_count`.

### 2. clean_data.json
The final, feature-engineered dataset exported from the analytical pipeline. It contains reconstructed historical values, calculated growth metrics, and future projections.
*   **Status:** Cleaned, Interpolated, and Transformed.
*   **Format:** Optimized for programmatic access and visualization in the Manim animation engine.

---

## 📊 Data Dictionary (clean_data.json)

| Feature | Data Type | Description |
| :--- | :--- | :--- |
| **Year** | Integer | The recorded or forecasted year (1921–2050). |
| **horse_count** | Float | The original raw value from CSO/ÚEK (contains `NaN` for missing years). |
| **horse_count_linear** | Float | Reconstructed value using Linear Interpolation (for comparison). |
| **horse_count_poly_cubic**| Float | Reconstructed value using Cubic Polynomial Interpolation (for comparison). |
| **Horses** | Integer | **The primary analytical feature.** Reconstructed values using Quadratic Interpolation (1921–2025) or Forecasted values (2026–2050). Rounded to units. |
| **horse_diff** | Float | Absolute annual difference in population ($Count_{t} - Count_{t-1}$). |
| **horse_pct_change** | Float | Year-over-year percentage change in population. |
| **horse_percentage_SMA_5**| Float | 5-Year Simple Moving Average of the percentage change (used for trend smoothing). |
| **Horses_lower** | Float | Lower bound of the 80% uncertainty interval (Prophet forecast, 2026+). |
| **Horses_upper** | Float | Upper bound of the 80% uncertainty interval (Prophet forecast, 2026+). |

---

## 🛠️ Data Processing & Methodology Note

A critical structural break occurs between **2001 and 2002**. 
*   **Pre-2002:** Data represents CSO estimates and agricultural censuses.
*   **Post-2002:** Data is sourced from the centralized mandatory register, resulting in a significant administrative jump in records.

For the purpose of long-term forecasting (2026–2050), the models were calibrated primarily on the post-2003 stable growth era to ensure predictive accuracy within the modern socio-economic context.

Detailed technical implementation of the cleaning and interpolation process can be found in the [01_population_analysis.ipynb](../notebooks/01_population_analysis.ipynb) notebook.