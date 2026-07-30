# Customer Churn Analysis
Author: Glit Hanpanitkitkan

### [Project File](https://github.com/glit-hub/customer_churn_analysis/blob/main/analysis.ipynb)
### [Tableau](https://public.tableau.com/app/profile/glit.han/viz/Customer_Churn_Analysis_17671731743320/CustomerChurnAnalysis)

## Project Overview:
**Research Question:** \
What are the driving factors that help determine whether a customer stays or leave a telecommunications company? How can we predict whether a customer will churn based on these variables?

**Motivation:** \
Customer retention is a critical objective for many companies, particularly in subscription-based and highly competitive industries such as telecommunications. With numerous alternatives available and low switching costs, customers can easily change providers, making churn a persistent challenge.

Understanding customer characteristics, preferences, and service usage is essential for identifying the factors that drive satisfaction and churn. By leveraging data-driven insights, companies can design targeted strategies to improve customer experience, reduce churn, and remain competitive.

## Data Sources:

| Dataset                         | Source                               | Key Features |
|---------------------------------|--------------------------------------|-------------|
| Telco Customer Churn | [IBM](https://community.ibm.com/community/user/blogs/steven-macko/2019/07/11/telco-customer-churn-1113) | Customer-level data including demographics, services, contracts, and churn outcome |

## Methods

### 1) Data Preparation
The dataset includes a mix of numeric and categorical fields describing customer demographics, services, and account details. To make the data model-ready, the workflow included:

- Converting binary **Yes/No** fields into **1/0** for consistent modeling and plotting
- Selecting a set of predictive features for churn modeling
- Ensuring the target label (`Churn Value`) is correctly formatted as a binary outcome:
  - **0 = No churn**
  - **1 = Churn**

### 2) Exploratory Data Analysis (EDA)
Before modeling, exploratory analysis was performed to understand churn behavior and feature relationships. This included:

- Distributions of key numeric variables (e.g., Tenure Months, Monthly Charges, Total Charges, CLTV)
- Categorical breakdowns of customer characteristics and services
- Comparing feature distributions by churn group (e.g., KDE distribution of **Monthly Charges** by churn)

A key observation from EDA is that churn patterns vary across customer segments. For example, Monthly Charges show different distribution shapes for churn vs non-churn customers, suggesting pricing/service tiers may relate to churn risk.

---

## Predictive Modeling

### Features Used
The model was trained using the following features:

- `Tenure Months`
- `Dependents`
- `Has Internet Service`
- `Monthly Charges`
- `Paperless Billing`
- `Tech Support`
- `Senior Citizen`
- `Partner`
- `Online Security`
- `CLTV`

### Models Trained
Because churn is a **binary classification** problem, the following models were evaluated:

- **Logistic Regression**
- **Decision Tree Classifier**
- **Random Forest Classifier**

### Evaluation Approach
Models were evaluated using:

- **Accuracy**
- **ROC-AUC**
- **Confusion Matrix**
- **Precision / Recall / F1-score** (Classification Report)

Because missing a churner can be costly in real business settings, recall for the churn class (**Churn = 1**) is emphasized as an important metric.

---

## Results

| Model | Accuracy | ROC-AUC | Recall (Churn=1) |
|------|----------:|--------:|-----------------:|
| Logistic Regression | 0.8027 | 0.8380 | 0.54 |
| Decision Tree (max_depth=3) | 0.7864 | 0.7934 | 0.38 |
| Random Forest (n=100) | 0.7899 | 0.8318 | 0.49 |

**Best overall model:** **Logistic Regression**  
It achieved the strongest ROC-AUC and the highest recall for churners among the tested models.

---

## Limitations

- **Moderate recall on churners:** Since missing a churner is the costliest error in a retention context, recall in the 0.38–0.54 range means a substantial share of true churners are still misclassified as staying, limiting how much the model can be trusted on its own for targeting interventions.
- **Single, static dataset:** The analysis relies on one snapshot of IBM's Telco Customer Churn dataset. Churn drivers can shift over time (pricing changes, new competitors, macroeconomic conditions), so the model reflects this one period rather than an evolving customer base.
- **No hyperparameter tuning:** The Decision Tree and Random Forest models were run with largely default or fixed settings (e.g., max_depth=3, n_estimators=100) rather than tuned via cross-validation or grid search.
- **Correlation rather than causation:** Relationships identified (e.g., low monthly charges associated with higher churn) describe association, not causation, so business actions based on these features should be tested (e.g., via A/B tests) before wide rollout.
- **No external validation:** The models were evaluated with a single train/test split on this dataset only; performance has not been validated against a separate time period, region, or company to confirm the findings generalize.

---

## How This Research Helps

- **Prioritizes retention efforts:** By ranking which customer attributes (tenure, dependents, internet service, monthly charges, tech support, etc.) most relate to churn, the business can focus limited retention budget and outreach on the highest-risk segments instead of treating all customers the same.
- **Supports proactive, not reactive, retention:** Because the model estimates churn probability before a customer leaves, teams (e.g., customer success, marketing) can intervene with offers, check-ins, or service upgrades ahead of cancellation rather than after.
- **Makes insights usable beyond the data team:** The accompanying Tableau dashboard translates the statistical findings into an accessible, visual format so non-technical stakeholders can see churn concentration by city and track KPIs without needing to interpret the underlying models.

## Tableau Dashboard (Data Storytelling)
To make insights accessible to non-technical audiences, a Tableau dashboard was built to highlight:

- Key performance numbers (total customers, churn count, churn rate)
- Churn distribution by top cities (stacked bar)
- City-level churn behavior and customer concentration
- KPI-style visuals for quick executive interpretation

**Tableau Public:** *[Link](https://public.tableau.com/app/profile/glit.han/viz/Customer_Churn_Analysis_17671731743320/CustomerChurnAnalysis)*  

---
