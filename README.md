# Assignment 1: What Drives the Price of a Car?

Author: Mbuya

Exploratory data analysis (EDA) and feature selection on the Automobile dataset (`automobileEDA.csv`, 201 cars, 29 columns). The goal is to find which variables influence a car's price the most and to turn the findings into a pricing recommendation for a car dealer.

## Contents

| File | Description |
|---|---|
| `Assignment1_Mbuya.ipynb` | The full analysis notebook (code, outputs and a short explanation after each output) |
| `automobileEDA.csv` | Input data (must be in the same folder as the notebook) |
| `Mbuya Data.csv` | Cleaned dataset, created by the notebook in Section 1.7 |
| `requirements.txt` | Python packages needed to run the notebook |

## Notebook structure

| Section | What it covers |
|---|---|
| 1. Data exploration and cleaning | Feature types, missing values, duplicates, misspelled makes, impossible engine measurements, outliers; saves `Mbuya Data.csv` |
| 2. Descriptive statistics | Summary statistics, frequency counts, distributions of price and of continuous and categorical variables |
| 3. Average price by group | Mean price by drive-wheels, body style, their combination, and make |
| 4. Effect on price | (a) Continuous variables: correlation and regression; (b) categorical variables: ANOVA and Kruskal-Wallis; (c) pairs of categorical variables: Cramér's V, chi-square, interaction of aspiration and drive-wheels |
| 5. Feature selection and recommendation | Filter method, mutual information and random-forest permutation importance, cross-validated check, VIF, and the dealer recommendation |

## Data cleaning summary

- **Missing values:** 5 filled (4 `stroke` values for Mazda rotary engines filled with the median; 1 `horsepower-binned` value for the Jaguar set to High).
- **Duplicates:** no exact duplicates. 14 rows differ only in price and were kept as genuine trim levels.
- **Labels:** `peugot` and `alfa-romero` corrected (14 rows).
- **Engine measurements:** 4 rows with typos in bore or stroke corrected, verified by recomputing engine displacement.
- **Outliers:** kept when they are real vehicles (luxury cars, diesel compression ratios). Only data-entry errors were changed.

## Key findings

- **Most influential variables:** `curb-weight`, `engine-size`, `horsepower`, fuel economy (`highway-mpg`, `city-mpg`), `width` and `make`. Engine size alone explains about 76% of the variance in price, and `make` alone about 80%.
- **Cars fall into three price tiers by make:** luxury (Jaguar, Mercedes-Benz, Porsche, BMW), middle, and budget.
- **Drivetrain:** rear-wheel-drive cars cost about twice as much as front-wheel-drive cars. The highest-priced segment is the rear-wheel-drive hardtop.
- **Turbo premium depends on drivetrain:** about +3,800 for front-wheel drive, no reliable premium for rear-wheel drive.
- **Not useful for pricing:** `num-of-doors`, `fuel-type`, `peak-rpm`, `compression-ratio`, `stroke`, `height`, `symboling`, `normalized-losses`.
- **Model check:** 5 to 6 features predict price about as well as all 25 (cross-validated R² of about 0.88 to 0.89).

See Section 5.2 of the notebook for the full recommendation and limitations.

## Requirements

- Python 3.9 or newer
- pandas, numpy, scipy, scikit-learn, matplotlib, seaborn
- Jupyter (or VS Code with the Jupyter extension)

## How to run

1. Create and activate a virtual environment:
   ```
   python -m venv .venv
   .venv\Scripts\activate          # Windows
   source .venv/bin/activate       # Linux / macOS
   ```
2. Install the packages:
   ```
   python -m pip install pandas numpy scipy scikit-learn matplotlib seaborn jupyter
   ```
   (or `python -m pip install -r requirements.txt`)
3. Put `automobileEDA.csv` in the same folder as the notebook.
4. Open `Assignment1_Mbuya.ipynb` and choose **Run All**. The cleaned file `Mbuya Data.csv` is written to the same folder.

## Limitations

The data has only 201 cars from one period, and some groups are very small (for example 3 rear-engine cars and 1 Mercury), so their averages are only indications. The results show association, not cause, and should be checked against current market prices before use.
