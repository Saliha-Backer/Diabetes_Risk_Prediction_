# 📊 Exploratory Data Analysis of Diabetes Risk Factors
This repository provides an end-to-end framework for analyzing clinical and demographic risk factors associated with diabetes onset across 50,000 patient records.It features non-destructive data cleaning, clinical feature engineering, and interactive visualizations.
---

## 📌 Table of Contents
- [Project Overview]
- [Key Features & Methodology]
- [Tech Stack]
- [Project Workflow]
- [Executive Insights]
- 
  ---

## 🎯 Project Overview
The objective of this project is to perform an end-to-end exploratory data analysis (EDA) to uncover how key indicators like Age, BMI, Blood Glucose, and HbA1c interact to signal diabetes risk.

- **Dataset Size:** 50,000 patient records
- **Data Quality:** Zero missing values, non-destructive IQR outlier capping via .clip()
- **Feature Engineering:** Categorical clinical binning via pd.cut()
  ---
## 🛠️ Tech Stack & Tools
-**Language:** Python
- **Data Analytics:** Pandas, NumPy
- **Visualizations:** Matplotlib, Seaborn (Static Baseline), Plotly Express (Interactive)
- **Environment:** JupyterLab / Jupyter Notebook
- 
  ---
## ⚙️ Project Workflow
### Phase 1: Problem Definition & Data Inspection
- Initial data loading, structure inspection (df.info(), df.describe()), and duplicate validation.

### Phase 2: Preprocessing & Feature Engineering
- **Outlier Capping:** Applied Interquartile Range (IQR) boundary capping with .clip() on continuous features to prevent distortion without dropping patient records.
- **Clinical Binning:** Segmented continuous BMI and Blood Glucose values into standard medical diagnostic categories using pd.cut().
  
### Phase 3: Exploratory Data Analysis (EDA)
- Constructed univariate, bivariate, and multivariate distribution charts across 10+ visualizations.
- Leveraged interactive Plotly hover elements alongside Seaborn statistical probability plots.

### Phase 4: Executive Insights
- Summarized key risk drivers, compounding age-BMI relationships, and strategic screening recommendations.

## 💡 Executive Insights
1. **Primary Indicators:** Blood Glucose and HbA1c exhibit the strongest individual correlation with diabetes status.
2. **Compound Risk:** High BMI combined with advancing Age multiplies overall metabolic risk significantly.
3. **Data Integrity:** Sample size (N=50,000) was 100% preserved through boundary capping.
