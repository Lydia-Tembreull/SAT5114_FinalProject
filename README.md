# Predicting Sleep Apnea Severity (OSA) Based on Physiological and Demographic Data

## 🔗 Quick Links
- **Video Presentation**: [YouTube Link Here](https://youtu.be/sFZuKeZ7rqk)
- **Presentation Slides**: [Cick Here to View Slides](file:///C:/Users/swiml/SAT5114_FinalProject/Lydia_Tembreull_Sleep_Apnea.pdf)

## Project Overview
Obstructive Sleep Apnea (OSA) is an increasing prevalent disease linked with cardiovascular disease and metabolic syndrome that is grossly under-diagnosed. Polysomnography (PSG), the current gold-standard for diagnosis, is costly and labor intensive.

Here, the potential for Automated Clinical Decision Support is shown using demographic and physiological data to predict disease severity. The models are trained and tested using the publicly available Sleep Heart Health Study (SHHS) dataset to predict one of four clinically defined levels of OSA severity using the Apnea-Hypopnea Index (AHI).

#### Goals:
- Achieve a multi-class classification accuracy of at least 75%.
- Achieve an AUC of at least 0.80 for predicting "Severe" sleep apnea.
- Identify the most significant physiological predictors using Explainable AI (SHAP).

## Dataset & Features
The study utilizes Visit 1 data from the SHHS, obtained through the **National Sleep Research Resources (NSSR)**.
- **Sample Size**: 5,804 patients.
- **Target Variable (Response)**: RDI Severity Category: The model predicts the severity of sleep apnea based on the Respiratory Disturbance Index at 3% oxygen desaturation (`rdi3p`). This is binned into four clinical classes:
    - **None** (AHI < 5).
    - **Mild** (5 $\leq$ AHI < 15).
    - **Moderate** (15 $\leq$ AHI < 30).
    - **Severe** (AHI $\geq$ 30).
- **Input Features (Predictors)**:
    - **Demographics**: Age (`age_s1`), Gender (`gender`), Race (`race`).
    - **Physical Metrics**: BMI (`bmi_s1`), Neck Circumference (`neck20`).
    - **Physiological Signals**: REM Oxygen Saturation (`mnsao2rh`), Average Heart Rate (`avhrbp`), Systolic Blood Pressure (`systbp`).
    - **Patient Experience**: Epworth Sleepiness Scale (`ess_s1`), Smoking Status (`smokstat_s1`).

## Methodology
1. **Preprocessing**: Applied median/mode imputation on missing data for continuous variables .
2. **Encoding & Scaling**: One-Hot encoded categorical variables (i.e., gender_Male, race_White) and used StandardScaler on continuous features.
3. **Feature Engineering**: Introduced an interaction term between BMI and Age.
4. **Model Comparison**: Compared Logistic Regression (baseline model), Random Forest, XGBoost, and SVM.
5. **Validation**: 70/15/15 Train-Validation-Test split with 5-fold cross-validation.
6. **Explainability**: Incorporated SHAP (SHapley Additive exPlanations) values for clinical explainability.

## Performance Results
The final model (Logistic Regression with tuned hyperparameters) achieved the following performance:
- **Severe Class AUC**: 0.88 (exceeds the target goal of 0.80).
- **Overall Accuracy**: 53.6% across all four classes (below the target goal of 75%).
- **Key Insight**: Male gender, advanced age, neck circumference, and BMI were identified as the primary positive drivers for Severe Obstructive Sleep Apnea classification. Mean oxygen saturation (`mnsao2rh`) acted as the most significant negative predictor.

## Project Structure
- `SleepApnea.ipynb`: Full ML pipeline including EDA, preprocessing, model tuning, and SHAP analysis.
- `shhs1-dataset-0.21.0.csv`: Source data (requires access via NSSR).
- `sshs-data-dictionary-0.21.0-variables.csv`: Supporting file that helps with variable decoding and categorical mapping.
- `sshs-data-dictionary-0.21.0-forms.csv`: Supporting file that acts as a map for various data collection forms used in the study.
- `shhs-data-dictionary-0.21.0-domains.csv`: Supporting file that helps in understanding the enumerated values (domains) that variables are allowed to take.

## How to Run
1. Clone the repository.
2. Install dependencies: `pip install pandas numpy scikit-learn xgboost shap seaborn`.
3. Open `SleepApnea.ipynb` in Jupyter Notebook or Google Colab.

## References

#### Clinical & Data Foundations:
- **Punjabi, N. M. (2008).** The epidemiology of adult obstructive sleep apnea. *Proceedings of the American Thoracic Society.*
- **Quan, S. F., et al. (1997).** The sleep heart healthy study: Design, rationale, and methods. *Sleep.*
- **National Sleep Research Resources (2026).** *Sleep Heart Health Study (SHHS) Visit 1 Dataset.* [https://sleepdata.org/datasets/shhs].

#### Machine Learning in Sleep Medicine:
- **Goldstein, C. A., et al. (2020).** Artificial Intelligence in sleep medicine: Background and implications for clinicians. *Journal of Clinical Sleep Medicine.*
- **Lundberg, S. M., & Lee, S.-I. (2017).** A unified approach to interpreting model predictions. *31st Conference on Neural Information Processing Systems (NIPS).*
- **Li, S., et al. (2025).** Advances in Machine Learning Prediction Models for the Screening of Obstructive Sleep Apnea in Adults. *Nature and Science of Sleep.*
- **Maniaci, A., et al. (2023).** Machine Learning Identification of Obstructive Sleep Apnea Severity through the Patient Clinical Features. *MDPI.*
- **Shi, Y., et al. (2023).** Application and interpretation of machine learning models in predicting the risk of severe obstructive sleep apnea in adults. *BMC Medical Information and Decision Making.*
