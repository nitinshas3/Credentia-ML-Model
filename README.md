🎓 AI-Powered Student Loan Recommendation Engine (Model Training)
This repository contains the complete workflow for training an XGBoost-based machine learning model to recommend the best education loan products for students. The model predicts approval probability for a student's profile across multiple bank loan products, ranking them for suitability.

🚀 Features
Predicts loan approval probability for students from 40+ Indian loan products.

Student-specific inputs: CGPA, university tier, income, loan amount, collateral, repayment period, etc.

Handles bank-specific rules: max loan amount, collateral conditions, tier restrictions.

Ranks loan products by approval probability and returns Top 3 recommendations for any student.

Hybrid dataset built from real Kaggle data plus synthetic features adapted for Indian education loans.

Exportable trained XGBoost model (loan_model.pkl) for use in backends or apps.

📊 1. Data Collection
🔹 Loan Products Dataset
Curated ~40 education loan products from Indian banks.
Columns include:

Bank name/product name

Interest rate

Max loan (domestic/abroad)

Repayment period

Processing fee

Collateral required

Eligibility (e.g., Tier-1 colleges only)

🔹 Student Dataset
Base: Kaggle Loan Data (originally US-based)
Columns from Kaggle:

credit_score

person_income

loan_amnt

previous_loan_defaults_on_file
Adaptations made:

Converted ranges to Indian context (income, loan amount, credit score)

Removed US-specific columns

Synthetic features added:

university_tier (Tier 1/2/3, correlated with credit score)

cgpa (linked to tier for realism)

collateral_available (binary, linked with income)

repayment_period (randomized 5–15 years)

👉 Final dataset
Kaggle base (adapted for India) + Synthetic student features, paired with each loan product.

⚙️ 2. Data Preparation
Merged student dataset with loan product dataset, pairing each student with every loan.

Hard rules for approval probability:

Requested loan > bank's max = probability 0

Collateral required but not available = 0

Tier not eligible = 0

Soft scoring:

Higher CGPA/tier, higher probability

Smaller gap between requested and max loan, higher probability

Higher credit score, higher probability

🤖 3. Model Training
Target: Approval Probability (between 0 and 1)

Features:

Student: cgpa, university_tier, person_income, loan_amnt, credit_score, previous_loan_defaults_on_file, collateral_available, repayment_period

Loan: Bank_Name, Product_Name, Interest_Rate, Max_Loan_Domestic, Repayment_Period, etc.

Preprocessing: One-Hot Encoding for categorical columns (Bank_Name, Product_Name, university_tier).

Model: XGBoost Regressor with tuned hyperparameters.

Output: Trained model saved as loan_model.pkl and ready for deployment.

📦 Usage
Clone the repo and run the notebook to train or update the model (train_model.ipynb or similar).

Use the exported model in APIs or integrate with app backends for loan recommendations.

Easily experiment with new features, data or rules by editing the preprocessing steps.

