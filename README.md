# Customer Retention & Churn Analytics

## Project Overview

Customer churn is a major business challenge for subscription-based companies, where retaining existing customers can be as important as acquiring new ones.

This project develops an end-to-end customer retention analytics solution using the IBM Telco Customer Churn dataset. The workflow combines data cleaning, exploratory data analysis, statistical testing, machine learning, customer risk scoring, financial exposure analysis, SQL-based business analysis, and an interactive Power BI dashboard.

The objective is not only to predict customer churn, but also to identify high-risk customer segments, quantify their financial significance, and prioritize customers for targeted retention strategies.

---

## Business Objectives

The project addresses the following business questions:

- What proportion of customers are churning?
- Which customer characteristics are associated with higher churn?
- Which contract, payment, tenure, and service segments show elevated churn?
- Are the observed differences statistically significant?
- Can machine learning estimate customer-level churn risk?
- Which customers should receive the highest retention priority?
- How much monthly-charge exposure is associated with higher-risk customers?
- How can these insights be presented through an interactive decision-support dashboard?

---

## Dataset

The project uses the **IBM Telco Customer Churn** dataset.

- **Customers:** 7,043
- **Original Features:** 21
- **Target Variable:** `Churn`
- **Target Classes:** Yes / No

The dataset contains customer information related to:

- Demographics
- Account tenure
- Contract type
- Internet and phone services
- Online security and technical support
- Payment method
- Monthly charges
- Total charges
- Churn status

---

## Tools & Technologies

### Python
- Pandas
- NumPy
- Matplotlib
- SciPy
- Scikit-learn
- Jupyter Notebook

### SQL
- SQLite
- SQL queries for customer segmentation and business analysis

### Business Intelligence
- Power BI
- Power Query
- DAX

### Machine Learning
- Logistic Regression
- Decision Tree
- Random Forest
- Gradient Boosting

---

## Project Workflow

The project follows an end-to-end analytics workflow:

1. Data Profiling & Cleaning
2. Exploratory Data Analysis
3. Statistical Analysis
4. Machine Learning
5. Model Evaluation
6. Customer Churn Risk Scoring
7. Financial Exposure Analysis
8. Business Prioritization
9. SQL Business Analysis
10. Power BI Dashboard
11. Retention Strategy Development

---

## Exploratory Data Analysis

Exploratory analysis was performed to understand overall churn and identify customer segments associated with elevated churn.

### Overall Churn

- Total Customers: **7,043**
- Churned Customers: **1,869**
- Retained Customers: **5,174**
- Overall Churn Rate: **26.54%**

Approximately one in four customers in the dataset had churned.

### Contract Type

Observed churn varied substantially by contract:

| Contract | Churn Rate |
|---|---:|
| Month-to-month | ~42.7% |
| One year | ~11.3% |
| Two year | ~2.8% |

Month-to-month customers showed substantially higher observed churn than customers on longer-term contracts.

### Payment Method

Electronic check customers showed the highest observed churn rate among payment methods.

| Payment Method | Churn Rate |
|---|---:|
| Electronic check | ~45.3% |
| Mailed check | ~19.1% |
| Bank transfer (automatic) | ~16.7% |
| Credit card (automatic) | ~15.2% |

Electronic check also represented the largest monthly-charge exposure associated with churned customers among payment methods.

### Customer Tenure

Customers in earlier tenure groups showed higher observed churn, indicating that the early customer lifecycle represents an important retention period.

### Internet Service

Fiber-optic customers showed approximately **41.9% observed churn**, compared with approximately **19.0% for DSL customers**.

### Online Security & Technical Support

Customers without Online Security or Tech Support showed substantially higher observed churn.

- No Online Security: ~41.8%
- Online Security: ~14.6%
- No Tech Support: ~41.6%
- Tech Support: ~15.2%

These findings represent associations in the dataset and should not be interpreted as proof of causation.

---

## Statistical Analysis

Statistical testing was used to determine whether important churn-related differences and associations were supported beyond descriptive visualization.

Methods included:

- Welch's independent two-sample t-test
- Chi-square test of independence
- Cohen's d
- Cramér's V
- Benjamini-Hochberg False Discovery Rate correction

Numerical variables including tenure, MonthlyCharges, and TotalCharges were tested across churn groups, while categorical customer characteristics were evaluated using chi-square tests.

Effect sizes were used alongside statistical significance to distinguish statistically detectable relationships from relationships with greater practical importance.

---

## Machine Learning

The project treats churn prediction as a supervised binary classification problem.

The target was encoded as:

- `0` = No Churn
- `1` = Churn

Customer ID was excluded from the predictive feature set because it is an identifier rather than a meaningful predictive characteristic.

Categorical variables were transformed using One-Hot Encoding, while preprocessing was fitted only on the training data to avoid data leakage.

The dataset was split into stratified training and testing sets using an 80/20 split.

### Models Evaluated

- Logistic Regression
- Decision Tree
- Random Forest
- Gradient Boosting

Models were evaluated using:

- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC
- Confusion Matrix
- ROC Curve
- Precision-Recall analysis

ROC-AUC was used as an important model-ranking metric, while recall, precision, F1 score, and business implications were also considered when evaluating the final solution.

---

## Churn Risk Scoring

The selected model was used to generate customer-level churn probabilities.

For business interpretation, probabilities were converted into project-defined risk categories:

| Churn Probability | Risk Category |
|---:|---|
| < 0.30 | Low Risk |
| 0.30–0.59 | Medium Risk |
| 0.60–0.79 | High Risk |
| >= 0.80 | Very High Risk |

These thresholds are project-defined analytical categories and are not intended as universal industry standards.

---

## Customer Retention Prioritization

Predicted churn risk alone does not capture the financial importance of a customer.

A business-oriented Priority Score was therefore created using:

`Priority Score = 0.70 × Churn Probability + 0.30 × Charge Score`

where:

`Charge Score = MonthlyCharges / Maximum MonthlyCharges`

Customers were then classified into:

| Priority Score | Priority Group |
|---:|---|
| >= 0.70 | Priority 1 |
| >= 0.50 | Priority 2 |
| < 0.50 | Priority 3 |

This framework combines estimated churn risk with customer financial value to support more targeted retention decisions.

The weighting and thresholds are project-defined business rules rather than universal retention formulas.

---

## Financial Exposure

The project distinguishes between **churn risk** and **financial impact**.

Monthly charges associated with churned or higher-risk customers are treated as financial exposure rather than guaranteed revenue loss.

A probability-weighted exposure measure was also used:

`Probability-Weighted Exposure = Σ (Churn Probability × MonthlyCharges)`

This provides an expected-value-style indicator combining model-estimated churn risk with monthly customer charges.

It should not be interpreted as guaranteed future revenue loss.

---

## SQL Analysis

SQLite was used to perform business-oriented SQL analysis on the cleaned and scored customer data.

SQL analysis included:

- Overall churn KPIs
- Contract-based churn analysis
- Payment-method analysis
- Service-based churn analysis
- Tenure segmentation
- Risk-category analysis
- Priority-group analysis
- Financial exposure analysis
- Identification of top retention candidates
- Executive business summaries

Customer-level retention candidates were ranked using business priority, churn probability, and monthly charges.

---

## Power BI Dashboard

An interactive Power BI dashboard was developed to translate the analysis into a business decision-support tool.

The dashboard contains four analytical pages:

### 1. Executive Overview

Provides high-level KPIs including:

- Total customers
- Churned customers
- Churn rate
- Monthly charges
- Contract-level churn
- Tenure-level churn

### 2. Churn Drivers

Explores historical churn patterns across:

- Payment method
- Internet service
- Online security
- Technical support
- Customer tenure

### 3. Risk & Financial Exposure

Focuses on ML-generated customer risk through:

- Risk-category distributions
- Higher-risk customers
- Average churn probability
- Monthly-charge exposure
- Probability-weighted exposure

### 4. Retention Prioritization

Provides an operational customer-level view using:

- Priority groups
- Priority scores
- Churn probabilities
- Risk categories
- Monthly charges
- Customer characteristics

Interactive slicers, synchronized filters, page navigation, and filter-reset functionality were added to support exploratory analysis.

---

## Key Business Insights

The analysis identified several customer populations associated with elevated churn:

1. **Month-to-month customers** showed substantially higher observed churn than customers with longer-term contracts.
2. **Electronic-check customers** combined high observed churn with substantial monthly-charge exposure.
3. **Newer customers** showed greater churn vulnerability, highlighting the importance of the early customer lifecycle.
4. **Fiber-optic customers** showed elevated observed churn and represent an important segment for further investigation.
5. Customers without **Online Security** or **Tech Support** showed substantially higher observed churn.
6. Customer-level ML predictions enabled risk assessment beyond broad segment-level analysis.
7. Combining churn probability with financial value produced a more actionable retention-prioritization framework.

---

## Proposed Retention Strategies

Based on the analytical findings, potential retention strategies include:

- Testing longer-term contract incentives for selected high-risk month-to-month customers.
- Testing automatic-payment adoption campaigns among high-risk electronic-check customers.
- Strengthening onboarding and early-lifecycle engagement for newer at-risk customers.
- Testing support or security-service interventions for relevant high-risk customers.
- Investigating potential service, pricing, or experience issues among high-risk fiber-optic customers.
- Providing stronger personalized retention attention to high-value Priority 1 customers.

These recommendations should be treated as testable business strategies rather than proven causal solutions. Controlled experiments can be used to measure their actual retention impact.

---

## Project Structure

```text
Customer-retention-churn-analytics/
│
├── data/
│   ├── raw/
│   └── processed/
│       ├── customer_churn_clean.csv
│       └── customer_scoring_final.csv
│
├── notebooks/
│   ├── 01_data_profiling.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_statistical_analysis.ipynb
│   └── 04_feature_engineering_&_ML_preparation.ipynb
│
├── sql/
│   ├── sql_analysis.ipynb
│   └── customer_churn.db
│
├── dashboard/
│   └── customer_churn_dashboard.pbix
│
├── README.md
├── requirements.txt
└── .gitignore