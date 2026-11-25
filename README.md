# Loan Default Prediction: Model Evaluation and Risk Analysis

## Objective

In this lab, I wanted to see how well different machine learning models could predict loan defaults and whether they would actually save a lender money.

## Methodology

- Simulated 6,000 loan applications with around 7% default prevalence.
- Used income, debt-to-income ratio, credit history, prior delinquencies, loan amount, and three random noise features.
- Compared a majority-class baseline, logistic regression, LASSO, Ridge, and random forest.
- Used cross-validation to tune LASSO and Ridge.
- Evaluated accuracy, precision, recall, F1, ROC AUC, and PR AUC.
- Compared MDI and permutation feature importance.
- Used McNemar's test to compare model accuracy.
- Built an expected-cost curve to find the best decision threshold.
- Tested probability calibration using Platt scaling and isotonic regression.

## Key Findings

**1. High accuracy doesn't mean good predictions**

My baseline got 92.56% accuracy just by predicting nobody would default. The random forest got 92.44% accuracy but only caught 1 out of 134 defaults at the default threshold.

**2. Simpler models performed better**

Logistic regression had a ROC AUC of 0.7069, compared with 0.6724 for the random forest. LASSO also removed all three irrelevant features without removing any real predictors.

**3. Feature importance can be misleading**

MDI gave the random noise features relatively high importance, while permutation importance showed they barely helped predictions.

**4. Changing the threshold reduced expected losses**

Lowering the threshold from 0.5 to 0.172 reduced estimated losses from $972.51 to $889.47 per application. This assumed a 60% loss on defaulted loans, an 8% lost interest margin, and $500 in reputational costs for wrongly declined applicants.

**5. Calibration matters**

Platt scaling improved the test Brier score from 0.06768 to 0.06695. The validation-selected threshold after Platt scaling was 0.2124, although it did not improve test cost compared with the original forest at its own validation-selected threshold.

**6. The forest didn't significantly outperform LASSO**

McNemar's exact test gave a p-value of 1.0, meaning I couldn't find a significant difference in accuracy between the two models.

## Conclusion

This lab showed me that a model can have high accuracy and still be pretty bad at catching defaults. The random forest was more complicated but didn't outperform logistic regression.

I also learned that choosing a threshold based on financial costs matters more than just using 0.5. However, my original threshold was selected on test data, so its estimated savings may be too optimistic.

I wouldn't recommend putting the random forest into production yet. I'd want to see it consistently reduce losses on new data before approving it.
