# Hedonic Diamond Pricing: Non-Linearities in the Gemstone Market

**Author:** Kekeli  
**Course:** AGEC 5213 — Econometrics  
**Date:** April 29, 2026

## Project Overview

This project investigates how to correctly predict diamond prices given the non-linear relationship between carat weight, cut grade, color grade, clarity grade, and transaction price. Using a dataset of ~50,000 diamond transactions, we compare five parametric OLS models against four non-parametric machine learning benchmarks.

**Key Finding:** Gradient boosting outperforms the best OLS model by 48% in out-of-sample RMSE, demonstrating that the hedonic price surface of diamonds contains non-linearities too complex for parametric models to fully capture.

---

## Quick Start

### Requirements
- **R** (version 3.6+) — Download from https://cran.r-project.org/
- **R Studio Desktop** (free) — Download from https://www.rstudio.com/products/rstudio/download/
- **Required R packages** (install via R Console):
  ```R
  install.packages(c("tidyverse", "dplyr", "ggplot2", "readr", "rpart", 
                     "rpart.plot", "randomForest", "gbm", "forecast"))
  ```

### Running the Analysis

1. **Open R Studio**
2. **File → Open File → Select `Econometrics_Project.Rmd`**
3. **Click "Knit"** (top of editor) to run the entire analysis
   - All EDA plots and model specifications will run
   - Output appears in the Viewer pane or as HTML

Alternatively, run individual code chunks:
- Click the green **Play button** on any code chunk to run just that section

---

## Files in This Repository

```
Diamond_Pricing_Project/
├── .gitignore                           (prevents R temp files)
├── README.md                            (this file)
├── Econometrics_Project.Rmd             (main R code — EDA + models)
├── Econometrics_Project_Final.pdf       (full paper with results)
└── diamonds.csv                         (dataset: ~50,000 transactions)
```

---

## Dataset

**Source:** Kaggle — Diamond Dataset  
**Size:** ~50,000 observations  
**Variables:**
- `price` — Transaction price (USD)
- `carat` — Diamond weight (carats)
- `cut` — Cut grade (Fair, Good, Very Good, Premium, Ideal)
- `color` — Color grade (J to D, where D is colorless)
- `clarity` — Clarity grade (I1 to IF, where IF is internally flawless)
- `depth`, `table`, `x`, `y`, `z` — Physical dimensions

---

## Model Specifications

### Parametric Models (OLS)
1. **Model 1:** Baseline linear (integer-encoded quality)
2. **Model 2:** Log-linear (integer-encoded quality)
3. **Model 3:** Log-linear with dummy variables
4. **Model 4:** Model 3 + Carat × Cut interactions
5. **Model 5:** Model 3 + Carat × Clarity interactions

### Non-Parametric Models
- **CART:** Single regression tree
- **Bagging:** 50 bootstrap trees
- **Random Forest:** 200 trees
- **Gradient Boosting:** 200 trees with sequential learning

---

## Key Results

| Model | RMSE ($) | MAPE (%) |
|-------|----------|----------|
| Model 1 (Baseline Linear) | 1,195 | 44.45% |
| Model 3 (Dummy Variables) | 1,164 | 12.10% |
| Model 4 (Carat × Cut) | 1,127 | 11.84% |
| **Gradient Boosting** | **586** | **10.51%** |

**Takeaway:** Moving from baseline to Model 3 resolves most misspecification. Gradient boosting achieves 48% lower RMSE, revealing the cost of linearity.

---

## Econometric Highlights

### Heteroscedasticity
- **Breusch-Pagan test:** BP = 3,718.7 (p < 0.001)
- **Remedy:** HC3 robust standard errors applied

### Grade Premia (Model 3, log-linear)
- **Cut (Ideal vs. Fair):** +15% premium
- **Color (D vs. J):** +18.5% premium
- **Clarity (IF vs. I1):** +60% premium

### Interaction Effects
- Carat × Cut interactions: statistically significant
- Carat × Clarity interactions: statistically significant

---

## Project Limitations

This analysis uses only **intrinsic physical attributes** of diamonds. The following demand-side variables are unavailable:
- Buyer demographics
- Macroeconomic conditions at time of transaction
- Retail channel (online, brick-and-mortar, auction)
- Temporal market trends

Under the assumption that these factors are approximately constant across the cross-section, bias is minimal.

---

## References

- Bajari, P., & Benkard, C. L. (2005). Demand estimation with heterogeneous consumers and unobserved product characteristics. *Journal of Political Economy*, 113(6), 1239–1276.
- Halvorsen, R., & Palmquist, R. (1980). The interpretation of dummy variables in semilogarithmic equations. *American Economic Review*, 70(3), 474–475.
- Malpezzi, S. (2003). Hedonic pricing models: A selective and applied review. In *Housing economics and public policy* (pp. 67–89). Blackwell.
- Rosen, S. (1974). Hedonic prices and implicit markets. *Journal of Political Economy*, 82(1), 34–55.

---

## Questions or Issues?

If you encounter package errors:
1. Check all required packages are installed (see Quick Start)
2. Verify `diamonds.csv` is in the same folder as `.Rmd`
3. Update R and R Studio to latest versions

Good luck! 📊
