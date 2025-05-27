## Investment Adoption Predictor
This project aims to predict customer adoption of investment (term deposit) using demographic and interaction data from a Portuguese bank's marketing campaigns. The approach is inspired by the Theory of Planned Behavior, which emphasizes the role of attitudes, social norms, and perceived control in decision-making. The model supports targeted marketing, personalized engagement, and ultimately seeks to increase adoption rates of investment products.

## Objective
To develop a machine learning pipeline that classifies whether a customer will subscribe to a term deposit based on:

Demographic attributes (e.g., age, job, education)

Behavioral features (e.g., past campaign outcomes)

Interaction history (e.g., contact communication type)

The final output enables actionable insights for marketing teams to tailor strategies more effectively.

## Theory Used
Theory of Planned Behavior (TPB)
The theory guides feature relevance and interpretation:

Attitude: customer's financial profile and product familiarity

Subjective Norms: contact outcomes and social characteristics (e.g., job, marital status)

Perceived Behavioral Control: external constraints (e.g., loan status, housing loan)

## Dataset
Source: UCI Bank Marketing Dataset

File used: bank-full.csv → cleaned version as bank_m.csv

Target: y (binary classification: 'yes' or 'no' for term deposit subscription)

 Attribute information:
   Input variables:
   # bank client data:
   1 - age (numeric)
   2 - job : type of job (categorical: "admin.","unknown","unemployed","management","housemaid","entrepreneur","student",
                                       "blue-collar","self-employed","retired","technician","services") 
   3 - marital : marital status (categorical: "married","divorced","single"; note: "divorced" means divorced or widowed)
   4 - education (categorical: "unknown","secondary","primary","tertiary")
   5 - default: has credit in default? (binary: "yes","no")
   6 - balance: average yearly balance, in euros (numeric) 
   7 - housing: has housing loan? (binary: "yes","no")
   8 - loan: has personal loan? (binary: "yes","no")
   # related with the last contact of the current campaign:
   9 - contact: contact communication type (categorical: "unknown","telephone","cellular") 
  10 - day: last contact day of the month (numeric)
  11 - month: last contact month of year (categorical: "jan", "feb", "mar", ..., "nov", "dec")
  12 - duration: last contact duration, in seconds (numeric)
   # other attributes:
  13 - campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact)
  14 - pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric, -1 means client was not previously contacted)
  15 - previous: number of contacts performed before this campaign and for this client (numeric)
  16 - poutcome: outcome of the previous marketing campaign (categorical: "unknown","other","failure","success")

  Output variable (desired target):
  17 - y - has the client subscribed a term deposit? (binary: "yes","no")

 Missing Attribute Values: None(Unkown)

## Exploratory Data Analysis (EDA)
1. Class Imbalance:
Only ~11% of customers subscribed to a term deposit — confirmed need for RandomOverSampler.

2. Age Distribution:
Majority were aged 30–40, but higher subscription rates appeared in 60+.

3. Job Roles:
Retired, student, and unemployed had surprisingly higher conversion rates.
Blue-collar workers had the lowest.

4. Contact Method:
Cellphone contact showed significantly better performance than telephone.

5. Duration:
Subscription likelihood increased sharply with call duration > 300 seconds.

6. Previous Campaign Outcome:
If the customer previously said "yes," they're far more likely to convert again.

7. Education:
Tertiary education correlated positively with subscription.

## Methodology
## ML Pipeline
A robust pipeline includes:

Preprocessing:
Label & One-Hot Encoding

Standardization of numerical features
standardScaler

Balancing:
RandomOverSampler for minority class oversampling

Model:
Baseline model
Logistic Regression
RandomForestClassifier
XGBoostClassifier

Evaluation:
ROC-AUC, classification report, accuracy_score
Feature coefficients for interpretability

## Evaluation Metrics
Best model is RandomForestClassifier
| Metric          | Value (placeholder) |
| --------------- | ------------------- |
| Accuracy        | 0.89                |
| ROC-AUC Score   | 0.78                |
| Precision (Yes) | 0.72                |
| Recall (Yes)    | 0.68                |

## Business Use Case
The model informs:
Call list prioritization
Personalized content (e.g., based on job/education)
Timing of outreach (avoid low-performing months)
Channel strategy (cellphone preferred)

## Project Structure
Investment-Adoption-Predictor/
├── data/
│   └── bank_m.csv
├── notebooks/
│   ├── bank.ipynb     ## Exploratory analysis
│   └── model.ipynb    ## Pipeline + modeling
├── README.md
└── requirements.txt

## How to Run
# Step 1: Clone repo
git clone https://github.com/yourusername/Investment-Adoption-Predictor.git
# Step 2: Navigate to project
cd Investment-Adoption-Predictor
# Step 3: Install dependencies
pip install -r requirements.txt
# Step 4: Launch notebook
jupyter notebook
## Model Files
The trained model (`rf_model.pkl`) and scaler (`scaler.pkl`) are not included in this repository due to size limits.  
[Download them here](rf_model= https://drive.google.com/file/d/1fhUldc4gHZIUImj187gkTK_QWkdJAv67/view?usp=drive_link , scaler= <https://drive.google.com/file/d/1erCAFG67ErjDrIA1L7jY8ugOtv_fyn0X/view?usp=drive_link>) and place them in the project root directory.

## Next Steps
Add SHAP for model explainability
Deploy with Streamlit (for marketing team dashboard)

##  License
Citation Request:
  This dataset is public available for research. The details are described in [Moro et al., 2011]. 
  Please include this citation if you plan to use this database:

  In P. Novais et al. (Eds.), Proceedings of the European Simulation and Modelling Conference - ESM'2011, pp. 117-121, Guimarães, Portugal, October, 2011. EUROSIS.

  Available at: [pdf] http://hdl.handle.net/1822/14838
                [bib] http://www3.dsi.uminho.pt/pcortez/bib/2011-esm-1.txt

