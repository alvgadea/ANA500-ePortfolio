# ANA500 ePortfolio

Jesus Adrian Alvarado Gadea
ANA500, National University

Four micro-projects applying the data science process (Acquire, Prepare, Analyze, Report,
Act) to a chosen dataset, each terminating at a different step per the assignment
specification.

| # | Focus | Terminates at | Status |
|---|---|---|---|
| 1 | NumPy and Pandas: organize, clean, prepare | Step 2, Prepare | Complete |
| 2 | Visualization (Matplotlib, Seaborn) | Step 4, Report | Complete |
| 3 | Regression (linear, SVM) | Step 5, Act | Complete |
| 4 | Deep learning regression on time-series (RNN) | Step 5, Act | Pending |

## Dataset

Adult / Census Income, UCI Machine Learning Repository, dataset ID 2. Becker, B. and
Kohavi, R. (1996). *Adult* [Dataset]. UCI Machine Learning Repository.
[https://doi.org/10.24432/C5XW20](https://doi.org/10.24432/C5XW20). Licensed CC BY 4.0.

## Micro-Project 1: Acquire and Prepare

[View the Micro-Project 1 notebook](MicroProject1_AdultIncome/Jesus_Alvarado_ANA500_MicroProject1_AdultIncome.ipynb)

Loaded and merged the raw UCI extract, then cleaned it with NumPy and Pandas: recoded
structural missingness to an explicit `Unknown` level rather than dropping it, removed 52
exact-duplicate rows, dropped the redundant `education` text column and the non-personal
`fnlwgt` survey weight, and built nine derived columns. Result: 48,842 to 48,790 rows,
6,465 to 0 missing cells, target rate preserved within 0.01 percentage points.

## Micro-Project 2: Analyze and Report

[View the Micro-Project 2 notebook](MicroProject2_AdultIncome/Jesus_Alvarado_ANA500_MicroProject2_AdultIncome.ipynb)

Nine Matplotlib/Seaborn figures examining the Micro-Project 1 hypothesis (education and
hours as dominant correlates of income, with occupation and marital status contributing
additional signal). Confirmed the named variables, surfaced two additions the hypothesis
did not name (age, capital-gain participation), and flagged sex/race disparities for the
Micro-Project 3 models to be checked against.

## Micro-Project 3: Analyze, Report, and Act

[View the Micro-Project 3 notebook](MicroProject3_AdultIncome/Jesus_Alvarado_ANA500_MicroProject3_AdultIncome.ipynb)

Fitted the named regression methods (linear regression, linear SVR) on the binary target
to document where they break (22.1% and 40.9% of predictions outside [0, 1]), then
compared them against logistic regression and SVM classifiers on the same held-out test
set. Incorporated instructor feedback from Micro-Project 2: marital status recoded to a
Married/Not-Married binary, age reduced to three groups, and the class imbalance
corrected with class weights (recall on the >50K class 0.59 to 0.84). Final model:
balanced logistic regression (AUC 0.905). Hypothesis verdict: partially supported and
refined, with marriage emerging as the largest broad demographic effect. Group-level
error rates documented by sex and race.

## Problem statement

Earnings in the 1994 United States workforce were distributed unevenly across demographic
and employment characteristics. This project describes which recorded personal and
employment attributes are associated with earning above $50,000 per year.

## Hypothesis

Educational attainment and weekly hours worked are the dominant correlates of exceeding
$50,000 in annual income, with occupation category and marital status contributing
additional explanatory signal beyond those two variables.

## Findings

Tested by the Micro-Project 3 models: partially supported and refined.

Confirmed as stated: education and hours worked are strong correlates of exceeding
$50,000, and both survive controlling for every other variable in the model.

Wrong as stated: marital status was named secondary, but its coefficient is the largest
of the broad demographic effects, above a full standard deviation of education. Capital-
gain participation, not named at all in the original hypothesis, carries the single
largest coefficient overall, though only 8.3% of the sample has any capital gain.

**Refined hypothesis:** being married with a spouse present, education, and hours worked
are the dominant broad correlates of exceeding $50,000. Capital-gain participation is a
narrow but nearly decisive marker for the few who have it, and occupation contributes
additional signal.
