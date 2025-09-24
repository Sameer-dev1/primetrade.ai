# Trader Performance vs. Market Sentiment Analysis

## Overview
This repository contains an analysis of trader performance (Closed PnL) against the Bitcoin Fear & Greed Index, using historical trading data from Hyperliquid (December 2024–April 2025) and sentiment data. The analysis focuses on closed positions with non-zero PnL, joined with sentiment data on matching dates.

## Files
- **DS_Task_primetrade.ai.ipynb**: Google Colab notebook with Python code, summary tables, and inline plots
- **fear_greed_index.csv**: Bitcoin Fear & Greed Index data (date, value, classification)
- **historical_data.csv**: Trading data (timestamps, accounts, coins, PnL, etc.)
- **summary_sentiment.csv**: Aggregated PnL metrics by sentiment classification
- **summary_account.csv**: Aggregated PnL metrics by account and sentiment
- **summary_coin.csv**: Aggregated PnL metrics by coin and sentiment
- **pnl_vs_sentiment_scatter.png**: Scatter plot of Closed PnL vs. Fear & Greed Index value
- **pnl_by_sentiment_boxplot.png**: Boxplot of Closed PnL distribution by sentiment classification

## Results

### Correlation
Correlation between Sentiment Value and Closed PnL: **0.01** (weak positive correlation, suggesting limited linear relationship between sentiment value and PnL).

### Summary by Sentiment Classification

| Classification | Total PnL | Average PnL | Number of Trades | Std Dev of PnL |
|----------------|-----------|-------------|------------------|---------------|
| Extreme Fear   | 739,110.25| 71.03       | 10,406           | 1,628.41      |
| Extreme Greed  | 2,715,171.31| 130.21    | 20,853           | 1,058.13      |
| Fear           | 3,357,155.44| 112.63    | 29,808           | 1,344.78      |
| Greed          | 2,150,129.27| 85.40     | 25,176           | 1,576.39      |
| Neutral        | 1,292,920.68| 71.20     | 18,159           | 743.21        |

**Key Observations:**
- **Extreme Greed**: Highest average PnL (130.21), but high trade volume suggests mixed outcomes
- **Fear**: Strong total PnL (3.36M), indicating potential for contrarian strategies
- **Extreme Fear**: Moderate gains, but fewer trades than Fear or Greed
- **Greed and Neutral**: Lower average PnL, with Greed showing higher volatility

### Summary by Account and Sentiment (Sample)

| Account | Classification | Total PnL | Average PnL | Number of Trades |
|---------|---------------|-----------|-------------|------------------|
| 0x083384f897ee0f19899168e3b1bec365f52a9012 | Extreme Fear | 124,769.22 | 3,372.14 | 37 |
| 0x083384f897ee0f19899168e3b1bec365f52a9012 | Extreme Greed | -40,282.34 | -163.75 | 246 |
| 0x083384f897ee0f19899168e3b1bec365f52a9012 | Fear | 1,113,373.55 | 1,059.35 | 1,051 |
| ... | ... | ... | ... | ... |
| 0xbee1707d6b44d4d52bfe19e41f8a828645437aab | Extreme Greed | 478,811.47 | 105.93 | 4,520 |

*Full table in summary_account.csv (150 rows).*

### Summary by Coin and Sentiment (Sample)

| Coin | Classification | Total PnL | Average PnL | Number of Trades |
|------|---------------|-----------|-------------|------------------|
| @1 | Extreme Greed | 495.67 | 33.04 | 15 |
| @1 | Greed | 1.08 | 0.36 | 3 |
| kPEPE | Greed | -6,949.14 | -19.85 | 350 |
| kSHIB | Extreme Greed | 264.97 | 15.59 | 17 |

*Full table in summary_coin.csv (599 rows).*

**Key Observation**: Stable assets (e.g., @1, @107) show gains in Extreme Greed; volatile coins (e.g., kPEPE, FARTCOIN) often lose in Greed.

### Hidden Patterns

- **Timing of Closes**: Profitable trades (e.g., @107 in Extreme Greed) were short-term, capturing upward momentum (values >76)
- **Loss Patterns**: FARTCOIN losses in Greed (values ~60-63) involved high initial positions, closed in batches, indicating over-holding
- **Sentiment Bias**: Trades concentrated in Greed/Extreme Greed, missing Fear opportunities (ideal for buying)
- **Coin Risk**: Volatile coins (e.g., FARTCOIN, kPEPE) had frequent small losses, suggesting over-trading
- **Position Sizing**: Larger positions amplified losses (e.g., -508 on 7,265 tokens)

## Insights and Recommendations

1. **Buy in Fear, Sell in Extreme Greed**: Profitable trades occurred during Extreme Greed (values >75). Strategy: Buy during Fear/Extreme Fear (<50) and sell at Extreme Greed peaks to lock gains
2. **Avoid Holding Through Sentiment Shifts**: Losses in Greed (60-75) suggest closing longs when sentiment drops below 70
3. **Risk Management for Volatile Coins**: FARTCOIN and kPEPE showed consistent losses in Greed. Use smaller position sizes and tight stops for volatile assets
4. **Diversify Timing and Assets**: Success in stable assets (@107) during Extreme Greed suggests quick scalps. Test contrarian buys in Fear (<30) for 20-30% returns per cycle
5. **Monitor Sentiment in Real-Time**: Integrate Fear/Greed Index with alerts, combining with technicals (e.g., RSI) to avoid overbought traps

## How to Run

1. Upload `fear_greed_index.csv` and `historical_data.csv` to Google Drive
2. Open `DS_Task_primetrade.ai.ipynb` in Google Colab
3. Install dependencies (run in a cell):
   ```python
   !pip install pandas numpy matplotlib seaborn
   ```
4. Run all cells to generate outputs and save files
