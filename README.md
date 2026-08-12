# AI-Driven Flood Risk Prediction and Risk-Sensitive Insurance Pricing

## 
Project Overview

This capstone project develops an **AI-driven flood-risk prediction model** that integrates **water infrastructure condition and climate data** to predict flood occurrence and demonstrates how these predictions can be applied to **risk-sensitive insurance pricing**.

The implementation focuses on **eThekwini and Johannesburg, South Africa**, and compares an integrated, model-driven pricing approach with a traditional flat historical-rate approach.

The project investigates whether combining infrastructure health indicators with climate information can provide useful signals for flood-risk prediction and whether those predictions can support more responsive insurance pricing.

---

## Objectives

The project has two main objectives:

### Objective 1: Flood Risk Prediction

Develop a predictive model that links:

* Water infrastructure condition
* Climate and rainfall information
* Historical flood events

to the probability of flood occurrence.

### Objective 2: Risk-Sensitive Insurance Pricing

Use the predicted flood probabilities to demonstrate a **risk-sensitive insurance pricing approach**, and benchmark the resulting premiums against traditional flat-rate historical pricing.

---

## Data Sources

Four independent categories of public data were integrated into the project.

### 1. Municipal Infrastructure and Financial Data

Infrastructure-related indicators included:

* Repairs and maintenance expenditure
* Non-revenue water percentage
* Water losses

These were sourced from municipal budget portals and audited annual reports.

### 2. Climate Data

Monthly climate information was obtained from the **ASSA extreme rainfall index**, providing rainfall-related information for the study period.

### 3. Historical Flood Events

Historical flood events were obtained from the **EM-DAT International Disaster Database**.

### 4. Infrastructure Health Scores

Water infrastructure condition was represented using:

* **Green Drop** scores
* **Blue Drop** scores

Data sources were independently cross-checked wherever possible. For example, Green Drop scores were verified against published Department of Water and Sanitation reports, while historical flood event dates were checked against independent sources before being included.

---

## Data Preparation and Integration

The different datasets used different reporting frequencies and formats.

To make the data suitable for modelling:

1. Data sources were cleaned and standardised.
2. Dates were aligned with South Africa's financial-year convention.
3. Annual infrastructure information was integrated with monthly climate and flood-event data.
4. The datasets were merged at a **monthly city-level resolution**.
5. A total of **244 city-month observations** were produced.
6. A completeness indicator called `Core_Complete` was created to identify observations containing the required core variables.
7. This resulted in **96 usable city-month observations** for the core modelling analysis.

Missing data were not blindly imputed. Imputation was only applied where the proportion of missing values was below approximately 30%. Variables with substantial missingness were excluded from the core model.

---

## Exploratory Data Analysis

Exploratory analysis identified several important characteristics of the data.

### Class Imbalance

Flood-positive months represented approximately **11.5%** of the observations, indicating a significant class imbalance.

### Rainfall and Flood Occurrence

Rainfall provided the clearest visual separation between flood and non-flood months.

However, some historical flood months did not have unusually high rainfall during the same month.

This suggested that flood occurrence may depend not only on immediate rainfall but also on **cumulative rainfall over previous months**.

This finding directly informed the feature-engineering strategy.

---

## Feature Engineering

Two rainfall-based features were created:

### One-Month Rainfall Lag

A lagged rainfall variable was introduced to capture the influence of rainfall from the previous month.

### Three-Month Rolling Rainfall

A three-month rolling rainfall total was created to represent cumulative rainfall conditions over time.

These features were derived from the existing rainfall data rather than introducing external information.

Municipality was also encoded as a numerical feature to account for structural differences between eThekwini and Johannesburg.

Additional features were tested during robustness analysis, including:

* Detrended water-loss variables
* Wet-season indicator

These additional features were not included in the final model because they did not improve performance.

---

## Machine Learning Methodology

A **Random Forest Classifier** was selected as the primary predictive model.

The modelling process included:

1. Stratified train-test splitting
2. Five-fold stratified cross-validation
3. Random Forest model training
4. Decision-threshold analysis
5. Precision-recall evaluation
6. Comparison with Logistic Regression

Rather than automatically using the standard 0.5 classification threshold, decision thresholds from **0.5 down to 0.1** were evaluated to identify a suitable precision-recall balance.

A Logistic Regression model was also used as a benchmark to determine whether Random Forest provided a genuine performance advantage.

---

## Model Results

The final Random Forest configuration used a **0.4 decision threshold**.

The model achieved:

| Metric    |   Result |
| --------- | -------: |
| Precision | **100%** |
| Recall    |  **45%** |

The model produced **zero false-positive flood predictions** across the study data.

The 45% recall indicates that the model identified approximately 45% of historical flood events.

### Feature Importance

Feature importance analysis indicated that **rainfall and lagged rainfall variables contributed approximately 75% of the model's predictive signal**.

Infrastructure-related variables provided a meaningful secondary contribution.

This provides supporting evidence for the project's hypothesis that climate conditions, together with infrastructure-related information, can provide useful signals for flood-risk prediction.

---

## Robustness Testing

Four independent robustness tests were conducted before finalising the model configuration.

These included testing:

* An expanded flood-event dataset containing additional independently verified events
* Higher-quality standardised infrastructure data from National Treasury
* Additional engineered features
* Alternative model configurations

Across these tests, the original, simpler configuration consistently outperformed the alternatives.

This suggests that, given the relatively small sample size, increasing model complexity or adding additional variables did not necessarily improve predictive performance.

---

# Insurance Pricing Simulation

The second objective applied the flood-risk predictions to an insurance pricing simulation.

The project uses the actuarial **pure premium approach**:

**Pure Premium = Frequency × Severity**

### Frequency

Flood frequency was represented using the model's **cross-validated flood probability** on a month-by-month basis.

### Severity

Flood severity was based on reported flood damage figures from EM-DAT.

Damage values reported in US dollars were converted to South African rand.

The **median** damage value was used rather than the mean to reduce the influence of a single catastrophic outlier event.

---

## Pricing Results

The integrated risk-sensitive pricing approach was compared with a traditional flat historical-rate premium.

The analysis found that the traditional approach:

* **Under-priced actual risk in approximately 28% of months**
* Had an average under-pricing gap exceeding **R270 million**
* Over-priced lower-risk periods during other months

The integrated approach does not simply increase premiums overall.

Instead, it **redistributes pricing according to changing predicted risk**, resulting in higher premiums during periods of elevated predicted flood risk and lower premiums during comparatively calm periods.

This demonstrates the potential mechanism through which predictive modelling could support more risk-sensitive insurance pricing.

---

## Potential Impact

The project demonstrates how combining infrastructure, climate, and historical disaster information could support decision-making in areas such as:

* Flood-risk assessment
* Municipal infrastructure planning
* Predictive maintenance
* Insurance risk assessment
* Dynamic or risk-sensitive pricing
* Disaster preparedness
* Resource allocation

For insurers, a predictive approach could potentially provide a more responsive representation of changing risk than a single historical flat rate.

For municipalities, infrastructure-related information could contribute to a broader understanding of flood vulnerability.

---

## Limitations

The results should be interpreted as **feasibility evidence rather than definitive proof**.

Three important limitations were identified.

### 1. Small Sample Size

The core modelling dataset contained only **96 usable city-month observations**, which limits the statistical generalisability of the results.

### 2. Flood Event Coverage

EM-DAT may underrepresent smaller, localised flood events that do not meet the database's reporting criteria.

### 3. Pricing Depends on Prediction Quality

The insurance pricing simulation is directly affected by the predictive performance of the flood-risk model.

In particular, the model's **45% recall** means that some historical flood events were not identified by the model.

Therefore, the pricing results should be viewed as a simulation demonstrating the potential application of predictive risk information rather than a production-ready insurance pricing system.

---

## Conclusion

This project provides feasibility evidence that **water infrastructure condition and climate information can be integrated into an AI-driven flood-risk prediction framework** for South African cities.

The Random Forest model identified rainfall and lagged rainfall as the strongest predictive signals while infrastructure variables provided additional information.

The predicted risk was subsequently incorporated into a pure-premium insurance pricing simulation, demonstrating how model-based risk estimates can produce more responsive pricing than a traditional flat historical rate.

Overall, the project demonstrates a potential pathway from:

```text
Infrastructure + Climate Data
            ↓
      Data Integration
            ↓
     Feature Engineering
            ↓
     Flood Risk Model
            ↓
   Predicted Flood Risk
            ↓
    Frequency × Severity
            ↓
Risk-Sensitive Premium Simulation
```

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Seaborn
* Jupyter Notebook
* Machine Learning
* Statistical Analysis
* Data Integration
* Predictive Modelling

---

## Repository Structure

```text
capstone-project/
│
├── data/
│   └── Project datasets
│
├── notebook/
│   └── Data analysis and modelling notebooks
│
├── outputs/
│   └── Figures, tables and model results
│
├── README.md
├── .gitignore
└── .gitattributes
```
---

## Author

**Zinhle Fanezi Mahlangu**

BSc Data Science | Mathematics & Statistics | Machine Learning | Python

Final-Year Data Science Capstone Project
