# Student Performance Analysis

Exploratory data analysis and baseline regression model built on the **UCI Student Performance** dataset. The project examines which factors — study habits, past failures, absences — are associated with final grades.

---

## Key results

| Metric | Value |
|--------|-------|
| Model | Linear Regression |
| MAE | 0.765 (on a 0–20 scale) |
| R² | 0.849 |

Notable correlations with final grade (G3):
- Prior grades G1 and G2: **+0.83 / +0.92** (strongest predictors)
- Past failures: **−0.39**
- Study time: **+0.25**
- Daily alcohol consumption: **−0.21**

---

## Dataset

**Source**: [UCI Machine Learning Repository – Student Performance](https://archive.ics.uci.edu/dataset/320/student+performance)  
**Students**: 649 (Portuguese secondary school, math course)  
**Features**: 33 variables covering demographics, family background, lifestyle, and academic history  
**Target**: `G3` — final period grade (0–20)

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
├── Student_Performance_Analysis.ipynb   # Main analysis notebook
├── requirements.txt                     # Python dependencies
└── README.md
```

### Notebook sections

| Section | Content |
|---------|---------|
| 1. Load dataset | Fetch from UCI via `ucimlrepo`, inspect shape and columns |
| 2. Quick overview | Data types, missing values, descriptive statistics |
| 3. Variable selection | Focus on the most analytically relevant features |
| 4. Correlation analysis | Pearson correlations with G3, full numeric heatmap |
| 5. Visualizations | Grade distribution, study time vs G3, absences vs G3, grade by failures |
| 6. Interpretation | Summary of observed patterns |
| 7. Predictive baseline | sklearn Pipeline with preprocessing, LinearRegression, MAE and R² evaluation |

---

## Setup and usage

**Requirements**: Python 3.8+

```bash
# Install dependencies
pip install -r requirements.txt

# Launch the notebook
jupyter notebook Student_Performance_Analysis.ipynb
```

**Dependencies** (`requirements.txt`):
```
pandas
numpy
matplotlib
scikit-learn
ucimlrepo
jupyter
```

The dataset is fetched automatically at runtime via `ucimlrepo` — no manual download needed.

---

## Limitations

- G1 and G2 are intermediate grades of the same course: their very high correlation with G3 dominates the model. A model trained without them would give a clearer picture of the impact of lifestyle variables.
- Single train/test split (80/20) on 649 rows — cross-validation would give more reliable performance estimates.
- Analysis covers only the math dataset; a Portuguese language dataset is also available from the same source.
