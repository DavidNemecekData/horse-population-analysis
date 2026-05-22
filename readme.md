# Equine Population in the Czech Republic: Interpolation & Forecasting

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)       
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)       
![Prophet](https://img.shields.io/badge/Prophet-FF694B?style=for-the-badge&logo=facebook&logoColor=white)   
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=google-colab&logoColor=white)   
![Manim](https://img.shields.io/badge/Manim-000000?style=for-the-badge&logo=python&logoColor=white)

## Quick Links & Visual Storytelling
Access the core outputs of this project:
* **[Animated Data Story (YouTube)](https://youtu.be/qD14eS9jWHM)** – A visual narrative of population shifts (1921–2025).
* **[Population Analysis Notebook](./notebooks/01_population_analysis.ipynb)** – Data cleaning, interpolation testing, and forecasting.
* **[Manim Animation Script](./notebooks/02_story.ipynb)** – Source code for the mathematical animation.

---

## Project Overview
This project analyzes the evolution of the horse population in the Czech Republic over the last century (1921–2025) and projects its development up to 2050. The analysis navigates complex historical data gaps and a fundamental shift in the horse's role within society—from an essential agricultural engine to a sports and companion animal.

**The Data Challenge:** The historical time series was interrupted by significant data gaps (15%) during the World War periods and a major **structural break in 2002**. This break was caused by a change in census methodology (transitioning from CSO estimates to the Central Register of Horses/ÚEK).

### Core Objectives:
1. **Analyze Population Dynamics:** Identify and quantify major shifts in horse counts.
2. **Reconstruct Missing History:** Deploy and test mathematical interpolation to fill gaps in the 1921–1945 period.
3. **Analyze Structural Breaks:** Isolate administrative methodology changes from organic population growth.
4. **Long-term Forecasting:** Generate a robust estimate of population trends up to 2050.
5. **Technical Communication:** Utilize high-end animation (Manim) to present findings to non-technical stakeholders.

---

## Final Output Preview
Below are the core visualizations representing the project's key analytical findings.

### 1. Historical Context & Milestones
A long-term perspective of the horse population (1921–2025) mapped against major socio-political eras. This chart visualizes how historical events like WWII and the post-1948 collectivization directly influenced the collapse of traditional equine dependency.
![Historical Context](./images/historical_context.png)

### 2. Population vs. Annual Growth Rate
This dual-axis visualization highlights the growth dynamics and the year-over-year percentage change. It clearly isolates the **2002 structural break**, where the jump in records reflects a shift in registration methodology rather than a biological increase in the population.
![Population and Growth](./images/population_and_growth.png)

### 3. Long-term Forecast to 2050
The final projection combining the reconstructed historical data with the Prophet forecasting model. The dashed line represents the baseline scenario for the next 25 years, complemented by an **80% uncertainty interval** to account for potential trend variability.
![History and Forecast](./images/history_and_forecast.png)

---

## Technical Execution

### 1. Data Cleaning & Interpolation Strategy
Missing data was reconstructed by testing multiple models using **Rolling Window Cross-Validation** (5-year blocks). 
* **Model Selection:** Both cubic and quadratic polynomial interpolations yielded highly comparable results during cross-validation.
* **Decision Logic:** Although the cubic model showed marginally lower MAE and RMSE values, I opted for the **Quadratic model**. Following the principle of parsimony, the simpler model was preferred as it offers superior stability and mitigates the risk of overfitting historical noise.
* **Residual Analysis:** This choice is validated by the residual distribution, which is centered around zero without significant skew or systematic patterns, ensuring a reliable reconstruction of the inter-war and WWII periods.

### 2. Exploratory Data Analysis (EDA)
* **The Peaks:** The population reached two distinct historical maximums in **1927 (456k)** and **1946 (450k)**, driven by agricultural and military necessity.
* **The Collapse:** A sharp, 35-year decline started in 1947, leading to a historical nadir in **1995 (only 18k horses)**. This 96% drop is a direct consequence of agricultural collectivization and rapid mechanization.
* **The Modern Recovery:** Since 1998, the trend has reversed. The current population (2025) stands at approximately **110,000**, representing a stable recovery phase where horses serve sport and recreational purposes.

### 3. Forecasting Layer (Prophet)
Forecasting was implemented using **Meta's Prophet** algorithm. To ensure accuracy, the model was trained exclusively on the 2003–2025 period to reflect the modern registration methodology.
* **Uncertainty Intervals:** The forecast includes an **80% uncertainty interval** to represent the range of probable outcomes.
* **2050 Projection:** The baseline scenario predicts a continued growth trend, reaching approximately **175,000 head** by 2050.
* **Model Validation:** Systematic tuning of the `changepoint_prior_scale` (optimal at 0.05) ensured the model captures the trend without being hyper-sensitive to year-over-year noise.

### 4. Mathematical Animation (Manim)
The final storytelling was executed using the **Manim (Mathematical Animation Engine)**. This script animates the historical curve, highlights specific peaks and decline periods, and visualizes the forecast uncertainty.

---

## Project Structure
* **[data/](./data/)**: Raw historical data and the final processed JSON dataset.
* **[notebooks/](./notebooks/)**: Data science workflow and Manim animation scripts.
* **[images/](./images/)**: Key visualizations used in this documentation.
* **[videos/](./videos/)**: The final rendered video (with and without audio).
* **[docs/](./docs/icons/)**: Icons and visual assets used for the animation.

---

## Environment & Reproducibility
* **Runtime:** The analysis and Manim animations were developed and executed in **Google Colab**, utilizing its cloud resources for rendering.
* **Dependencies:** Key libraries include `prophet`, `manim`, `pandas`, and `scikit-learn`. 
* **Setup:** All required packages are listed in [requirements.txt](./requirements.txt).