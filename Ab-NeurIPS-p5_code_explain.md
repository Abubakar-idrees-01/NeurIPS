# Polymer Property Prediction

This project implements a pipeline for predicting multiple polymer properties from SMILES (Simplified Molecular Input Line Entry System) strings using cheminformatics and machine learning techniques.

---

## 🔧 What the Code Does

### 1. **Load Required Libraries**
The script starts by importing standard data science libraries:
- `pandas`, `numpy` for data handling
- `sklearn` and `lightgbm` for modeling
- `rdkit` for molecular feature extraction
- `tqdm` for progress bars

It also installs RDKit from a local wheel file to extract molecular features from SMILES.

---

### 2. **Load the Data**
It reads three CSV files:
- `train.csv`: SMILES strings + known target properties
- `test.csv`: SMILES strings to predict on
- `sample_submission.csv`: Template for saving results

---

### 3. **Feature Engineering**
From each SMILES string, the following features are extracted:

- **Morgan Fingerprints (FP)**: A bit-vector representation of molecular substructures (length = 2048).
- **Molecular Descriptors**: Numerical descriptors like molecular weight, number of rings, etc.

The function `smiles_to_features()` handles this with error handling for malformed SMILES.

---

### 4. **Concatenate Features**
The fingerprint and descriptor features are combined into a single feature matrix for both training and testing data.

---

### 5. **Data Cleaning & Imputation**
- Replace infinite values with NaNs.
- Drop columns in the training set that are entirely NaN.
- Impute all remaining NaNs using column-wise means (using `SimpleImputer`).

---

### 6. **Target Handling**
Only rows in `train.csv` with at least one non-null target (`Tg`, `FFV`, `Tc`, `Density`, `Rg`) are kept. Targets are imputed with column means for modeling.

---

### 7. **Train/Validation Split**
The training set is split into:
- **Training set**: 90%
- **Validation set**: 10%

This is used to evaluate model performance.

---

### 8. **Model Training (with Progress Bars)**
For each target:
- Two models are trained:
  - `LightGBMRegressor` with early stopping
  - `RandomForestRegressor`
- Both models are trained on the training set and evaluated on the validation set.
- Their predictions are averaged for a final prediction per target.

Progress bars show training status using `tqdm`.

---

### 9. **Final Predictions**
Once the models are validated:
- They are retrained on the full training data (train + validation).
- Predictions are made on the test set.

---

### 10. **Save Submission**
The predictions are saved to `submission.csv` in the same format as `sample_submission.csv`.

---

## 🛡 Error Handling in the Code
- Invalid SMILES: Handled safely with try/except.
- Infinities in features: Replaced with NaNs, then imputed.
- NaNs in targets: Filled with mean values.
- Misaligned indices: `.reset_index(drop=True)` ensures alignment after filtering.
- Model training errors: Avoided by converting to `.values` before fitting.

---

## 🧪 Target Columns

The following five columns are the regression targets:
- `Tg`
- `FFV`
- `Tc`
- `Density`
- `Rg`

Each is modeled separately.

---

## 📊 Output

The final result is a `submission.csv` file containing the predicted values for each target column, aligned by test sample `id`.

---

## 💡 Summary

This pipeline:
- Automatically extracts rich molecular features
- Cleans and imputes data robustly
- Trains two different regressors per target
- Averages predictions for better generalization
- Handles all edge cases gracefully

It’s modular and can be extended to new molecular properties or features easily.

---
