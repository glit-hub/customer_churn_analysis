# Customer Churn Analysis
Author: Glit Hanpanitkitkan

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

## Tableau Dashboard (Data Storytelling)
To make insights accessible to non-technical audiences, a Tableau dashboard was built to highlight:

- Key performance numbers (total customers, churn count, churn rate)
- Churn distribution by top cities (stacked bar)
- City-level churn behavior and customer concentration
- KPI-style visuals for quick executive interpretation

**Tableau Public:** *[Link](https://public.tableau.com/app/profile/glit.han/viz/Customer_Churn_Analysis_17671731743320/CustomerChurnAnalysis)*  

---
