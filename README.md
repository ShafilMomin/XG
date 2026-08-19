# XGBoost — Breast Cancer Classification

Classifying breast tumours as **benign or malignant** using **XGBoost**, evaluated with a confusion matrix and validated with **10-fold cross validation** for a robust, variance-aware accuracy estimate.

---

## What's Inside

| File | Description |
|---|---|
| `xg_boost.ipynb` | Full pipeline — XGBoost training, evaluation, and K-Fold CV |
| `Data.csv` | Wisconsin Breast Cancer dataset (683 samples, 10 features) |

---

## Dataset — `Data.csv`

The **Wisconsin Breast Cancer Dataset** contains cytological features extracted from fine-needle aspirate (FNA) samples of breast masses. Each feature is scored on a scale of 1–10 by a clinician.

| Column | Description |
|---|---|
| `Sample code number` | Patient ID (dropped as a feature via `iloc`) |
| `Clump Thickness` | Thickness of cell clumps |
| `Uniformity of Cell Size` | Consistency in cell size |
| `Uniformity of Cell Shape` | Consistency in cell shape |
| `Marginal Adhesion` | Tendency of cells to stick together |
| `Single Epithelial Cell Size` | Size of single epithelial cells |
| `Bare Nuclei` | Proportion of nuclei without cytoplasm |
| `Bland Chromatin` | Uniformity of chromatin texture |
| `Normal Nucleoli` | Visibility of nucleoli |
| `Mitoses` | Rate of cell division |
| `Class` | **Target** — `2` = Benign, `4` = Malignant |

**Class distribution:** 444 benign · 239 malignant

---

## Pipeline

```
Load Data.csv  (683 samples × 10 features)
        ↓
Train/Test Split   (80% / 20%, random_state=0)
        ↓
XGBClassifier      (default hyperparameters)
        ↓
Confusion Matrix + Accuracy Score  ← single-split result
        ↓
10-Fold Cross Validation           ← reliable estimate
Mean Accuracy  ±  Standard Deviation
```

> No feature scaling is needed — XGBoost is a tree-based ensemble and is invariant to feature magnitude.

---

## Why XGBoost?

XGBoost (Extreme Gradient Boosting) builds an ensemble of decision trees sequentially, where each new tree corrects the residual errors of the previous ones. It is known for:

- High accuracy out of the box with default parameters
- Built-in regularisation (L1 + L2) to prevent overfitting
- Robust performance on tabular data without feature scaling
- Fast training via parallel tree construction

---

## Why K-Fold Cross Validation?

A single train/test split can produce an optimistic or pessimistic accuracy depending on how the data happened to be split. 10-fold CV trains and evaluates the model 10 times on different partitions of the training set, then reports:

- **Mean Accuracy** — the true expected performance
- **Standard Deviation** — how stable the model is across different splits

A low standard deviation alongside high mean accuracy indicates the model generalises reliably.

---

## Requirements

```bash
pip install numpy pandas matplotlib scikit-learn xgboost
```

Python 3.7+ recommended.

---

## Usage

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
jupyter notebook xg_boost.ipynb
```

Ensure `Data.csv` is in the same directory as the notebook before running.

---

## File Structure

```
.
├── Data.csv
└── xg_boost.ipynb
```
