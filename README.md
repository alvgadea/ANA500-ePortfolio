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
| 3 | Regression (linear, SVM) | Step 5, Act | Pending |
| 4 | Deep learning regression on time-series (RNN) | Step 5, Act | Pending |

## Dataset

Adult / Census Income, UCI Machine Learning Repository, dataset ID 2. Becker, B. and
Kohavi, R. (1996). *Adult* [Dataset]. UCI Machine Learning Repository.
https://doi.org/10.24432/C5XW20. Licensed CC BY 4.0.

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

## Problem statement

Earnings in the 1994 United States workforce were distributed unevenly across demographic
and employment characteristics. This project describes which recorded personal and
employment attributes are associated with earning above $50,000 per year.

## Hypothesis

Educational attainment and weekly hours worked are the dominant correlates of exceeding
$50,000 in annual income, with occupation category and marital status contributing
additional explanatory signal beyond those two variables.
