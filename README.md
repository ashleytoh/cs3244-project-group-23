# Enhancing Financial Inclusion through Fair and Predictive Credit Models
CS3244 Group 23


## Table of Contents
- [Project Overview](#project-overview)
  - [Motivation](#motivation)
  - [Problem Statement](#problem-statement)
- [Datasets](#datasets)

- [Setup Instructions](#setup-instructions)
- [Repository Structure and Workflow](#repository-structure-and-workflow)
  - [Directory Structure](#directory-structure)
  - [Recommended Order of Review](#recommended-order-of-review)
- [Acknowledgements](#acknowledgements)
##  Project Overview
### Motivation
Traditional credit approval systems rely on rigid, rule-based criteria. These models often:
- Reject creditworthy individuals
- Approve risky applicants
- Perform poorly in volatile economies

Moreover, many machine learning models prioritize accuracy without addressing fairness — leading to systemic exclusion of various groups.

### Problem Statement
Our project aims to build a credit approval model that balances accuracy and fairness, allowing financial institutions to make ethical, data-driven decisions while promoting financial inclusion.



## Datasets

We utilised a [credit card dataset](https://www.kaggle.com/datasets/rikdifos/credit-card-approval-prediction) for our project. This contains two datasets linked by a common client `ID`:

### `application_record.csv` – Personal and financial information  
Each row represents a loan application.

| Feature | Values | Explanation |
|---------|--------|-------------|
| ID | Integer | Loan Application identifier. Foreign key linking to credit_record.csv. |
| CODE_GENDER | M, F | Gender of the applicant. |
| FLAG_OWN_CAR | 0, 1 | Whether the applicant owns a car. |
| FLAG_OWN_REALTY | 0, 1 | Whether the applicant owns a property. |
| CNT_CHILDREN | Integer | Number of children. |
| AMT_INCOME_TOTAL | Float | Annual income of the applicant. |
| NAME_INCOME_TYPE | Categorical | Type of income (e.g., Working, Commercial associate, Pensioner, etc.). |
| NAME_EDUCATION_TYPE | Categorical | Highest education level attained. |
| NAME_FAMILY_STATUS | Categorical | Marital status. |
| NAME_HOUSING_TYPE | Categorical | Living arrangement (e.g., Rented apartment, House / apartment). |
| DAYS_BIRTH | Integer | Applicant's age in days (negative = counted backwards from today). |
| DAYS_EMPLOYED | Integer | Employment length in days (negative = currently employed, positive = jobless). |
| FLAG_MOBIL | 0, 1 | Whether a mobile phone is available. |
| FLAG_WORK_PHONE | 0, 1 | Whether a work phone is available. |
| FLAG_PHONE | 0, 1 | Whether a phone is available. |
| FLAG_EMAIL | 0, 1 | Whether an email is available. |
| OCCUPATION_TYPE | Categorical | Applicant's occupation. |
| CNT_FAM_MEMBERS | Float | Number of family members.|

---
<br>

### `credit_record.csv` – Monthly credit history  
Each row reflects an applicant’s loan status in a specific month.


| Feature | Values | Explanation |
| --- | --- | --- |
| ID | Integer | Unique Client Identifier: Foreign Key to link records to application_record.csv |
| MONTHS_BALANCE | 0, -1, -2, ... | 0 = current month, -1 = previous, etc. |
| STATUS | 0-5, C, X | 0 = 1-29 days overdue, 1 = 30-59, ..., 5 = >150 days, C = paid off, X = no loan |
---

## Setup Instructions

Ensure that you have [Python 3.10.6](https://www.python.org/downloads/release/python-3106/) installed.

### 1. Clone the repository:
In your terminal, enter the following command to clone the repository. Afterwards, `cd` into the project directory.
   ```bash
   git clone https://github.com/your-username/cs3244-project-group-23.git
   cd cs3244-project-group-23
   ``````

### 2. Create your virtual environment:
   ```bash
   python3 -m venv venv
 ````````

### 3. Activate your virtual environment
**MacOS:**
   ```bash
   source venv/bin/activate
   ```
**Windows:**
   ```bash
    venv\Scripts\activate  
   ```
### 4. Install dependencies
   ```bash
    pip install -r requirements.txt
   ```



##  Repository Structure and Workflow
### Directory Structure
```plaintext
CS3244-PROJECT-GROUP-23/
├── baseline_models/
│   └── baseline_models.ipynb 
├── data/
│   ├── processed/
│   │   ├── cleaned_applications.csv # Cleaned version of raw application data (produced from `data_preprocessing/data_cleaning.ipynb`)
│   │   ├── cleaned_credit_records.csv # Cleaned version of raw credit records (produced from `data_preprocessing/data_cleaning.ipynb`)
│   │   ├── test_set.csv # Test set used to evaluate model performance (produced from `data_preprocessing/data_preprocessing.ipynb`)
│   │   ├── train_set_SMOTEd.csv # Train set with SMOTE (produced from `data_preprocessing/data_preprocessing.ipynb`)
│   │   └── train_set.csv # Train set with no SMOTE (produced from `data_preprocessing/data_preprocessing.ipynb`)
│   └── raw/
│       ├── application_record.csv # Original dataset containing applicant demographic and employment info
│       └── credit_record.csv # Original dataset with applicant credit history over time
├── data_preprocessing/
│   ├── data_cleaning.ipynb 
│   └── feature_engineering.ipynb
├── final_model/
│   ├── visuals/ # Folder containing plots and figures generated during analysis and evaluation
│   │   ├── interactive_3d_plot_fns.html         # Interactive 3D plot visualizing False Negatives (produced from `final_model/microanalysis.ipynb`)
│   │   ├── interactive_3d_plot_misclass.html    # Interactive 3D plot of misclassified points (produced from `final_model/microanalysis.ipynb`)           
│   ├── fairness_eval.ipynb 
│   ├── microanalysis.ipynb
│   ├── test_set_with_predictions.csv # Output CSV with model predictions on the test set (produced from `final_model/tuning.ipynb`)
│   └── tuning.ipynb
├── requirements.txt
└── README.md       
```
### Recommended Order of Review

To understand the project development from data processing to final analysis, we recommend reviewing the Jupyter notebooks in the following sequence:

1.  **Data Preparation:**
    * `data_preprocessing/data_cleaning.ipynb`: Understand how the original datasets (i.e. `data/raw/`) were initially cleaned and handled.
    * `data_preprocessing/feature_engineering.ipynb`: See how we conducted EDA leading to feature engineering, which created the datasets in `data/processed/`.
2.  **Modeling & Evaluation:**
    * `baseline_models/baseline_models.ipynb`: Explore the initial baseline models used for comparison.
    * `final_model/tuning.ipynb`: Delve into the hyperparameter tuning process for the selected final model architecture.
3.  **Analysis & Fairness:**
    * `final_model/fairness_eval.ipynb`: Examine the fairness metrics and analysis performed on the final model.
    * `final_model/microanalysis.ipynb`: Review any further detailed analysis of the model's performance or predictions.


Following this order provides a logical progression through our methodology. The `visuals/` directory contains outputs generated during these steps, and `final_model/test_set_with_predictions.csv` holds the final output predictions on the test data. By following this structure, you’ll be able to clearly trace our work from raw data to final analysis and fairness evaluation.

## Acknowledgements

The original dataset, ["Credit Card Approval Prediction"](https://www.kaggle.com/datasets/rikdifos/credit-card-approval-prediction), was obtained from Kaggle. We thank the authors for making this data available.

---

