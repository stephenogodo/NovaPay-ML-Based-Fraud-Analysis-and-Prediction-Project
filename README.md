# NovaPay ML-Project-on-Fraud-Detection-Analysis-and-Modelling
## INTRODUCTION:
NovaPay is a digital-first cross-border money transfer company based in Toronto, Canada. Operating in the United Kingdom,
Canada and the United States, NovaPay empowers users to seamlessly send, receive, and hold multiple currencies across international borders.

## Key Pain Points:
1. Identity theft, account takeover, transaction laundering, and unauthorized payments

2. Highly imbalanced dataset (fraud represents less than 1% of all transactions)

3. Insufficient adaptive detection tools in the current workflow

4. False positives that frustrate legitimate users

5. Regulatory pressure for transparency and explainable fraud decisions

These issues collectively justify the need for a machine learning–driven solution.

## AIM:
This project aims to use historical transaction and customer data to train a machine learning model that predicts fraudulent transactions. 
The model will analyse transaction data such as amounts, currency pairs, timestamps, channel indicators (mobile/web/ATM), device fingerprints, 
IP addresses, and geographic country codes, along with customer profile information, including account age, KYC verification tier, typical 
transaction amounts, and historical behavior patterns.

## OBJECTIVES:
1. To develop a solution that can provide real-time fraud scores to transaction processors, allowing NovaPay to block fraudulent transactions accurately. 
2. To reduce false positives/false alarms that frustrate legitimate users, and
3. To maintain a stronger platform security.

## METHODOLOGY:
1. I carried out thorough data cleaning and standardization.
2.  I completed the comprehensive analysis covering:
    *data preprocessing, 
    *exploratory data analysis, EDA,
3. Feature engineering, 
4. Model training 
5. Evaluation,
6. Hyperparameter tuning,
7.  and model interpretability using SHAP.

## STEPS AND KEY FINDINGS:
Data Preprocessing and Cleaning: I started by meticulously inspecting the dataset for inconsistencies, missing values, and duplicates. 
We successfully handled missing data by dropping rows where appropriate and cleaned categorical features by standardizing their values 
and handling 'unknown' entries. This ensured the dataset was robust and ready for analysis.

Exploratory Data Analysis (EDA): The EDA unveiled critical patterns and potential indicators of fraud. I analyzed the distribution of 
the target variable (is_fraud), revealing a class imbalance that is typical in fraud datasets. I investigated numerical features like 
amount_usd, fee, and risk scores, observing their distributions for both fraudulent and non-fraudulent transactions. Categorical features 
such as home_country, channel, kyc_tier, and ip_country were analyzed for their frequency and relationship with fraud rates. Notably, I 
found that countries with lower transaction volumes could sometimes exhibit higher fraud rates, and specific channels (e.g., 'web') or 
KYC tiers ('low') were associated with elevated fraud risks. The time-based analysis identified trends in transaction volumes and fraud 
rates across different hours of the day and different days of the week.

Feature Engineering: Based on the insights from EDA, I engineered several new features designed to capture fraud signals more effectively. 
These included night_hour, account_very_new, account_new, velocity_burst, amount_high, ip_high_risk, and device_low_trust. These features 
proved to be strong predictive signals, particularly account_very_new and velocity_burst, which highlighted the increased risk associated 
with new accounts and rapid transaction sequences.

Model Training and Evaluation: I trained a suite of machine learning models, including Logistic Regression, Random Forest, XGBoost, and LightGBM. 
The Random Forest Classifier emerged as the top performer, achieving an impressive accuracy of 99% with a precision of 100% for fraudulent 
transactions and a recall of 92%. This indicates the model's exceptional ability to correctly identify all instances it flags as fraud, and to 
catch a very high percentage of actual fraudulent transactions.

Hyperparameter Tuning: I further optimized the Random Forest model using RandomizedSearchCV. While the tuning process confirmed the model's robustness, 
It showed that the initial performance was already near optimal, with no significant gains in the F1-score.

Model Interpretability with SHAP: To understand why our model makes certain predictions, I employed SHAP values. The SHAP summary and bar plots clearly 
identified the most influential features. The top contributors to fraud detection were confirmed to be txn_velocity_1h, velocity_burst, ip_risk_score, 
risk_score_internal, account_age_days (and its engineered variants like account_very_new), and device_trust_score (and device_low_trust). I also used SHAP 
to explain a random fraudulent transaction, illustrating how specific feature values contributed to the model's final prediction.

This comprehensive project has not only delivered a highly performant fraud detection model but also provided deep, interpretable insights into the underlying 
drivers of fraudulent activities. These insights can be invaluable for developing targeted fraud prevention strategies and improving overall financial security.



=======FIND BELOW A CONCISE SUMMARY OF THE DELIVERABLES OF THE NOVAPAY FRAUD DETECTION PROJECT===========
                                   FINAL SUMMARY REPORT


DATASET OVERVIEW
  Total Transaction: 10,816
  Fraud Cases: 986 (9.12%)
  Train Set:8,652 rows (684 fraud cases)
  Test Set: 2,164 rows (382 fraud cases)
  Feature Engineered: 27
  
MODEL PERFORMANCE  (Test Set)            
Logistic Regression
Precision = 79%; Recall = 94%; F1-score = 0.86; ROC-AUC = 0.97

Random Forest
Precision = 100% ; Recall = 92%; F1-score = 0.96; ROC-AUC =  0.99

XGBoost 
Precision = 93% ; Recall = 92%;  F1-score =  0.93;    ROC-AUC =  0.97


BEST MODEL: Random Forest
100% Precision (no false positives)
92% Recall (less false negatives), i.e., only 8% escaped being detected
Zero legitimate transactions blocked


TOP 5 FRAUD INDICATORS (SHAP Analysis)
1. txn_velocity_1h
2. velocity_burst
3. ip_risk_score
4. txn_velocity_24h
5. risk_score_internal


KEY BUSINESS INSIGHTS
1. New accounts(<90 days) have a 3 - 46% fraud rate vs 1-2% for more mature accounts
2. Transactions with txn velocity2.3/hour show 70 - 80% fraud rate
3. Transactions involving high amount(2k-$5k) have 75 - 95% fraud rate
5. Low device trust (<0.5) indicates 84% fraud probability
6. Night hour (0 - 5 AM) shows 1.92x higher fraud rate


DELIVERABLE COMPLETED
1. Data cleaning & quality assessment
2. Feature engineering (8 new features created)
3. 4 ML models trained and evaluated
5. Model saved for deployment (fraud_model_rf.pkl)



PROJECT OUTCOME

1. Achieved 100% precision (No customer frictions resulting from false blocks)
2. Identified clear fraud patterns for business rules
3. Demonstrated 8.42x lift with velocity-based features
4. Ready for production deployment


                                PROJECT SUCCESSFULLY COMPLETED
