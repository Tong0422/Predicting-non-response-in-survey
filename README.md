# Predicting Income Non-Response in a Mozambican Household Survey

## 📌 Project Overview

In survey research, income-related questions often receive high non-response rates, which can bias results and reduce data utility. This project analyzes household survey data from Northern Mozambique to understand which factors are associated with income non-response. 

Using logistic regression and model selection techniques, I identify household and demographic characteristics that predict whether a respondent skips the income question.

---

## 🎯 Objectives

- Clean and preprocess real-world survey data
- Explore demographic and infrastructure-related predictors of income non-response
- Fit logistic regression models, including interaction terms (e.g., gender × electric)
- Use model selection techniques: AIC, BIC, best subset, cross-validation
- Evaluate model performance with AUC, accuracy, and different tests
- Draw actionable insights for improving future surveys

---

## 🧾 Data Description

This project uses a reduced version of the Mozambique Survey dataset. The following variables were included in the analysis:

| Variable         | Description                                        |
|------------------|----------------------------------------------------|
| `INCOME_NONRESPONSE` | Whether the respondent skipped the income question (1 = yes, 0 = no) |
| `SEX`            | Sex of the respondent (0 = Male, 1 = Female)       |
| `AGE`            | Age of the respondent (in years)                   |
| `HEAD`           | Whether the respondent is the head of household (1 = yes, 0 = no)    |
| `EDUC`           | Education level (0 = “None”, 1 = “Primary of the 1st degree”, 2 = “Primary of the 2nd degree”, 3 = “Secondary of the 1st degree”, 4 = “Secondary of the 2nd degree”, 5 = “Higher level”)|
| `PAY_WATER`      | Whether the household pays for water (1 = yes, 0 = no)              |
| `ELECTRIC`       | Whether the household has access to electricity (1 = yes, 0 = no)     |
| `TIME_LENGTH`    | How long did the survey take to complete (in minutes)        |

### Missing Values
Special codes were used in the dataset to represent missing values:
- `-1`, `9998`, `9999` → These were treated as missing and converted to `NA`.

Observations with missing data were removed before modeling (~8.4% of the total dataset).

---

## 🛠 Tools & Methods

- **Language**: R (R Markdown)
- **Libraries**: `dplyr`, `ggplot2`, `bestglm`, `caret`, `ResourceSelection`
- **Methods**:
  - Logistic regression (main effects + interaction)
  - Model selection (AIC, BIC, exhaustive search)
  - Cross-validation (10-fold, repeated)
  - ROC AUC and Hosmer–Lemeshow test

---

## 📊 Final Model Comparison

| Criterion   | Selected Features                                  | Description                                     |
|------------|-----------------------------------------------------|-------------------------------------------------|
| **AIC**     | `HEAD`, `PAY_WATER`, `ELECTRIC`                    | Best trade-off between fit and complexity       |
| **BIC**     | `PAY_WATER`, `ELECTRIC`                            | Simplest adequate model                         |
| **Accuracy**| `AGE`, `PAY_WATER`, `ELECTRIC`, `TIME_LENGTH`      | Highest cross-validated classification rate     |
| **AUC**     | `HEAD`, `PAY_WATER`, `ELECTRIC`, `TIME_LENGTH`     | Best ranking ability on unseen data             |

> ✅ Final model selected: `HEAD`, `PAY_WATER`, `ELECTRIC`, `TIME_LENGTH`  
> This model achieved the best AUC and strong generalization in cross-validation, making it ideal for predicting non-response in future surveys.

---

## 🧠 Key Findings

- Households that **pay for water** were **52.5% less likely** to skip income questions.
- Households with **electricity access** were **79% more likely** to skip.
- Gender played a moderating role — women with electricity access were especially likely to skip income questions.
- **Time spent on the survey** also contributed to non-response, possibly due to survey fatigue.
- Class imbalance and response behavior varied across towns and infrastructure access.

---

## 📣 Summary 

This project helps identify which households are more or less likely to skip income questions in a national water access survey. Using data from over 1,000 households in Mozambique, I found that skipping income questions is closely related to whether people have access to electricity, pay for water, or whether the respondents are household heads. These patterns were also influenced by gender.

This insight can help survey designers rephrase or better time-sensitive questions to improve response rates, making data more complete and reliable for policymaking.

---

## 🌐 View Full Report

👉 [Click here to view the full HTML report](./income_nonresponse_analysis.html)  
*(If using GitHub Pages, you can replace this with your live link)*


