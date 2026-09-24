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
