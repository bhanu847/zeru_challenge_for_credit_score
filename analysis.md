# Wallet Scoring Analysis

## Score Distribution

![Score Distribution](score_distribution.png)

| Score Range | Wallet Count |
|-------------|-------------:|
| 0-100       | 15           |
| 100-200     | 42           |
| 200-300     | 76           |
| ...         | ...          |
| 900-1000    | 120          |

---

## Observations

- **Low-score wallets (0–300):**
  - Usually have high borrows compared to deposits
  - Many had liquidation events
  - Rarely repay debts

- **Mid-range wallets (400–700):**
  - Mix of moderate deposits and borrows
  - Some repays, but still occasional risk patterns

- **High-score wallets (800–1000):**
  - Mostly deposit-only wallets, never liquidated
  - Frequently repay borrowed funds
  - Consistent healthy usage over time

---

## Behavior Insights

- Liquidation is the **strongest negative signal**
- Repay actions help improve score
- Large deposits relative to borrows strongly correlate with higher scores
