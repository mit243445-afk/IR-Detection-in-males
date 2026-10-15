# IR Detection in Males

Detecting insulin resistance in men using consumer wearable data and machine learning.

This repository contains the analysis code for my Master's by Research thesis (MR603) at the Melbourne Institute of Technology.

## Overview

Most wearable-based metabolic risk studies pool men and women together, so little is known about how well wearable signals detect insulin resistance in men specifically. This project builds and evaluates models on a male-only cohort to answer two research questions:

1. **RQ1:** Which wearable-derived metrics most strongly relate to insulin resistance in men?
2. **RQ2:** Does adding wearable data improve detection over routine clinical information (age and BMI)?

## Data

- **Cohort:** WEAR-ME study (Metwally et al.), restricted to men without diabetes (n = 464, of whom 108 or 23.3% are insulin resistant)
- **Outcome:** insulin resistance defined as HOMA-IR ≥ 2.9
- **Wearable features (5):** resting heart rate, heart rate variability, daily steps, weekly active zone minutes, sleep duration
- **Excluded by design:** continuous glucose monitoring features, since the outcome is derived from glucose and CGM is a medical device rather than passive consumer sensing

The dataset is **not included** in this repository. It must be obtained from the original source under its own access terms. Place the data file in a `data/` folder before running the notebooks.

## Methods

- Nested model tiers (M0 to M5), adding feature blocks step by step on top of age and BMI
- **Primary model:** penalised logistic regression
- **Secondary model:** shallow XGBoost
- **Exploratory model:** Explainable Boosting Machine (EBM)
- **Validation:** repeated stratified 5-fold cross-validation (20 repeats); internal validation only
- **Feature importance stability:** 1,000 bootstrap resamples

## Key results

- Resting heart rate was the strongest wearable feature (OR 1.90 per SD, 95% CI 1.46 to 2.47) and ranked first in 86.9% of bootstrap samples
- The five wearable features added +0.040 AUROC (95% CI 0.005 to 0.074) over age and BMI
- The added value shrank when a routine blood panel (+0.023) or fasting glucose (+0.013) was already included

These results are internally validated only and have not been tested on an external cohort.

## Repository structure

```
.
├── data/                 # not tracked; place the dataset here
├── notebooks/            # analysis notebooks
├── requirements.txt      # Python dependencies
└── README.md
```

> Update this section to match the actual file names in the repo.

## Getting started

```bash
git clone https://github.com/mit243445-afk/IR-Detection-in-males.git
cd IR-Detection-in-males
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

Main libraries: pandas, numpy, pyarrow, scikit-learn, xgboost, interpret (EBM), matplotlib.

## Author

**Sujan**, Master's by Research candidate, Melbourne Institute of Technology

Supervisors: Dr. Nasim Ahmed (Principal Supervisor), Dr. Amoakoh Gyasi-Agyei (Cluster Lead)

## Disclaimer

This is a research project and is not a clinical or diagnostic tool.
