# algorithmic-trading-homework
Module 14 Challenge: Machine Learning Trading Bot

## Establish a Baseline Performance
The SVC model, providing our baseline performance, results in the following metrics:
- Accuracy: **0.55**
- Long precision: **0.56**
- Long recall: **0.96**
- Short precision: **0.43**
- Short recall: **0.04**

![Actual Returns vs. Strategy Returns](Resources/actual_vs_strategy_returns.png)

With regard to cumulative products, in 2015, strategy returns exceeded actual returns. In early 2016, strategy returns deviated from actual returns, underperforming until 2018. From 2018 until mid-2020, strategy returns matched actual returns, but then deviated again. Overall, strategy returns have greatly underperformed compared to actual returns.

## Tune the Baseline Trading Algorithm

### Question: What impact resulted from increasing or decreasing the training window?
![Difference Between Average Cumulative Products of Actual Returns and Strategy Returns From 2019–04 Through 2021–01 for Various Training Models](Resources/avg_cumprod_diff_training.png)

![Actual Returns vs. Strategy Returns - 33-Month Training](Resources/actual_vs_strategy_returns_33M.png)

**Answer:** Decreasing the training window to as little as one week showed minor improvement in the cumulative product of strategy returns over the baseline 3-month training window. While increasing the training window initially decreased the cumulative product, continuing to increase the training window from 9 months to 33 months showed steady improvement in the cumulative product. After 33 months, further increasing of the training window showed a plateau, followed by a decline, in the cumulative product of strategy returns as compared to the cumulative product of actual returns.

### Question: What impact resulted from increasing or decreasing either or both of the SMA windows?
![Difference Between Average Cumulative Products of Actual Returns and Strategy Returns From 2019–04 Through 2021–01 for Various SMA Combinations](Resources/avg_cumprod_diff_sma.png)

![Actual Returns vs. Strategy Returns - SMA 48-730](Resources/actual_vs_strategy_returns_sma_48-730.png)

**Answer:** Neither increasing nor decreasing the short-window (fast) SMA, relative to the long-window (slow) SMA, had any effect on the cumulative product of strategy returns over the baseline 4-100 (fast-slow) SMA combination. Decreasing the slow SMA showed minor improvement in the cumulative product of strategy returns. While increasing the slow SMA initially decreased the cumulative product, continuing to increase the slow SMA beyond 400 showed steady improvement in the cumulative product.

### Conclusion
![Actual Returns vs. Strategy Returns - Optimized](Resources/actual_vs_strategy_returns_optimized.png)

Using a training period of 33 months and SMA windows of 48 (fast) and 730 (slow), the cumulative product of strategy returns closely matches the cumulative product of actual returns, over-performing the latter for much of the testing period and only deviating for the last few months.