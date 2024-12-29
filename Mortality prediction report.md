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
## Results
### 1. ICU mortality prediction
The predictor distributions for survival and mortality classes overlapped, with subtle shifts in central tendencies and tails. The mean age was around 63 years, with older patients (mode around 80 years) in the mortality group (Class 1) compared to younger patients (mode around 60 years) in the survival group (Class 0), indicating higher mortality risk with age. The average ICU length of stay was 5 days, and the average time to death was 2 months.

A class imbalance was observed, with survival cases (Class 0) outnumbering mortality cases (Class 1) by 3:1, which can bias model predictions. To address this, undersampling of the majority class was applied to balance the dataset and improve prediction accuracy for the minority class. 

Without addressing the class imbalance in the dataset, all models exhibited low F1-scores, indicating poor predictive accuracy for the minority class (mortality). However, after implementing undersampling techniques to balance the dataset, significant improvements in F1-scores were observed across all models. 

HGB emerged as the best-performing model, achieving an F1-score of 0.80 on the test set. Its ROC-AUC scores of 0.94 for the training set and 0.87 for the test set demonstrate strong discriminatory power in distinguishing between survival and mortality. Additionally, HGB inherently handled missing data effectively, contributing to its robust performance. Both RF and XGB models exhibited signs of overfitting, with inflated performance metrics on the training set (1.00 for RF, 0.98 for XGB) but significantly lower metrics on the test set (0.79 for both models). This suggests limited generalisability to unseen data, making them less reliable for future predictions. GB and LR showed similar performance, with F1-scores slightly lower than HGB, however, their discriminatory power did not match that of HGB.

SHAP analysis revealed the most important predictors influencing ICU mortality risk, highlighting both positive and negative contributors. Among the top positive contributors, age emerged as the most significant factor, with older patients exhibiting a higher risk of mortality.
### 2. Weekend effect
The most frequent causes of mortality in both groups: Sepsis, pneumonia, and intracranial hemorrhage accounted for over 4% of deaths, followed by conditions such as heart failure, abdominal pain, hypotension, cardiac arrest, altered mental status, and subarachnoid hemorrhage. 

The "weekend effect" on mortality may be influenced by patient demographics. In the unadjusted Cox model, weekend admission was not significantly associated with mortality (HR: 1.06, 95% CI: 0.98–1.14, p = 0.168) whereas it was significant after being adjusted for age, gender, and ethnicity. Age had the strongest impact, with senior patients having nearly three times higher mortality risk compared to younger patients (HR: 2.86, 95% CI: 2.47–3.31, p < 0.001)

However, after proportional hazards assumption was checked, age and ethnicity violated the assumption. Stratifying the model by these variables made the weekend admission effect non-significant (HR: 1.08, 95% CI: 0.9992–1.170, p = 0.0525), suggesting that the initial association was confounded by age and ethnicity. This indicates that the "weekend effect" may be an artifact of these factors, rather than a true difference between weekend and weekday admissions.