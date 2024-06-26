## Overview

This project implements an algorithmic trading bot that uses machine learning to automate trade decisions. It enhances existing trading signals with machine learning algorithms to adapt to new data and evolving markets.

## Baseline Performance

## SVC Model Performance

We used the SVC classifier model from SKLearn's support vector machine (SVM) learning method to establish a baseline performance. Here are the key findings:

- **Accuracy**: 0.55 (55%)
- **Precision**:
    
    - Class -1.0: 0.43
    - Class 1.0: 0.56
    - Weighted Avg: 0.50
    
- **Recall**:
    
    - Class -1.0: 0.04
    - Class 1.0: 0.96
    - Weighted Avg: 0.55
    
- **F1-Score**:
    
    - Class -1.0: 0.07
    - Class 1.0: 0.71
    - Weighted Avg: 0.43
    

The baseline trading algorithm performed moderately well, with an overall accuracy of 55%. The model shows a significant imbalance in its predictions:

1. It has high recall (0.96) for the positive class (1.0) but very low recall (0.04) for the negative class (-1.0).
2. Precision is better balanced between the two classes (0.43 for -1.0 and 0.56 for 1.0).
3. The F1-score, which balances precision and recall, is much higher for the positive class (0.71) compared to the negative class (0.07).

This suggests that the model is biased towards predicting the positive class, which could lead to many false positives in a trading context. While it correctly identifies most positive instances, it struggles to identify negative instances accurately.

## Tuning the Trading Algorithm

## Adjusting the Training Dataset Size

I experimented with different sizes of the training dataset by slicing the data into different periods. Here are the results:

- **Training Window 1**: 3 months
    
    - **Performance**: Moderate improvement in precision and recall.
    
- **Training Window 2**: 6 months
    
    - **Performance**: Slight improvement in accuracy but no significant change in F1-score.
    

Impact of increasing/decreasing the training window: Increasing the training window generally improved the model's performance slightly, but the gains were not substantial.

## Adjusting SMA Input Features

I adjusted the SMA input features by changing one or both of the SMA windows. Here are the results:

- **SMA Window 1**: 4 days (short), 100 days (long)
    
    - **Performance**: Baseline performance.
    
- **SMA Window 2**: 10 days (short), 50 days (long)
    
    - **Performance**: Improved precision and recall, slight increase in F1-score.
    

Impact of increasing/decreasing SMA windows: Adjusting the SMA windows to shorter periods improved the model's responsiveness to market changes, leading to better precision and recall.

## Optimized Parameters

Based on our experiments, the set of parameters that best improved the trading algorithm returns are:

- **Short SMA Window**: 10 days
- **Long SMA Window**: 50 days
- **Training Window**: 6 months

Optimized Algorithm Performance: The optimized algorithm showed a noticeable improvement in precision and recall, leading to better overall performance compared to the baseline model.

## New Model Performance (Random Forest Classifier)

Here are the key findings:

- **Accuracy**: 0.51 (51%)
- **Precision**:
    
    - Class -1.0: 0.44
    - Class 1.0: 0.56
    - Weighted Avg: 0.50
    
- **Recall**:
    
    - Class -1.0: 0.35
    - Class 1.0: 0.64
    - Weighted Avg: 0.51
    
- **F1-Score**:
    
    - Class -1.0: 0.39
    - Class 1.0: 0.60
    - Weighted Avg: 0.51
    

The Random Forest Classifier shows a slight improvement over the baseline SVC model, with an overall accuracy of 51%. Here's a breakdown of its performance:

1. The model shows better balance in its predictions compared to the SVC model, with improved recall for the negative class (-1.0) and slightly reduced recall for the positive class (1.0).
2. Precision is similar to the SVC model, with a slight improvement for the negative class and a minor decrease for the positive class.
3. The F1-score shows improvement for the negative class (0.39 vs 0.07) and a slight decrease for the positive class (0.60 vs 0.71).
4. The overall weighted average F1-score (0.51) is higher than that of the SVC model (0.43), indicating better overall performance.

## Evaluation Report

## Final Conclusions and Analysis

1. **Baseline SVC Model**: The SVC model showed moderate performance with 55% accuracy but had a significant bias towards the positive class, potentially leading to many false positives.
2. **Random Forest Classifier**: This model demonstrated more balanced performance across both classes, addressing some of the bias issues seen in the SVC model. While the overall accuracy is slightly lower (51% vs 55%), the more balanced predictions suggest that this model may be more reliable across different market conditions.
3. **Performance Comparison**: The Random Forest model shows improved performance in terms of balanced predictions and a higher overall F1-score, suggesting it may be better suited for capturing both upward and downward market movements.
4. **Strategy Returns**: Based on the cumulative returns plot, both models' strategy returns generally outperform the actual returns, especially in the latter part of the testing period. This indicates that both models have captured useful patterns in the data that translate to potentially profitable trading decisions.
5. **Recommendation**: While both models show promise, the Random Forest Classifier appears to be more robust due to its balanced performance across classes. It may be the preferred choice for a more stable trading strategy.

![](actual_vs_strategy_returns.png) The cumulative returns plot shows that the strategy returns generally outperformed the actual returns, indicating the effectiveness of the trading algorithm. Further tuning and model experimentation could lead to even better performance.
