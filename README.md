# synthea-idc10
# Emergency Department (ED) Prediction using XGBoost
This project aims to predict whether a patient encounter requires emergency department (ED) care using structured healthcare data. It leverages machine learning techniques (especially XGBoost) and ICD-10 classification to assist clinical decision-making.

# Project Goals
Predict whether a patient case is likely to result in an emergency visit.

Understand key features contributing to ED predictions (feature importance).

Provide patient-level insights: ED probability, gender ratio, ICD-10 codes and their descriptions.

# Model Overview
We used the following models:

✅ XGBoost Classifier (best overall accuracy and feature interpretability)

🌲 Random Forest Classifier (as a benchmark)

📊 Baseline logistic model (for comparison)

Metrics evaluated:

Precision, Recall, F1-score

Confusion Matrix

ROC Curve & AUC Score

# Dataset Description
The dataset includes over 700,000 patient encounters, enriched with the following features:
- DESCRIPTION       | Procedure description,
- ENCOUNTERCLASS    | Type of encounter (inpatient, outpatient, etc.)
- GENDER, AGE, CITY	| Patient demographics
- BASE_ENCOUNTER_COST , TOTAL_CLAIM_COST , PAYER_COVERAGE	| Financial metrics
- ICD10CM , ICD-10 | diagnosis code
- ED_label	Binary outcome: 1 = ED needed, 0 = not needed

We also use an external reference table (ICD10_Reference.csv) to map ICD-10 codes to human-readable descriptions.

# Feature Importance (XGBoost)
Top predictive features include:

ENCOUNTERCLASS_urgentcare

BASE_ENCOUNTER_COST

ENCOUNTERCLASS_outpatient


# Demo Output
Example: For Well child visit (procedure):

=== Prediction Summary ===
Description: Well child visit (procedure)
Total patients: 43,950
Predicted ED visits: 76.82%
Male ratio: 49.50%
Female ratio: 50.50%

=== ICD-10 Codes (Predicted ED cases) ===
Z76.89: Persons encountering health services in other circumstances
Z20.822: Contact with and (suspected) exposure to COVID-19
...
# Project Structure
├── data/
│   ├── df1_merge.csv            # Merged encounter & patient data
│   ├── ICD10_Reference.csv      # ICD-10 → description mapping
├── notebooks/
│   ├── ed_prediction_pipeline.ipynb
├── images/
│   ├── xgboost_feature_importance.png
├── utils/
│   ├── model_utils.py           # Training, evaluation, plotting
│   ├── description_insight.py   # ICD-10 level summarization
├── README.md
⚙️ Setup Instructions
bash
Copy
Edit
# Recommended environment
Python 3.8+

# Install required packages
pip install -r requirements.txt
🚀 How to Run
Open notebooks/ed_prediction_pipeline.ipynb

Execute all cells to load data, train model, and display ED analysis

Use the helper function:

python
Copy
Edit
analyze_description_case_en(
    description_input="Well child visit (procedure)",
    df_source=df1_merge,
    df_icd10_reference=df3
)
👨‍⚕️ Credits
Developed as part of a healthcare analytics initiative to assist physicians in classifying patient urgency and ED triage potential using structured EHR data and machine learning.
