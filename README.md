🎓 AI-Powered Student Loan Recommendation Engine

This project is an AI-based loan recommendation system designed to help students find the most suitable education loan products. The model takes student-specific details as input and outputs the approval probability for different bank loan products, ranking them from best to least suitable.

🚀 Features

✅ Predicts loan approval probability for students across 40 loan products.

✅ Supports student-specific inputs: CGPA, university tier, income, loan amount, collateral, etc.

✅ Handles bank-specific constraints: max loan amount, collateral rules, Tier-1 college restrictions.

✅ Ranks loan products by approval probability and returns Top 3 recommendations.

✅ Designed with a hybrid dataset (real Kaggle data + synthetic student features).

✅ Exportable trained ML model (.pkl file) for deployment in APIs or apps.

📊 1. Data Collection
🔹 Loan Products Dataset

Collected and curated ~40 education loan products from Indian banks.

Columns included:

Bank name & product name

Interest rate

Max loan (Domestic & Abroad)

Repayment period

Processing fee

Collateral required

Eligibility (e.g., Tier-1 colleges only)

🔹 Student Dataset

Base dataset: Taken from Kaggle Loan Data
 (originally US-based).

Columns available from Kaggle:

credit_score

person_income

loan_amnt

previous_loan_defaults_on_file

Adaptations made:

Converted values to Indian ranges (income, loan amount, credit score).

Removed US-specific attributes (like home_ownership).

Synthetic features added:

university_tier → (Tier 1 / Tier 2 / Tier 3, partially correlated with credit score & income).

cgpa → generated with correlation to tier, with randomness.

collateral_available → binary, linked with income level.

repayment_period → randomized between 5–15 years.

👉 Final dataset = Kaggle base (adapted to India) + Synthetic Student Features

⚙️ 2. Data Preparation

Merged student dataset with loan product dataset so each student is paired with every loan.

Applied hard rules for approval probability:

If requested loan > max bank limit → probability = 0.

If collateral required but not available → probability = 0.

If tier not eligible for product → probability = 0.

Applied soft scoring:

Higher CGPA & tier → higher probability.

Lower difference between requested and max loan → higher probability.

Higher credit score → higher probability.

🤖 3. Model Training

Target variable: Approval Probability (0–1).

Features used:

Student features: cgpa, university_tier, person_income, loan_amnt, credit_score, previous_loan_defaults_on_file, collateral_available, repayment_period.

Loan features: Bank_Name, Product_Name, Interest_Rate, Max_Loan_Domestic, Repayment_Period, etc.

Preprocessing:

Applied One-Hot Encoding to categorical columns (Bank_Name, Product_Name).

Model:

Random Forest Regressor (sklearn) with tuned hyperparameters.

Output:

Trained model saved as loan_model.pkl.