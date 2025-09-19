# 🌬️ Applied Machine Learning – Predictive Maintenance on Wind Turbines

This repository documents an **Applied Machine Learning (AML)** project focused on **predictive maintenance for wind turbines**.  
The goal was to detect potential failures early by analyzing **SCADA sensor data** (temperature, rotation speed, power, windspeed, etc.).  

Due to a **severe class imbalance** (≈0.61% failure cases), the project applied advanced **resampling techniques (SMOTE-ENN)** to improve the recognition of rare failure events.  

---

## 🗂 Repository Structure
- `data/` – wind turbine dataset (SCADA data, from Kaggle)  
- `notebooks/` – Jupyter notebook with full workflow (EDA → preprocessing → modeling → evaluation)  
- `requirements.txt` – dependencies to reproduce results  
- `README.md`, `LICENSE`, `.gitignore`

---

## 📊 Workflow
1. **Exploratory Data Analysis (EDA)**  
   - Detection and removal of anomalous sensor values (e.g., unrealistic inverter temperatures)  
   - Correlation analysis to reduce redundancy  
   - Feature engineering: time-based features (month, season), normalization, target recoding  

2. **Dealing with Imbalance**  
   - Target variable: binary failure label (0 = no error, 1 = error)  
   - Severe imbalance (≈99.4% normal vs. 0.6% failure)  
   - Applied **SMOTE-ENN** to oversample failures and remove noise → balanced dataset  

3. **Modeling**  
   - **Decision Tree** (baseline, interpretable)  
   - **Random Forest** (robust ensemble)  
   - **XGBoost** (gradient boosting, strong performance with imbalanced data)  
   - Hyperparameter tuning with **GridSearchCV**  

4. **Evaluation**  
   - Metrics: Accuracy, Precision, Recall, **F1-score**, ROC-AUC, Confusion Matrix  
   - Focus on **Recall and F1-score** of the minority class (failures)  
   - Cross-validation to ensure robustness  

5. **Results**  
   - Before resampling: high accuracy (>99%) but poor recall for failure events  
   - After SMOTE-ENN: recall significantly improved, especially for Random Forest and XGBoost  
   - After hyperparameter tuning:  
     - **Random Forest** → best trade-off between Precision & Recall  
     - **XGBoost** → robust performance across scenarios  
     - **Decision Tree** → interpretable but less effective  

6. **Feature Importance**  
   - Key predictive features: inverter and rotor temperatures, windspeed, rotation, and system cabinet temps  
   - Feature reduction from 32 → 24 most relevant features improved generalization  

---
