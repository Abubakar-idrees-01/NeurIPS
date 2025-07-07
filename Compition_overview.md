# 🧪 Open Polymer Prediction 2025

Welcome to my repository for the **Open Polymer Prediction 2025** competition! This challenge aims to accelerate the discovery of sustainable and high-performance polymers using machine learning.

---

## 🚀 Overview

Polymers are vital materials in industries ranging from healthcare to electronics and sustainability. Despite their importance, predicting their real-world properties from chemical structures remains a complex task due to limited high-quality data.

In this competition, hosted on [platform name], participants are provided with a **large-scale open-source dataset** (10x larger than existing resources) to build models that can predict the behavior of polymers based on their chemical structure (SMILES strings).

---

## 🎯 Objective

Predict **five fundamental polymer properties** from SMILES:

1. **Tg** – Glass Transition Temperature  
2. **FFV** – Fractional Free Volume  
3. **Tc** – Thermal Conductivity  
4. **Density**  
5. **Rg** – Radius of Gyration  

These properties are derived from molecular dynamics simulations and are critical in assessing polymer performance.

---

## 📊 Evaluation Metric

The competition uses a **Weighted Mean Absolute Error (wMAE)** to score submissions. This metric ensures:
- Equal contribution from each property (range normalization)
- Emphasis on rarer properties (inverse square-root sample weighting)
- Normalized total weight across all tasks

---

## 🗂️ Submission Format

Submit a CSV file named `submission.csv` with the following structure:

```csv
id,Tg,FFV,Tc,Density,Rg
2112371,0.0,0.0,0.0,0.0,0.0
2021324,0.0,0.0,0.0,0.0,0.0
...
