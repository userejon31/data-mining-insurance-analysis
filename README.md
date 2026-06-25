# Exploratory Data Analysis — Medical Insurance Costs

**Course:** Data Mining · Universidad Politécnica de Yucatán  
**Dataset:** [Insurance Premium Prediction](https://www.kaggle.com/datasets/noordeen/insurance-premium-prediction) — Noorden, M. (2019). Kaggle.

---

## Overview

This project applies the **Data Understanding** phase of the CRISP-DM methodology to a U.S. medical insurance dataset. The goal is to profile the data, uncover initial patterns, detect quality issues, and produce evidence-backed recommendations before any modelling work begins.

The analysis is delivered as a self-contained Jupyter Notebook with an aquamarine visual theme.

---

## Dataset

| Property | Value |
|:---|:---|
| Observations | 1,338 rows |
| Variables | 7 (6 inputs + 1 target) |
| Target variable | `charges` — annual medical cost billed to insurance (USD) |
| Source | Kaggle · Noorden, M. (2019) |

### Variables

| Variable | Type | Description |
|:---|:---|:---|
| `age` | Numerical — Discrete | Age of the primary beneficiary (years) |
| `sex` | Categorical — Nominal | Biological sex of the beneficiary |
| `bmi` | Numerical — Continuous | Body mass index (kg/m²) |
| `children` | Numerical — Discrete | Number of dependents covered by the plan |
| `smoker` | Categorical — Binary | Whether the beneficiary smokes |
| `region` | Categorical — Nominal | U.S. residential region (NE / NW / SE / SW) |
| `charges` | Numerical — Continuous | Total annual medical costs billed to insurance |

---

## Notebook Structure

The notebook (`insurance_eda.ipynb`) is organised into eight sections:

1. **Initial Description and Variable Classification** — dataset dimensions, dtypes, and a manual variable taxonomy.
2. **Descriptive Exploration** — summary statistics, histograms, boxplots, frequency tables, and bar charts.
3. **Initial Data Quality Review** — null values, duplicates, category validation, range checks, and identification of encoding errors.
4. **Relationship Between Variables and the Target** — boxplots by group (sex, smoker) and scatter plots (charges vs. BMI / age) differentiated by smoking status.
5. **Correlation Analysis** — Pearson heatmaps for numerical and encoded variables, plus a ranked bar chart of |r| with `charges`.
6. **Outliers in Charges** — IQR-based detection with Q1/Q3/bounds, outlier count, profile table, and a dedicated boxplot.
7. **Additional Exploration** — grouped bar (BMI category × smoker), split violin (age range × smoker), and log-transform comparison.
8. **Conclusions and Recommendations** — six evidence-backed findings, a data cleaning action table, and a proposed initial feature set for linear regression.

---

## Key Findings

- **Smoking is the dominant cost driver** — smokers pay on average 4× more than non-smokers (|r| ≈ 0.79 with charges).
- **BMI × Smoker interaction** — the cost jump from overweight to obese is ~+15,000 USD only among smokers; non-smokers show a flat trend. An `obese_smoker` flag is recommended.
- **Age contributes a steady linear trend** (|r| ≈ 0.30) across all segments.
- **Sex has negligible predictive value** — distributions are nearly identical between male and female beneficiaries.
- **charges is right-skewed** (skewness > 1.5); a log transformation stabilises variance and is recommended before modelling.
- **Decimal-encoding errors** were detected in a small number of `charges` records (e.g., 3,871,122 instead of 38,711.22) — these must be corrected in the cleaning stage.

---

## Figures

All plots are saved to `data/` and embedded in the notebook output.

| File | Content |
|:---|:---|
| `fig_histograms.png` | Distributions of all numerical variables |
| `fig_boxplots_num.png` | Boxplots of all numerical variables |
| `fig_barcharts_cat.png` | Frequency bar charts for categorical variables |
| `fig_charges_groups.png` | Charges by sex and smoking status |
| `fig_scatter_bmi_age.png` | Charges vs. BMI and Age, coloured by smoker |
| `fig_corr_num.png` | Correlation heatmap — numerical variables |
| `fig_corr_full.png` | Correlation heatmap — all encoded variables |
| `fig_corr_charges.png` | Ranked correlation of each variable with charges |
| `fig_boxplot_charges.png` | Outlier boxplot for charges (IQR method) |
| `fig_bmi_smoker_segment.png` | Median charges by BMI category × smoker |
| `fig_violin_age_smoker.png` | Split violin: charges by age range × smoker |
| `fig_log_charges.png` | Raw vs. log-transformed charges distribution |

---

## Project Structure

```
data-mining-insurance-analysis/
├── data/
│   ├── insurance.csv          # Raw dataset
│   └── fig_*.png              # Generated figures
├── insurance_eda.ipynb        # Main analysis notebook (fully executed)
├── insurance_eda.html         # Self-contained HTML export
└── README.md
```

---

## Setup

```bash
# Clone the repository
git clone https://github.com/<your-username>/data-mining-insurance-analysis.git
cd data-mining-insurance-analysis

# Create and activate a virtual environment
python3 -m venv .venv
source .venv/bin/activate

# Install dependencies
pip install pandas numpy matplotlib seaborn scipy jupyter

# Launch the notebook
jupyter notebook insurance_eda.ipynb
```

> Alternatively, open `insurance_eda.html` directly in any browser — no installation required.

---

## Dependencies

| Package | Purpose |
|:---|:---|
| `pandas` | Data loading and manipulation |
| `numpy` | Numerical operations |
| `matplotlib` | Base plotting engine |
| `seaborn` | Statistical visualisations (heatmaps, violin plots) |
| `scipy` | Skewness and kurtosis calculations |

---

## License

This project is submitted for academic evaluation at Universidad Politécnica de Yucatán. The dataset is publicly available on Kaggle under its original license.
