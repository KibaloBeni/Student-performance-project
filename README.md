# Student Performance Analysis

Exploratory data analysis and baseline regression model built on the **UCI Student Performance** dataset (649 students, 33 variables). The project examines which factors — study habits, past failures, absences — are associated with final grades.

The repository contains **two notebooks** that cover the same analysis at different levels of depth — see [Project structure](#project-structure) below.

---

## Key results

| Metric | Value |
|--------|-------|
| Model | Linear Regression |
| MAE | ~0.77 (on a 0–20 scale, 5-fold CV) |
| R² | ~0.85 (with prior grades G1/G2) |
| R² — habits only | ~0.32 (without G1/G2) |

Notable correlations with final grade (G3):
- Prior grades G1 and G2: **+0.83 / +0.92** (strongest predictors)
- Past failures: **−0.39**
- Study time: **+0.25**
- Daily alcohol consumption: **−0.21**
- Higher education aspiration: meaningful positive signal

---

## Dataset

**Source**: [UCI Machine Learning Repository – Student Performance](https://archive.ics.uci.edu/dataset/320/student+performance)  
**Students**: 649 (Portuguese secondary school, math course)  
**Features**: 33 variables covering demographics, family background, lifestyle, and academic history  
**Target**: `G3` — final period grade (0–20)  
**No download needed** — the dataset is fetched automatically at runtime via `ucimlrepo`.

Key variables used in this analysis:

| Variable | Description |
|----------|-------------|
| `G1`, `G2` | First and second period grades |
| `studytime` | Weekly study time (1 = <2h, 4 = >10h) |
| `failures` | Number of past class failures |
| `absences` | Number of school absences |
| `internet` | Internet access at home (yes/no) |
| `higher` | Wants to pursue higher education (yes/no) |
| `Medu`, `Fedu` | Mother's / Father's education level |
| `Dalc`, `Walc` | Daily and weekend alcohol consumption |

---

## Project structure

```
.
├── Student_Performance_Analysis.ipynb                   # Notebook 1 — clean baseline
├── Student_Performance_Analysis_with_observation.ipynb  # Notebook 2 — annotated & extended
├── requirements.txt                                     # Python dependencies
├── .gitignore
└── README.md
```

### Notebook 1 — `Student_Performance_Analysis.ipynb`

A concise, readable baseline analysis. Each section contains code and minimal commentary — suited as a clean starting point or a quick reference.

| Section | Content |
|---------|---------|
| 1. Load dataset | Fetch from UCI via `ucimlrepo`, inspect shape and columns |
| 2. Quick overview | Data types, missing values, descriptive statistics |
| 3. Variable selection | Focus on the most analytically relevant features |
| 4. Correlation analysis | Pearson correlations with G3, numeric heatmap |
| 5. Visualizations | Grade distribution, study time vs G3, absences vs G3, grade by failures |
| 6. Simple interpretation | Key takeaways from the analysis |
| 7. Predictive baseline | sklearn Pipeline, LinearRegression, MAE and R² on a single 80/20 split |

### Notebook 2 — `Student_Performance_Analysis_with_observation.ipynb`

An extended version of Notebook 1 with written observations after each section, improved visualizations, and a more rigorous modelling approach.

| Section | What is added vs Notebook 1 |
|---------|-----------------------------|
| 2. Quick overview | Missing values checked on **all** columns (not just top 10) |
| 4. Correlation analysis | Annotated **seaborn heatmap** with values in each cell + written analysis of key findings |
| 5. Visualizations | **Boxplot** for study time (more readable for an ordinal variable), **2 additional plots** for `internet` and `higher` education aspiration |
| 6. Predictive baseline | **Two models compared**: Model A (all features incl. G1/G2) vs Model B (habits only, excl. G1/G2) — evaluated with **5-fold cross-validation** + coefficient analysis |
| Throughout | **`### Observations` blocks** after each section with concrete values and interpretation |
| 7. Limitations | Explicit discussion of scope, assumptions, and possible next steps |

---

## Setup and usage

**Requirements**: Python 3.8+

```bash
# Install dependencies
pip install -r requirements.txt

# Launch either notebook
jupyter notebook Student_Performance_Analysis.ipynb
jupyter notebook Student_Performance_Analysis_with_observation.ipynb
```

`requirements.txt` includes: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `ucimlrepo`, `jupyter`.

---

## Limitations

- **Grade autocorrelation**: G1 and G2 are intermediate grades of the same course — their very high correlation with G3 dominates any model that includes them (R² ≈ 0.85). Notebook 2 addresses this explicitly with a second model trained without them (R² ≈ 0.32), giving a more honest picture of how much lifestyle and habit variables actually explain.
- **Single course**: results may not generalise beyond this Portuguese secondary school math dataset. A Portuguese language dataset from the same source is also available.
- **No causal inference**: correlations do not imply causation — e.g. students who aspire to higher education may differ in unmeasured ways.
- **G3 zeros**: ~7% of students scored 0, likely representing dropouts rather than low performers, which can distort regression estimates.
