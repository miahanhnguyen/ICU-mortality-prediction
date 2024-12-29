# ICU mortality prediction
## Aim:
- Using machine learning models to predict mortality based on the first 24 hours ICU data.
- Investigate the weekend effect on mortality.
## Background:
Research has shown that data from the initial 24-hour ICU period provides critical early indicators of patient outcomes, as it captures the patient's initial physiological response to critical care. Various machine learning models have been explored for ICU mortality prediction. Robust approaches to handling missing data and outliers are essential in real-world ICU datasets.

The “weekend effect” hypothesis suggests that ICU admissions during weekends are associated with a higher mortality risk. Patients with serious illnesses have a higher risk of mortality for weekend admissions. Differences in staffing levels, availability of specialists, and variability in care practices may contribute to these outcomes (5). This study will explore whether this effect is reproducible in MIMIC data while accounting for confounders such as age, gender and ethnicity that may differ between weekdays and weekends. To address this question, we employed the Cox proportional hazards model to analyze the effect of weekend admission while adjusting for key demographic predictors. 
