# 📊 Exploratory Data Analysis (EDA) of Diabetes Risk Factors
An end-to-end clinical data analysis and visualization framework operating on 50,000 patient records. This project evaluates key physiological, demographic, and metabolic markers—specifically Blood Glucose, HbA1c, BMI, and Age—to uncover early indicators of prediabetes and diabetes onset.
---

## 📌 Table of Contents
- [Project Overview]
- [Dataset Architecture]
- [Key Methodology & Data Cleaning]
- [Tech Stack & Libraries]
- [Project Execution Phases]
- [Detailed Key Insights]
- [Future Scope]
 
## 🎯 Project Overview
Early detection of diabetes significantly improves patient outcomes and reduces long-term healthcare costs. The primary goal of this Exploratory Data Analysis (EDA) project is to rigorously clean, transform, and analyze clinical metrics to construct a clear risk-stratification profile for patients.

### **Core Objectives:**
1. Identify primary physiological drivers linked to elevated blood glucose levels.
2. Evaluate compounding risk patterns between non-modifiable factors (Age) and lifestyle factors (BMI).
3. Prepare a distribution-preserved dataset using advanced outlier handling rather than destructive row removal.

---

## 📐 Dataset Architecture
The raw dataset consists of 50,000 patient rows capturing demographic and diagnostic attributes.

| Variable Name| Data Type |Range / Description |Clinical Importance|
| :--- | :--- | :--- | :--- |
|**Age** | Numerical (Integer) | 18 - 80+ years | Key demographic risk factor |
|**BMI** | Numerical (Float) | 10.0 - 70.0+ | Measure of body composition |
|**Blood Glucose** | Numerical (Float) | 70 - 300+ mg/dL | Direct indicator of metabolic function |
|**HbA1c Level** | Numerical (Float) | 3.5% - 9.0%+ | 3-month average blood sugar levels |
|**Diabetes Status** | Categorical/Binary | 0 (non-diabetic), 1 (Diabetic) | Target variable |

---

## 🛠️ Key Methodology & Data Cleaning

### 1. Non-Destructive Outlier Handling (.clip())
Instead of dropping extreme clinical values (which reduces statistical power), an Interquartile Range (IQR) capping methodology was implemented using Pandas .clip().

* **Upper Bound:** $Q3 + 1.5 \times IQR$
* **Lower Bound:** $Q1 - 1.5 \times IQR$

'''python
# Capping extreme values to upper and lower IQR boundaries
Q1 = df['Blood_Glucose'].quantile(0.25)
Q3 = df['Blood_Glucose'].quantile(0.75)
IQR = Q3 - Q1

lower_limit = Q1 - 1.5 * IQR
upper_limit = Q3 + 1.5 * IQR

df['Blood_Glucose'] = df['Blood_Glucose'].clip(lower=lower_limit, upper=upper_limit)

### 2. Clinical Categorical Binning (pd.cut())
Continuous metrics were discretized into medical diagnostic categories to perform statistical cohort comparisons.

'''python
# Categorizing BMI into standard medical weight classes
bmi_bins = [0, 18.5, 24.9, 29.9, 100]
bmi_labels = ['Underweight', 'Normal', 'Overweight', 'Obese']
df['BMI_Category'] = pd.cut(df['BMI'], bins=bmi_bins, labels=bmi_labels)

## 💻 Tech Stack & Libraries
1. Core Language: Python 3.x
2. Data Manipulation: Pandas, NumPy
3. Static Visualizations: Matplotlib, Seaborn
4. Interactive Analytics: Plotly Express
5. Environment: JupyterLab / Jupyter Notebook

## ⚙️ Project Execution Phases
### Phase 1: Problem Framing & Structural Inspection
* Inspected dataset schema using ⁠df.info()⁠ and ⁠df.describe()⁠.
*  Validated zero missing values across all primary features.

### Phase 2: Data Preprocessing & Feature Engineering
* Capped skewed clinical features using IQR thresholds (⁠.clip()⁠).
* Binned continuous variables (⁠BMI⁠, ⁠Blood_Glucose⁠) using ⁠pd.cut()⁠.

### Phase 3: Exploratory Data Analysis (EDA)
* Generated univariate histograms and box plots to establish baseline distributions.
* Built multivariate Seaborn box plots and Plotly interactive scatter plots to isolate cross-metric relationships.

### Phase 4: Executive Insights & Reporting
* Summarized risk findings into actionable clinical recommendations.

## 💡 Detailed Key Insights
1. Primary Clinical Predictors:
Blood Glucose⁠ and ⁠HbA1c⁠ levels display the strongest direct correlation with positive diabetes diagnoses. Patients with blood glucose exceeding 140\text{     mg/dL} show a steep increase in diagnosis rate.
2. Compound Risk Factors:
Age and BMI act as compound risk multipliers. Patients in the Obese BMI category over the age of 45 represent the highest concentration of positive cases.
3. Sample Integrity Maintained:
By utilizing ⁠.clip()⁠ rather than deleting outlier rows, all 50,000 patient records were successfully preserved for cross-tabulation and statistical grouping (⁠groupby⁠/⁠pivot_table⁠).

## 🚀 Future Scope
1. Predictive Modeling: Train Machine Learning models (Logistic Regression, Random Forest, XGBoost) to predict diabetes likelihood.
2. Feature Expansion: Incorporate longitudinal patient health metrics such as blood pressure trends, physical activity levels, and family history.
