# 🧪 Ab-NeurIPS-p1 code (Explained)

This repository contains a baseline solution for the **Open Polymer Prediction 2025** competition hosted on Kaggle. This guide explains **how the code works step by step**, including data processing, feature extraction, model training, and submission generation.

---

## 🏆 Score

✅ Public Leaderboard Score: **0.075**

---

## 📘 Step-by-Step Code Explanation

### **STEP 1: Load Basic Packages and Data**

- Load the essential libraries like `pandas`, `numpy`, and read the `train`, `test`, and `sample_submission.csv` files.
- Define the five target polymer properties:  
  `['Tg', 'FFV', 'Tc', 'Density', 'Rg']`.

---

### **STEP 2: Install RDKit Offline**

- RDKit is a cheminformatics library for computing molecular descriptors from SMILES strings.
- Since internet access is disabled, RDKit is installed from a local `.whl` file.

---

### **STEP 3: Feature Extraction Using RDKit**

- For each SMILES string:
  - Convert it into a molecule using RDKit.
  - Compute ~200 chemical descriptors using `rdkit.Chem.Descriptors`.
- This results in a structured feature matrix for both the training and test sets.
- Uses `tqdm` for progress tracking.

---

### **STEP 4: Data Preprocessing**

- Drop the `'id'` column from the feature matrices.
- Fill any missing values with the **mean values from the training data**.
- Prepare `X_train`, `X_test`, and `y_train` for modeling.

---

### **STEP 5: Model Training with LightGBM**

- For each target property (`Tg`, `FFV`, etc.):
  - Filter out rows where the target is missing.
  - Split the data into train and validation sets.
  - Train a **LightGBM regressor** with early stopping.
  - Evaluate using **Mean Absolute Error (MAE)**.
  - Predict target values for the test set.

- Store both:
  - Validation scores (for diagnostics)
  - Test set predictions

---

### **STEP 6: Submission File Creation**

- Combine all predictions into a single DataFrame.
- Format according to the sample submission file: columns include `'id'` and all five target properties.
- Save the result as `submission.csv` for uploading to Kaggle.

---

## 💡 Summary

This baseline pipeline:
- Uses **RDKit** for SMILES-to-feature conversion,
- Applies **LightGBM** for regression modeling,
- Achieves a leaderboard score of **0.075**,
- Is fully offline-compatible and runs under 9 hours.

---

## 📌 Future Improvements

- Add molecular fingerprints (e.g. Morgan) as features
- Explore deep learning models like Graph Neural Networks (GNNs)
- Implement multi-target models to capture inter-target relationships
- Feature selection to reduce noise and improve performance

---

## 🙌 Credits

Built using the NeurIPS 2025 dataset for Open Polymer Prediction.
