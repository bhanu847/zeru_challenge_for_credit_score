# zeru_challenge_for_credit_score

# DeFi Wallet Credit Scoring (Aave V2 Challenge)

## Overview
This project builds a **machine learning model** that assigns a **credit score (0–1000)** to each wallet interacting with the Aave V2 protocol, based solely on historical transaction behavior.

Higher scores indicate reliable & responsible usage, while lower scores indicate risky, bot-like, or exploitative behavior.

---

## Method Chosen

1. **Data Source**
   - JSON transaction-level data (`deposit`, `borrow`, `repay`, `liquidationcall`)
   - Each row = 1 transaction with `userWallet`, `action`, `amount`, `assetPriceUSD`

2. **Feature Engineering**
   - Aggregate wallet-level features:
     - `total_deposit_usd`
     - `total_borrow_usd`
     - `num_deposits`
     - `num_borrows`
     - `num_liquidations`
     - `num_repays`

3. **Synthetic Labels**
   - **Good wallet (1)**: Deposited more than borrowed & no liquidations
   - **Risky wallet (0)**: Borrowed more than deposited or had liquidations

4. **Machine Learning**
   - `RandomForestClassifier` trained to classify good vs risky wallets
   - Feature importance explains what behaviors matter most

5. **Credit Scoring**
   - Predict probability wallet is “good”
   - Scale probability → credit score (300–1000) using MinMaxScaler

---

## Processing Flow

Raw JSON Transactions
↓
Flatten with pandas.json_normalize
↓
Aggregate wallet-level behavior (pivot)
↓
Generate synthetic labels (good vs risky)
↓
Train RandomForest classifier
↓
Predict wallet probability of being good
↓
Scale 0–1 → credit score 300–1000
↓
Save JSON output: wallet_scores_ml.json


Architecture Diagram

          ┌──────────────────────────┐
          │ Raw Aave V2 Transactions │
          └────────────┬─────────────┘
                       ↓
         ┌──────────────────────────────┐
         │ pandas JSON normalize & pivot│
         └────────────┬─────────────────┘
                      ↓
     ┌─────────────────────────────────────────┐
     │ Synthetic labels (good vs risky wallets)│
     └─────────────────┬───────────────────────┘
                       ↓
      ┌────────────────────────────────────┐
      │ RandomForest Classifier (sklearn)  │
      └──────────────┬─────────────────────┘
                     ↓
       ┌──────────────────────────────────────────┐
       │ Probability wallet is good → Scale 300-1000│
       └──────────────────────┬───────────────────┘
                              ↓
                    wallet_scores_ml.json


Dependencies:-
Python 3.8+
pandas, numpy
scikit-learn
matplotlib

Install via:  pip install pandas numpy scikit-learn matplotlib
