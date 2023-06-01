# algorithmic-trading-homework
Module 14 Challenge: Machine Learning Trading Bot

## Establish a Baseline Performance
The SVC model, providing our baseline performance, results in the following metrics:

| ---------- | Accuracy | Long precision | Long recall | Short precision | Short recall |
|:---------- |:--------:|:--------------:|:-----------:|:---------------:|:------------:|
| **Result** | 0.55     | 0.56           | 0.96        | 0.43            | 0.04         |

![Actual Returns vs. Strategy Returns - Baseline](Resources/actual_vs_strategy_returns_baseline.png)

With regard to cumulative products, in 2015, strategy returns exceeded actual returns. In early 2016, strategy returns deviated from actual returns, underperforming until 2018. From 2018 until mid-2020, strategy returns matched actual returns, but then deviated again. Overall, strategy returns have greatly underperformed compared to actual returns.

## Tune the Baseline Trading Algorithm

### Question: What impact resulted from increasing or decreasing the training window?
![Metrics Comparison for Various Training Periods](Resources/metrics_comparison_training.png)

**Answer:**

With regard to the average difference between the cumulative product of strategy returns and the cumulative product of actual returns (CumProd Diff), decreasing the training window to as little as one week showed minor improvement over the baseline 3-month training window. While increasing the training window initially increased the difference, continuing to increase the training window from 9 months to 33 months showed steady reduction in the difference. After 33 months, further increasing of the training window showed a plateau, followed by another increase, in the difference.

Concerning the classification reports generated for the machine-learning models, accuracy and long precision remained rather constant across all training windows. While long recall and short recall also remained rather constant across all training windows&mdash;with the exception of a dip/spike over 8- and 9-month training windows&mdash;they were in opposition to each other. The only metric that showed any real fluctuation was that of short precision. For training windows under 11 months in length, short precision remained rather steady around 0.40. For training windows of 11 months and beyond, the precision flat-lined at 0, with the exception of a spike between 18 and 24 months.

![Actual Returns vs. Strategy Returns - 24-Month Training](Resources/actual_vs_strategy_returns_24M.png)

Given the above analysis, a 24-month training window seems optimal. While the optimal difference in cumulative products was found at the 33-month training window, the model had predicted no short signals (`-1`), thereby forcing a short precision and short recall of 0.00. Providing our original SVC model with a 24-month training window results in the following metrics:
- Accuracy: **0.55**
- Long precision: **0.56**
- Long recall: **1.00**
- Short precision: **0.80**
- Short recall: **0.00**

### Question: What impact resulted from increasing or decreasing either or both of the SMA windows?
![Metrics Comparison for Various SMA Combinations](Resources/metrics_comparison_sma.png)

**Answer:**

With regard to the average difference between the culumative product of strategy returns and the cumulative product of actual returns, neither increasing nor decreasing the short-window (fast) SMA, relative to the long-window (slow) SMA, had any effect on the cumulative product of strategy returns over the baseline 4-100 (fast-slow) SMA combination. Decreasing the slow SMA made for minor improvement in the difference. While increasing the slow SMA initially increased the difference, continuing to increase the slow SMA beyond 400 showed steady reduction of the difference.

Concerning the classification reports generated for the machine-learning models, accuracy and long precision remained rather constant across all SMA combinations, with the exception of a few dips in accuracy that aligned with dips in long recall. Long recall remained fairly steady above 0.080, though did witness a few extreme dips below 0.10. Short recall was always in opposition to long recall, spiking whenever long recall dipped. Short precision is the only metric that seemed to fluctuate independently. 

![Actual Returns vs. Strategy Returns - SMA 48-730](Resources/actual_vs_strategy_returns_sma_16-140.png)

Given the above analysis, a fast-slow SMA combination of 16-140 seems optimal. Providing our original SVC model with 48-600 SMA combination results in the following metrics:
- Accuracy: **0.56**
- Long precision: **0.56**
- Long recall: **0.99**
- Short precision: **0.52**
- Short recall: **0.01**

### Conclusion
![Actual Returns vs. Strategy Returns - Tuned](Resources/actual_vs_strategy_returns_tuned.png)

Using a training period of 24 months and SMA windows of 16 (fast) and 140 (slow), the cumulative product of strategy returns closely matches the cumulative product of actual returns, over-performing the latter for much of the testing period and only deviating for the last few months.

The classification report for the model provides the following metrics:
- Accuracy: **0.56**
- Long precision: **0.56**
- Long recall: **1.00**
- Short precision: **1.00**
- Short recall: **0.00**

## Evaluate a New Machine Learning Classifier

### Conclusion
![Actual Returns vs. Strategy Returns - AdaBoost Classifier](Resources/actual_vs_strategy_returns_adaboostclassifier.png)

The new machine-learning classifier utilized was an AdaBoost classifier. The classification report for the model provides the following metrics:
- Accuracy: **0.55**
- Long precision: **0.56**
- Long recall: **0.92**
- Short precision: **0.44**
- Short recall: **0.08**

### Question: Did this new model perform better or worse than the provided baseline model?
**Answer:**

The new model performed nearly identically to the provided baseline model. There were no changes in accuracy, long precision or cumulative product of strategy returns. Short precision increased by 0.01 and short recall increased by 0.04, but long recall decreased by 0.04.

### Question: Did this new model perform better or worse than your tuned trading algorithm?
**Answer:**
Overall, the new model did not perform quite as well as the tuned trading algorithm. 

## Summary Evaluation Report
![Actual Returns vs. Strategy Returns - Baseline](Resources/actual_vs_strategy_returns_baseline.png)
![Actual Returns vs. Strategy Returns - Tuned](Resources/actual_vs_strategy_returns_tuned.png)
![Actual Returns vs. Strategy Returns - AdaBoost Classifier](Resources/actual_vs_strategy_returns_adaboostclassifier.png)

| Metric              | Baseline model | Tuned model | AdaBoost model |
|:---                 | ---            | ---         | ---            |
| **Accuracy**        | 0.55           | 0.56        | 0.55           |
| **Long precision**  | 0.56           | 0.56        | 0.56           |
| **Long recall**     | 0.96           | 1.00        | 0.92           |
| **Short precision** | 0.43           | 1.00        | 0.44           |
| **Short recall**    | 0.04           | 0.00        | 0.08           |

