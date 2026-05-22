# Notebooks: Analysis & Storytelling Pipeline

This directory contains the core analytical logic and the visual storytelling engine of the project. The workflow is split into two sequential stages, designed and executed within the **Google Colab** environment to leverage cloud-based rendering resources.

## 01_population_analysis.ipynb
**Purpose:** Data cleaning, historical reconstruction, and time-series forecasting.

This notebook serves as the project's analytical backbone. It handles the transition from raw, fragmented records to a structured, feature-engineered dataset.

*   **Key Features:**
    *   **Data Imputation:** Implementation of Rolling Window Cross-Validation to test interpolation models. (Selection of Quadratic Polynomial Interpolation based on model parsimony and residual stability).
    *   **Structural Break Analysis:** Identification of the 2002 methodology shift and its isolation from organic growth trends.
    *   **Growth Metrics:** Calculation of annual percentage changes and 5-year Simple Moving Averages (SMA).
    *   **Forecasting:** Deployment of Meta's Prophet algorithm tuned for modern-era growth (2003–2050), including 80% uncertainty intervals.
    *   **Export:** Generation of `clean_data.json` used by the subsequent animation stage.

## 02_story.ipynb
**Purpose:** Programmatic video generation using the Manim library.

This notebook translates the analytical findings into a cinematic data narrative. It uses the Python library **Manim (Mathematical Animation Engine)** to render the evolution of the horse population.

*   **Key Features:**
    *   **Scene Architecture:** Code for 10 distinct animated scenes covering the introduction, historical peaks, the great collapse, recovery, and future projections.
    *   **Dynamic UI:** Implementation of live numerical counters (ValueTrackers) and animated labels.
    *   **Visual Assets:** Integration of external icons (`horse_icon.png`, `manim_logo.png`) as `ImageMobjects`.
    *   **Rendering:** Optimized for Google Colab, rendering individual scenes that are subsequently compiled in post-production.

---

## Environment & Setup

Both notebooks were developed and tested in **Google Colab**. 

### Important Notes:
1.  **Dependencies:** Ensure all libraries from the root [requirements.txt](../requirements.txt) are installed. Notebook 02 requires specific system dependencies for Manim (FFmpeg, LaTeX), which are handled within the notebook cells.
2.  **Data Pathing:** Notebook 02 depends on the `clean_data.json` produced by Notebook 01.
3.  **Drive Integration:** If running in Colab, ensure your Google Drive is mounted to access the `data/`, `images/`, and `videos/` directories.