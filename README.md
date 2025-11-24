# 📉 Bitcoin Sentiment vs. Trader Performance Analysis

This project performs a quantitative analysis of a high-frequency trading account on Hyperliquid to determine if **Bitcoin Market Sentiment** (specifically the *Fear & Greed Index*) acts as a leading indicator for profitability.

The analysis specifically tests the hypothesis: **"Does this trader perform better when the market is fearful or greedy?"**

## 📊 Key Findings

Based on the analysis of historical trade data and sentiment scores:

1.  **The Contrarian Edge:** The trader performs significantly better during periods of **Market Fear**. A statistical T-test confirmed the difference in PnL between Fear and Greed days is statistically significant ($p < 0.0001$).
2.  **Asset Correlation:** This sentiment-based edge is driven almost entirely by **Bitcoin (BTC)** trades (Correlation: -0.15). **Altcoin** performance shows almost zero correlation with macro market sentiment.
3.  **The "Mania" Paradox:** While "Greed" is generally less profitable, the specific bucket of **"Extreme Greed"** showed the highest *average* returns. However, further analysis revealed this was driven by massive outliers (high variance), suggesting a high-risk "lottery ticket" dynamic during market mania, whereas "Extreme Fear" offered consistent, reliable returns.

---

## 🖼️ Visualizations

### 1. Bitcoin vs. Altcoins: The Sentiment Disconnect
We separated trades into BTC-only and Altcoins. The regression below shows a clear negative slope for BTC (Contrarian: Profits rise as Sentiment falls), while Altcoins remain flat (Uncorrelated).

<img width="1035" height="468" alt="image" src="https://github.com/user-attachments/assets/89f2ef4c-3e99-4fb8-b67a-dd1d7731fbc4" />

### 2. Fear vs. Greed Performance
Aggregating PnL during "Fear" days (< 45 score) vs "Greed" days (> 55 score). The disparity suggests the strategy thrives on volatility and panic dumps.

<img width="549" height="449" alt="image" src="https://github.com/user-attachments/assets/d1631ae1-2975-4e1d-a98d-0b7f748f6d22" />

### 3. Distribution of Returns by Sentiment Zone
Using a logarithmic scale boxplot to visualize the spread of returns. Note the massive outliers in "Extreme Greed" vs the tight consistency in "Fear".

<img width="861" height="468" alt="image" src="https://github.com/user-attachments/assets/07153027-abdd-4cae-9808-79e87c5b43c8" />

---

## 🛠️ Methodology

### Data Sources
1.  **Hyperliquid Trade Logs:** `historical_data.csv` (Contains execution price, size, side, PnL, timestamps).
2.  **Alternative.me API:** `fear_greed_index.csv` (Daily sentiment classification).

### Data Processing Steps
1.  **Cleaning:** Standardized timestamps to UTC, cleaned ticker symbols using Regex (e.g., `@107` $\to$ `TOKEN_107`), and handled missing sentiment values via forward-filling.
2.  **Aggregation:** Grouped high-frequency trades into Daily aggregates (Total PnL, Win Rate, Trade Count).
3.  **Statistical Testing:**
    * **Pearson/Spearman Correlation:** To measure linear and rank relationships.
    * **Lag Analysis:** To check if sentiment *yesterday* predicts PnL *today*.
    * **T-Test:** `scipy.stats.ttest_ind` used to validate the hypothesis that Fear PnL $\neq$ Greed PnL.

---

## 🚀 Installation & Usage

### Prerequisites
* Python 3.8+
* Jupyter Notebook

### Setup
1.  Clone the repository:
    ```bash
    git clone [https://github.com/yourusername/bitcoin-sentiment-analysis.git](https://github.com/yourusername/bitcoin-sentiment-analysis.git)
    ```
2.  Install dependencies:
    ```bash
    pip install pandas numpy matplotlib seaborn scipy
    ```
3.  Run the analysis:
    ```bash
    jupyter notebook Assignment.ipynb
    ```

---

## 📂 File Structure

```text
├── Assignment.ipynb       # Main analysis notebook
├── fear_greed_index.csv   # Sentiment dataset
├── historical_data.csv    # Trading data (Not included in repo for privacy)
├── images/                # Generated plots for README
│   ├── btc_vs_alt_corr.png
│   ├── fear_vs_greed_bar.png
│   └── sentiment_buckets.png
└── README.md              # Project documentation
