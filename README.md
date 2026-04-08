<div align="center">

<!-- Header Banner -->
<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:0D2B4E,100:008E9B&height=200&section=header&text=Cancer%20Data%20Analysis&fontSize=48&fontColor=ffffff&fontAlignY=38&desc=Global%20Cancer%20Patients%20Dataset%20%7C%202015–2024&descAlignY=58&descSize=18" />

<br/>

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org)

<br/>

> **A comprehensive exploratory and predictive analysis of 50,000 global cancer patients, covering demographics, risk factors, treatment economics, and machine learning-based severity prediction.**

</div>

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Project Structure](#-project-structure)
- [Analysis Modules](#-analysis-modules)
- [Key Findings](#-key-findings)
- [ML Models](#-ml-models)
- [Installation](#-installation)
- [Usage](#-usage)
- [Technologies Used](#-technologies-used)
- [Results Summary](#-results-summary)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🔬 Overview

This project performs a full-stack data analysis pipeline on a global cancer patient dataset spanning **2015–2024**. The analysis covers:

- 📊 **Descriptive statistics** across age, gender, country, cancer type, and stage
- 🔗 **Correlation analysis** between risk factors and cancer severity
- 🩺 **Early-stage diagnosis rates** across 8 cancer types
- 💰 **Economic burden analysis** by demographics and geography
- 🤖 **Machine learning models** (Random Forest) for severity prediction
- 🧪 **Hypothesis testing** (Pearson, Spearman, Kruskal-Wallis, OLS) on clinical outcomes

---

## 📂 Dataset

| Property | Details |
|---|---|
| **Source** | `global_cancer_patients_2015_2024.csv` |
| **Records** | 50,000 patient entries |
| **Features** | 15 variables |
| **Period** | 2015 – 2024 |
| **Countries** | 10 (Australia, Brazil, Canada, China, Germany, India, Japan, Pakistan, UK, USA) |
| **Missing Values** | None |
| **Duplicates** | None |

### Feature Description

| Feature | Type | Description |
|---|---|---|
| `Patient_ID` | object | Unique patient identifier |
| `Age` | int | Patient age (20–89 years) |
| `Gender` | object | Male / Female / Other |
| `Country_Region` | object | Country of patient origin |
| `Year` | int | Year of diagnosis (2015–2024) |
| `Genetic_Risk` | float | Genetic predisposition score (0–10) |
| `Air_Pollution` | float | Environmental exposure score (0–10) |
| `Alcohol_Use` | float | Alcohol consumption score (0–10) |
| `Smoking` | float | Smoking intensity score (0–10) |
| `Obesity_Level` | float | BMI-based obesity score (0–10) |
| `Cancer_Type` | object | Type of cancer (8 types) |
| `Cancer_Stage` | object | Stage 0, I, II, III, or IV |
| `Treatment_Cost_USD` | float | Total treatment cost in USD |
| `Survival_Years` | float | Years survived post-diagnosis |
| `Target_Severity_Score` | float | Composite cancer severity score |

---

## 📁 Project Structure

```
cancer-data-analysis/
│
├── 📓 Cancer_data_Analysis.ipynb     # Main analysis notebook
├── 📄 global_cancer_patients_2015_2024.csv  # Dataset
├── 📋 README.md                      # Project documentation
├── 📊 report/                        # Generated plots and figures
│   ├── age_distribution.png
│   ├── risk_factor_correlations.png
│   ├── feature_importance.png
│   └── ...
└── 📦 requirements.txt               # Python dependencies
```

---

## 🧩 Analysis Modules

### 1. 📈 Descriptive Analysis
- Age distribution (KDE + Histogram) — Mean: **54.4 years**, Range: 20–89
- Gender distribution — Male (16,796) / Female (16,709) / Other (16,495)
- Country/Region distribution — ~5,000 patients per country (balanced)
- Cancer type & stage distribution — 8 types, 5 stages (~equal representation)
- Treatment cost distribution — Mean: **$52,467**, Range: $5K–$100K (uniform, no skewness)

### 2. 🔬 Risk Factor vs Severity Analysis
Linear regression analysis of 5 risk factors against `Target_Severity_Score`:

| Risk Factor | R² Value | Slope | Interpretation |
|---|---|---|---|
| Smoking | 0.23 | 0.20 | Strong positive link |
| Genetic Risk | 0.23 | 0.20 | Near-equal to smoking |
| Alcohol Use | 0.13 | 0.15 | Moderate contributor |
| Air Pollution | 0.13 | 0.15 | Environmental impact |
| Obesity Level | 0.06 | — | Weakest predictor |

> All risk factors show **positive slopes** — higher risk consistently maps to higher severity.

### 3. 🏥 Early-Stage Diagnosis Proportion
Proportion of patients diagnosed at Stage 0 or Stage I, by cancer type:

| Cancer Type | Early Diagnosis (%) |
|---|---|
| Liver | 40.61% (**highest**) |
| Colon | 40.42% |
| Skin | 40.41% |
| Prostate | 40.19% |
| Cervical | 39.86% |
| Leukemia | 39.53% |
| Breast | 39.47% |
| Lung | 38.43% (**lowest**) |

### 4. 💰 Economic Burden Analysis
- Treatment costs vary significantly across countries — USA & Australia highest; India & Pakistan lowest
- No significant gender-based cost differences observed
- Costs rise with age, especially 61+ cohorts in developed nations
- Public healthcare nations (Canada, Germany, UK) show stable cross-age costs

### 5. 🧪 Hypothesis Testing

| Test | Variables | Method | Result |
|---|---|---|---|
| Cost vs Survival | Treatment Cost ↔ Survival Years | Pearson + Spearman | No significant correlation |
| Stage vs Cost | Cancer Stage ↔ Treatment Cost | Kruskal-Wallis (p=0.4254) | No significant difference |
| Stage vs Survival | Cancer Stage ↔ Survival Years | Kruskal-Wallis (p=0.6033) | No significant difference |
| Interaction Effect | Genetic Risk × Smoking → Severity | OLS Regression (p=0.628) | No amplification effect |

---

## 🤖 ML Models

### Random Forest — Target Severity Score Prediction

```
Model        : RandomForestRegressor
n_estimators : 200
max_depth    : None
Train R²     : 0.969
Test R²      : 0.775
```

**Feature Importances:**

```
Smoking          ████████████████████  23.4%
Genetic Risk     ███████████████████   22.9%
Treatment Cost   █████████████████     21.3%
Alcohol Use      ██████████            12.9%
Air Pollution    ██████████            12.7%
Obesity Level    ████                   5.7%
Age / Gender     █                     <1.0%
```

> The model explains **77.5%** of variance in severity score on unseen test data.

---

## 💡 Key Findings

1. **🚬 Smoking & Genetics are the top drivers** of cancer severity — combined they explain ~46% of feature importance in the RF model.
2. **💰 Treatment costs are NOT correlated with survival** — higher spending doesn't equal longer survival, pointing to systemic access inequities rather than quality differences.
3. **🌍 Global cost inequality is stark** — developed nations pay 40–60% more for treatment than developing countries.
4. **📊 Cancer stage does not significantly affect costs or survival** in this dataset (per Kruskal-Wallis tests).
5. **🧬 Genetic risk and smoking do not interact** to amplify severity — their effects appear independent.
6. **🩺 Lung cancer has the lowest early-diagnosis rate (38.4%)** — highlighting a need for better pulmonary screening programs.

---

## ⚙️ Installation

```bash
# Clone the repository
git clone https://github.com/your-username/cancer-data-analysis.git
cd cancer-data-analysis

# Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate       # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### requirements.txt

```
numpy
pandas
matplotlib
seaborn
scipy
scikit-learn
statsmodels
jupyter
```

---

## 🚀 Usage

```bash
# Launch Jupyter Notebook
jupyter notebook Cancer_data_Analysis.ipynb
```

Or run individual sections by cell — the notebook is organized into clearly labeled markdown sections:

- `# Descriptive Analysis`
- `# Determine the relationship between risk factors and cancer severity`
- `# Analyze the proportion of early-stage diagnoses by cancer type`
- `# Identify key predictors of cancer severity and survival years`
- `# Explore the economic burden of cancer treatment`
- `# Assess whether higher treatment cost is associated with longer survival`
- `# Evaluate if higher cancer stages lead to greater treatment costs and reduced survival years`
- `# Examine whether higher genetic risk amplifies the negative effects of smoking`

---

## 🛠️ Technologies Used

| Library | Purpose |
|---|---|
| `pandas` | Data loading, wrangling, groupby analysis |
| `numpy` | Numerical operations |
| `matplotlib` | Plotting and visualization |
| `seaborn` | Statistical visualizations (KDE, heatmap, barplot) |
| `scipy.stats` | Pearson/Spearman correlation, Kruskal-Wallis, Shapiro-Wilk, linregress |
| `statsmodels` | OLS regression with interaction terms |
| `scikit-learn` | Random Forest, Label Encoding, train-test split, R² evaluation |

---

## 📊 Results Summary

| Analysis | Outcome |
|---|---|
| Dataset Quality | ✅ Clean — 0 nulls, 0 duplicates |
| Top Severity Predictor | 🚬 Smoking (23.4% feature importance) |
| Best Early Diagnosis Rate | 🔴 Liver Cancer (40.61%) |
| Worst Early Diagnosis Rate | 🫁 Lung Cancer (38.43%) |
| RF Model Test R² | 🤖 0.775 (strong) |
| Cost-Survival Correlation | ❌ None found |
| Stage-Cost Correlation | ❌ None found (p=0.43) |
| Genetic Risk × Smoking Interaction | ❌ Not significant (p=0.63) |
| Costliest Region | 🇺🇸 USA / 🇦🇺 Australia |
| Most Affordable Region | 🇵🇰 Pakistan / 🇮🇳 India |

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a new branch: `git checkout -b feature/your-feature-name`
3. Make your changes and commit: `git commit -m "Add: your feature description"`
4. Push to the branch: `git push origin feature/your-feature-name`
5. Open a Pull Request

Please ensure your code follows PEP 8 style guidelines and includes appropriate comments.

---

<div align="center">

**If this project helped you, consider giving it a ⭐ on GitHub!**

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:008E9B,100:0D2B4E&height=100&section=footer" />

</div>
