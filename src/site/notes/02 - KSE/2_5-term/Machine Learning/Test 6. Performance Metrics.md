---
{"dg-publish":true,"dg-path":"KSE/Machine Learning/Test 6. Performance Metrics.md","permalink":"/kse/machine-learning/test-6-performance-metrics/","tags":["kse","ai","machine-learning"],"created":"2025-04-16T00:59:40.904+03:00","updated":"2025-04-16T01:12:30.065+03:00"}
---


# Test 6. Performance Metrics

---

$\textcolor{WildStrawberry}{\text{Question 1}}$

Define accuracy. Write its formula and explain in which scenarios accuracy is a suitable metric and when it can be misleading.

> [!success]+ Answer 1!  
> Accuracy measures the proportion of correct predictions:
>
> $$
> > \text{Accuracy} = \frac{\text{TP} + \text{TN}}{\text{TP} + \text{TN} + \text{FP} + \text{FN}}
> $$
>
> - **Suitable** when classes are balanced and all errors carry similar cost.
> - **Misleading** on imbalanced data: a model that always predicts the majority class can have high accuracy despite poor performance on the minority class.

---

$\textcolor{WildStrawberry}{\text{Question 2}}$

Define precision, recall, and F1‑score. Provide their formulas. Given a confusion matrix, explain how these metrics reflect different aspects of classification performance.

> [!success]+ Answer 2!
>
> - **Precision** (positive predictive value):
>   $$
>   >   \text{Precision} = \frac{\text{TP}}{\text{TP} + \text{FP}}
>   $$
> - **Recall** (sensitivity or true positive rate):
>   $$
>   >   \text{Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}}
>   $$
> - **F1‑score** (harmonic mean of precision and recall):
>   $$
>   >   F1 = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
>   $$
> - **Interpretation**:
>   - **Precision** focuses on the correctness of positive predictions.
>   - **Recall** focuses on coverage of actual positives.
>   - **F1** balances both, penalizing extreme imbalance between precision and recall.

---

$\textcolor{WildStrawberry}{\text{Question 3}}$

Explain the confusion matrix for a binary classifier. Label its four cells and describe how you derive accuracy, precision, recall, and specificity from it.

> [!success]+ Answer 3!  
> A binary confusion matrix:
>
> |                     | Predicted Positive | Predicted Negative |
> | ------------------- | ------------------ | ------------------ |
> | **Actual Positive** | TP                 | FN                 |
> | **Actual Negative** | FP                 | TN                 |
>
> - **Accuracy** = (TP + TN) / total
> - **Precision** = TP / (TP + FP)
> - **Recall** = TP / (TP + FN)
> - **Specificity** (true negative rate) = TN / (TN + FP)

---

$\textcolor{WildStrawberry}{\text{Question 4}}$

Define Mean Squared Error (MSE) and Root Mean Squared Error (RMSE). Provide their formulas and explain what each metric conveys about regression performance.

> [!success]+ Answer 4!
>
> - **MSE**: average squared difference between predictions and targets:
>   $$
>   >   \text{MSE} = \frac{1}{n}\sum\_{i=1}^n\bigl(y_i - \hat y_i\bigr)^2
>   $$
> - **RMSE**: square root of MSE, in the same units as the target:
>   $$
>   >   \text{RMSE} = \sqrt{\text{MSE}}
>   $$
> - **Interpretation**:
>   - **MSE** penalizes larger errors more heavily.
>   - **RMSE** is more interpretable, reflecting typical error magnitude.

---

$\textcolor{WildStrawberry}{\text{Question 5}}$

Describe the ROC curve and AUC. Define true positive rate and false positive rate. Explain how to construct the ROC curve and interpret the AUC value.

> [!success]+ Answer 5!
>
> - **True Positive Rate (TPR)** = Recall = TP / (TP + FN)
> - **False Positive Rate (FPR)** = FP / (FP + TN)
> - **ROC curve**: plot TPR vs. FPR as the classification threshold varies from 0 to 1.
> - **AUC** (Area Under the Curve): probability that a randomly chosen positive ranks higher than a negative.
>   - **AUC = 1.0**: perfect separation.
>   - **AUC = 0.5**: no better than random guessing.
> - **Use**: compare classifier discrimination ability independent of threshold or class balance.
