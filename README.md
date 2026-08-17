# ANA500 ePortfolio

**Jesus Adrian Alvarado Gadea**
ANA500, National University

Four micro-projects applying the data science process (Acquire, Prepare, Analyze, Report,
Act) to two datasets, each project terminating at a different step per the assignment
specification. Portfolio complete.

| # | Focus | Terminates at | Dataset | Status |
|---|---|---|---|---|
| 1 | NumPy and Pandas: organize, clean, prepare | Step 2, Prepare | Adult Income | Complete |
| 2 | Visualization (Matplotlib, Seaborn) | Step 4, Report | Adult Income | Complete |
| 3 | Regression (linear, SVM, logistic) | Step 5, Act | Adult Income | Complete |
| 4 | Deep learning regression on time series (LSTM, GRU) | Step 5, Act | Beijing PM2.5 | Complete |

---

## What is in this repository

```
ANA500-ePortfolio/
├── README.md
├── MicroProject1_AdultIncome/
│   ├── Jesus_Alvarado_ANA500_MicroProject1_AdultIncome.ipynb
│   └── data/adult-all.csv                  raw UCI extract (48,842 rows)
├── MicroProject2_AdultIncome/
│   ├── Jesus_Alvarado_ANA500_MicroProject2_AdultIncome.ipynb
│   └── data/adult_income_prepared.csv      output of Micro-Project 1
├── MicroProject3_AdultIncome/
│   ├── Jesus_Alvarado_ANA500_MicroProject3_AdultIncome.ipynb
│   └── data/
│       ├── adult_income_prepared.csv       input
│       └── adult_income_prepared_v2.csv    output, adds married and age_group
└── MicroProject4_BeijingPM25/
    ├── Jesus_Alvarado_ANA500_MicroProject4_BeijingPM25.ipynb
    └── data/beijing_pm25_raw.csv           raw hourly file (43,824 rows)
```

Each project folder is self-contained: the notebook and the data it reads sit together, so
every notebook runs from its own directory without editing any paths. All four notebooks
have been executed end to end, so the figures and output are visible on GitHub without
running anything.

## Datasets

**Micro-Projects 1 to 3 — Adult / Census Income.**
UCI Machine Learning Repository, dataset ID 2. Becker, B. and Kohavi, R. (1996). *Adult*
[Dataset]. https://doi.org/10.24432/C5XW20. Licensed CC BY 4.0.
48,842 rows, 14 predictors, binary income target, extracted from the 1994 US Census.

**Micro-Project 4 — Beijing PM2.5.**
UCI Machine Learning Repository, dataset ID 381. Liang, X., Zou, T., Guo, B., Li, S.,
Zhang, H., Zhang, S., Huang, H. and Chen, S. X. (2015). Assessing Beijing's PM2.5
pollution: severity, weather impact, APEC and winter heating. *Proceedings of the Royal
Society A*, 471(2182). Licensed CC BY 4.0.
43,824 hourly rows, January 2010 to December 2014, PM2.5 paired with meteorology.

The dataset changes for the final project because the Adult extract is a single 1994
cross-section with no time dimension, and recurrent networks need a sequence to read.

## Running the notebooks

```
pip install numpy pandas matplotlib seaborn scikit-learn tensorflow jupyter
cd MicroProject4_BeijingPM25        # or any project folder
jupyter notebook
```

Micro-Projects 1 to 3 need only NumPy, Pandas, Matplotlib, Seaborn, and scikit-learn.
Micro-Project 4 additionally needs TensorFlow. Every notebook reads from its own `data/`
subfolder, and the loaders fall back to a remote mirror if a local file is missing.

---

## Micro-Project 1: Acquire and Prepare

[View the Micro-Project 1 notebook](MicroProject1_AdultIncome/Jesus_Alvarado_ANA500_MicroProject1_AdultIncome.ipynb)

Loaded and merged the raw UCI extract, then cleaned it with NumPy and Pandas: recoded
structural missingness to an explicit `Unknown` level rather than dropping it, removed 52
exact-duplicate rows, dropped the redundant `education` text column and the non-personal
`fnlwgt` survey weight, and built nine derived columns. Result: 48,842 to 48,790 rows,
6,465 to 0 missing cells, target rate preserved within 0.01 percentage points.

## Micro-Project 2: Analyze and Report

[View the Micro-Project 2 notebook](MicroProject2_AdultIncome/Jesus_Alvarado_ANA500_MicroProject2_AdultIncome.ipynb)

Nine Matplotlib/Seaborn figures examining the Micro-Project 1 hypothesis. Confirmed the
named variables, surfaced two additions the hypothesis did not name (age, capital-gain
participation), and flagged sex and race disparities for the Micro-Project 3 models to be
checked against.

## Micro-Project 3: Analyze, Report, and Act

[View the Micro-Project 3 notebook](MicroProject3_AdultIncome/Jesus_Alvarado_ANA500_MicroProject3_AdultIncome.ipynb)

Compared six models on a 75/25 stratified split: linear regression, linear SVR, logistic
regression (plain and class-balanced), LinearSVC, and an RBF-kernel SVC. Incorporated
instructor feedback from Micro-Project 2: marital status recoded to a Married/Not-Married
binary, age reduced to three groups, and the class imbalance corrected with class weights
(recall on the >50K class 0.59 to 0.84). Final model: balanced logistic regression
(AUC 0.905). Sex and race were excluded as predictors and used only to document
group-level error rates.

## Micro-Project 4: Deep Learning Regression on a Time Series

[View the Micro-Project 4 notebook](MicroProject4_BeijingPM25/Jesus_Alvarado_ANA500_MicroProject4_BeijingPM25.ipynb)

Forecast next-hour PM2.5 from the trailing 24 hours of pollution and weather. Prepared the
raw file (datetime assembly, missingness audit, time interpolation of short gaps,
chronological 70/15/15 split with train-only scaling), then compared five models on the
final unseen months: persistence, linear regression on the flattened window, a dense
network, an LSTM, and a GRU. Result: the recurrent networks win on every metric (LSTM MAE
10.4, RMSE 18.6, R-squared 0.945, against persistence at 10.9 and 19.9), while the
memoryless models given the same history barely match persistence. Error analysis by
pollution severity band documents where the forecast can be trusted.

---

## Problem statements

**Micro-Projects 1 to 3.** Earnings in the 1994 United States workforce were distributed
unevenly across demographic and employment characteristics. These projects describe which
recorded personal and employment attributes are associated with earning above 50,000
dollars per year.

**Micro-Project 4.** Fine-particle air pollution in Beijing swings sharply from hour to
hour, and dangerous episodes arrive with little warning. This project describes how the
next hour's PM2.5 concentration relates to the recent history of pollution and weather.

## Hypotheses

**Micro-Projects 1 to 3.** Educational attainment and weekly hours worked are the dominant
correlates of exceeding 50,000 dollars in annual income, with occupation category and
marital status contributing additional explanatory signal beyond those two variables.

**Micro-Project 4.** The recent 24 hours of pollution and weather carry predictive signal
beyond the current reading alone: (a) models using that history will beat a persistence
forecast, and (b) recurrent networks reading the window as an ordered sequence will
outperform memoryless models given the same window flat.

## Findings

**Adult Income hypothesis — partially supported, and refined.**

Confirmed as stated: education and hours worked are strong correlates of exceeding
$50,000, and both survive controlling for every other variable in the model.

Wrong as stated: marital status was named secondary, but its coefficient is the largest of
the broad demographic effects, above a full standard deviation of education. Capital-gain
participation, not named at all in the original hypothesis, carries the single largest
coefficient overall, though only 8.3% of the sample has any capital gain.

Refined: being married with a spouse present, education, and hours worked are the dominant
broad correlates. Capital-gain participation is a narrow but nearly decisive marker for the
few who have it, and occupation contributes additional signal.

**Beijing PM2.5 hypothesis — part (b) supported cleanly, part (a) only in a narrower
form.**

The recurrent networks beat every other model on every metric, across two cell types. The
memoryless models given the same 24-hour history barely match a persistence forecast, so it
is not the history alone that beats the last reading, it is the history read in order. The
recurrent advantage at one hour ahead is real but modest, because the next hour is
genuinely dominated by the current one.

Both hypotheses survived contact with the evidence only after refinement, which is the
iterative process the assignment describes.
