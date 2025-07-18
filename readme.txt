 Aave V2 Wallet Credit Scoring using ML

This project analyzes historical transaction-level data from the Aave V2 protocol and generates a **credit score (0–1000)** for each wallet based solely on its behavior. The score is designed to reflect user reliability, responsible DeFi usage, and potential risk behavior.

---

Data

The input data is a JSON file containing DeFi transactions from 100K wallets. Each entry records actions such as:

- `deposit`
- `borrow`
- `repay`
- `redeemunderlying`
- `liquidationcall`

---

Features Engineered

We derived the following features per wallet:

- Count of each action type
- Sum of token amounts per action
- Total number of transactions
- Ratios like `borrow_amount / deposit_amount`
- Presence of liquidations
- Clustering category via KMeans

---

 Architecture

1. **Data Flattening:** Normalize nested JSON data using `pandas.json_normalize`.
2. **Feature Engineering:** Compute per-wallet behavioral metrics (frequency and volume).
3. **Clustering:** Apply KMeans to group wallets by similar usage patterns.
4. **Scoring Logic:**
   - Start with a **rule-based base score**
   - Penalize for risky behavior (e.g., liquidations)
   - Reward healthy repayments and deposits
5. **Machine Learning:**
   - Train a `RandomForestRegressor` on the engineered features using the base score as target.
   - Predict and refine credit scores (0–1000) using model outputs.

---

Output

- `wallet_scores_ml.csv`: Contains wallet addresses, cluster assignment, and final credit scores.
- `score_distribution_ml.png`: Histogram showing the distribution of generated scores.



Running the Code

1. Upload the JSON data into the Colab environment.
2. Run the Python script to process and score the wallets.
3. Results will be saved as `.csv` and `.png` files.


Requirements

- Python 3.x
- pandas, numpy, scikit-learn, matplotlib

Install via:

```bash
pip install pandas numpy scikit-learn matplotlib
