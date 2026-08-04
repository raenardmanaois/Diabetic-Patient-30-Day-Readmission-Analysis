# Diabetic-Patient-30-Day-Readmission-Analysis
Tools: Tableau Public for data cleaning Dataset: Diabetes 130-US Hospitals for Years 1999-2008 (UCI Machine Learning Repository)

Overview

Hospital readmissions within 30 days are a key quality and cost metric in healthcare; they're tied to Medicare reimbursement penalties and are widely used as a proxy for gaps in care coordination and discharge planning. This project explores which patient and encounter-level factors are associated with 30-day readmission risk among diabetic patients, using a real, publicly available clinical dataset spanning 130 US hospitals from 1999–2008.

The Data

The original dataset contained 101,766 inpatient encounters across 50 variables, including patient demographics, diagnoses, lab results, medications, and visit history.

Data cleaning steps:

Excluded 2,423 encounters where the patient was discharged due to death or transferred to hospice care, since these encounters cannot be meaningfully assessed for readmission risk. This left 99,343 encounters in the final analysis.
Standardized missing values (originally coded as ?) across all fields.
Dropped the weight column, which was 97% missing and unusable.
Preserved missingness as a meaningful category where clinically relevant — for example, missing lab results (A1Cresult, max_glu_serum) were recoded as "Not Tested" rather than dropped, since a missing result typically means the test wasn't ordered, not that data was lost.
Mapped raw ICD-9 diagnosis codes into readable clinical categories (Diabetes, Circulatory, Respiratory, Injury, etc.) for interpretability.
Created a simplified binary target variable, Readmitted_Within_30Days, from the original three-category readmission field, to focus specifically on the 30-day window most relevant to hospital quality metrics.

Key Findings

1. Diagnosis type matters — diabetes and injury carry the highest risk. Patients whose primary diagnosis was diabetes had the highest 30-day readmission rate of any category (~13%), followed closely by injury-related admissions (~12.5%). Categories like musculoskeletal and respiratory diagnoses showed the lowest readmission rates (~9.5–10%). This suggests that diagnosis complexity and the chronic, ongoing management diabetes requires may play a larger role in readmission risk than diagnosis category alone would suggest.

2. Age is a weaker predictor than expected. Readmission risk was low among pediatric patients but jumped sharply by young adulthood. From there, it remained relatively flat — roughly 10–13% — across all adult age groups, including the oldest patients in the dataset. This was a notable finding: age alone does not appear to strongly differentiate readmission risk once a patient reaches adulthood, which runs counter to the common assumption that older patients are consistently at higher risk. (Note: the youngest adult age bracket has a smaller sample size than others, so that specific spike should be interpreted with some caution.)

3. Length of stay shows the clearest relationship with readmission. Readmission risk climbed fairly steadily with length of stay, roughly doubling from ~8% for one-day stays to ~14–15% for stays of 8–10 days. This could reflect that longer stays are a marker of greater illness severity to begin with, or that extended hospitalization itself introduces additional risk (e.g., deconditioning, hospital-acquired complications). The data can't distinguish between these explanations on its own.

Limitations & Next Steps

This analysis is descriptive, not predictive; each factor (diagnosis, age, length of stay) was examined independently, so it isn't possible to say from these charts alone which factor matters most when the others are held constant. A natural next step would be a multivariate model (e.g., logistic regression) incorporating these and other variables (number of medications, prior emergency visits, chronic disease count) to identify the strongest independent predictors of readmission and better inform where hospital intervention resources would have the greatest impact.

About This Project

This project was built as part of my transition into healthcare analytics, combining a biology background and clinical research experience with hands-on data cleaning, visualization, and analytical storytelling skills. It reflects the kind of question; "what drives a key hospital quality metric, and where should limited intervention resources go" that population health and clinical data analyst roles are built around.
