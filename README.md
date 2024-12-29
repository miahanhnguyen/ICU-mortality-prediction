# ICU mortality prediction
## Aim:
1. Using machine learning models to predict mortality based on the first 24 hours ICU data.
2. Investigate the weekend effect on mortality.
## Background:
Research has shown that data from the initial 24-hour ICU period provides critical early indicators of patient outcomes, as it captures the patient's initial physiological response to critical care. Various machine learning models have been explored for ICU mortality prediction. Robust approaches to handling missing data and outliers are essential in real-world ICU datasets.

The “weekend effect” hypothesis suggests that ICU admissions during weekends are associated with a higher mortality risk. Patients with serious illnesses have a higher risk of mortality for weekend admissions. Differences in staffing levels, availability of specialists, and variability in care practices may contribute to these outcomes. This analysis uses the Cox proportional hazards model to analyze the effect of weekend admission while adjusting for key demographic predictors.
## Methods
### 1. ICU mortality prediction
Data preprocessing:
- Missing data
- Outliers
- EDA
- Imputation
Model testing:
- Logistic Regression
- Random Forest
- Gradient Boosting Tree
- XGBoost
- Histogram Gradient Boosting
Performance metrics:
- F1-score
- AUC-ROC
- Confusion matrix
To assess the contribution of individual predictors: using SHAP (SHapley Additive ExPlanations) - a game-theory-based approach that provides interpretable attributions for each feature.
### 2. Weekend effect
Data selection:
- Patients admitted through the emergency room, without transfers or referrals.
- Weekend admission: a binary variable distinguishing between weekend admission (Saturday and Sunday) and weekday admission (Monday to Friday).
Statistical analysis: Cox proportional hazards models
- Unadjusted model: Assessing the effect of weekend admission on mortality alone.
- Adjusted model: Controlling for potential confounders. 
