# XGBoost Classification

An educational notebook that classifies breast-tumour measurement records using XGBoost. It reports test-set accuracy, a confusion matrix and 10-fold cross-validation on the training split.

**Python · XGBoost · pandas · scikit-learn**

## Dataset and fixes

The included file is [Data (3).csv](Data%20%283%29.csv): **683 rows**, nine measurement features, a sample identifier and a class column. Original labels are **2 (benign)** and **4 (malignant)**.

The updated [notebook](xg_boost.ipynb):

- Reads the actual filename instead of the missing `Data.csv`.
- Drops `Sample code number` from model inputs.
- Encodes labels as 0 and 1 for XGBClassifier; prints the original label mapping.
- Uses `random_state=0` and limits model threads to two.

## Workflow

```text
CSV → remove identifier → encode labels → 80/20 split
    → XGBoost → test predictions → training-set cross-validation
```

The split contains **546 training rows and 137 test rows**, using `random_state=0`. Tree models do not require StandardScaler here.

## Verified results

The updated notebook ran end to end during review:

| Check | Result |
| :--- | :--- |
| Test accuracy | 97.08% (133 / 137 correct) |
| Training-set 10-fold CV mean | 96.71% |
| CV standard deviation | 1.96 percentage points |

Test confusion matrix, using encoded labels 0 and 1: `[[85, 2], [2, 48]]`. These results describe this small dataset and split. Cross-validation is not external clinical validation; this learning notebook is not a medical diagnostic tool.

## Run it

Open the notebook in Jupyter or Google Colab. Keep its CSV/TSV in the notebook's working folder; opening a notebook from GitHub in Colab does not automatically upload the data.

For a local setup, clone this repository, create and activate a virtual environment, then run:

```bash
python -m pip install numpy pandas matplotlib scikit-learn xgboost notebook
python -m notebook
```

Run cells from top to bottom.

[Verification notes](VALIDATION.md) · Tested versions: `requirements.txt`.
