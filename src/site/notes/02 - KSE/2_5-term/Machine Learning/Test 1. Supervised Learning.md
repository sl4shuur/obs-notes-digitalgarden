---
{"dg-publish":true,"dg-path":"KSE/Machine Learning/Test 1. Supervised Learning.md","permalink":"/kse/machine-learning/test-1-supervised-learning/","tags":["kse","ai","machine-learning"],"created":"2025-04-15T15:11:30.113+03:00","updated":"2025-04-16T01:05:36.637+03:00"}
---


# Test 1. Supervised Learning

---

$\textcolor{WildStrawberry}{\text{Question 1}}$

Explain the k‑Nearest Neighbour (k‑NN) algorithm. What are its main hyperparameters? How does the choice of distance metric and feature scaling affect its performance? Give an example of a scenario where k‑NN might perform poorly.

> [!success]+ Answer 1!  
> The k‑NN algorithm classifies a query point by finding the k closest training examples (according to some distance metric) and taking a majority vote (classification) or average (regression).
>
> - **Hyperparameters**:
>   - **k** (number of neighbours)
>   - **Distance metric** (e.g. Euclidean, Manhattan, Minkowski)
>   - **Weighting scheme** (uniform vs. distance‑weighted)
> - **Feature scaling** (e.g. standardization, min–max) is crucial: unscaled features with larger ranges dominate distance calculations.
> - **Distance metric** choice affects sensitivity to outliers and feature correlations.
> - **Poor scenario**: High‑dimensional sparse data (“curse of dimensionality”)—neighbours become equidistant, degrading performance.

---

$\textcolor{WildStrawberry}{\text{Question 2}}$

Write down the hypothesis function and cost function for ordinary least squares linear regression. What assumptions underlie this model? How do you evaluate the quality of a fitted linear regression model?

> [!success]+ Answer 2!
>
> - **Hypothesis**:
>   $$
>   >   h_{\mathbf w}(x) = w_0 + \sum_{j=1}^d w_j x_j
>   $$
> - **Cost (MSE)**:
>   $$
>   >   J(\mathbf w) = \frac{1}{2n}\sum_{i=1}^n \bigl(h_{\mathbf w}(x^{(i)}) - y^{(i)}\bigr)^2
>   $$
> - **Assumptions**:
>   1. **Linearity**: true relationship is linear in parameters.
>   2. **Homoscedasticity**: constant variance of errors.
>   3. **Independence** of errors.
>   4. **Normality** of error distribution (for inference).
> - **Evaluation**:
>   - **R²** (coefficient of determination)
>   - **RMSE** or **MAE** on hold‑out data
>   - Residual analysis for pattern/heteroscedasticity

---

$\textcolor{WildStrawberry}{\text{Question 3}}$

Describe how a decision tree makes splits. Define both Gini impurity and information gain. How does tree depth influence bias and variance? What strategies exist to prevent overfitting in trees?

> [!success]+ Answer 3!
>
> - **Splitting**: at each node, evaluate all possible feature–threshold pairs, choose the one that maximizes the reduction in impurity.
> - **Gini impurity** for node t:
>   $$
>   >   G(t) = 1 - \sum_{k=1}^K p_{k|t}^2
>   $$
> - **Entropy** and **information gain**:
>   $$
>   >   H(t) = -\sum_{k=1}^K p_{k|t}\log_2 p_{k|t},\quad IG = H(\text{parent}) - \sum_{c}\frac{n_c}{n}H(c)
>   $$
> - **Depth effect**:
>   - **Shallow trees** → high bias, low variance
>   - **Deep trees** → low bias, high variance
> - **Prevent overfitting**:
>   - **Pruning** (pre‑ or post‑)
>   - **Max depth**, **min samples per leaf** constraints
>   - **Ensemble methods** (bagging, boosting)

---

$\textcolor{WildStrawberry}{\text{Question 4}}$

Define overfitting and underfitting in supervised learning. How can you detect overfitting using training and validation errors? List and briefly describe three techniques to reduce overfitting.

> [!success]+ Answer 4!
>
> - **Underfitting**: model too simple, high error on both train & validation.
> - **Overfitting**: model too complex, low training error but high validation error.
> - **Detection**: plot training vs. validation error as model complexity grows; a widening gap (low train, rising val) signals overfitting.
> - **Mitigation techniques**:
>   1. **Regularization** (L1/L2 penalties) to constrain weights
>   2. **Early stopping** during iterative training
>   3. **Simplify model** (reduce depth/features) or **prune**

---

$\textcolor{WildStrawberry}{\text{Question 5}}$

Explain the purpose of splitting data into training, validation, and test sets. What are typical split ratios? When might you prefer a simple hold‑out split versus k‑fold cross‑validation?

> [!success]+ Answer 5!
>
> - **Training set**: fit model parameters.
> - **Validation set**: tune hyperparameters and detect overfitting.
> - **Test set**: unbiased estimate of final performance.
> - **Typical ratios**: 60/20/20, 70/15/15, or 80/10/10 (train/val/test).
> - **Hold‑out vs. CV**:
>   - **Hold‑out**: fast, adequate when data is abundant.
>   - **k‑fold CV**: more reliable on limited data, reduces variance in performance estimate.

---

$\textcolor{WildStrawberry}{\text{Question 6}}$

Describe k‑fold cross‑validation. How is the final performance metric computed? What are its advantages and disadvantages compared to a single hold‑out validation? How do you choose k?

> [!success]+ Answer 6!
>
> - **Procedure**: partition data into k equal folds; for each fold i, train on k–1 folds, evaluate on fold i; repeat for all i.
> - **Final metric**: average of the k fold scores (e.g. mean accuracy or mean RMSE).
> - **Advantages**:
>   - More stable, low‑variance estimate
>   - Utilizes all data for training and validation
> - **Disadvantages**:
>   - k× more training cost
>   - Potential data leakage if not stratified for classification
> - **Choosing k**: common values are 5 or 10; larger k gives lower bias but higher computational cost.

---

$\textcolor{WildStrawberry}{\text{Question 7}}$

Differentiate between classification and regression tasks. Give two real‑world examples of each. What types of model outputs and evaluation metrics are appropriate for each?

> [!success]+ Answer 7!
>
> - **Classification**: predict discrete labels.
>   - Examples: email spam detection; disease diagnosis (healthy vs. sick).
>   - Outputs: class labels or class probabilities.
>   - Metrics: accuracy, precision, recall, F1‑score, AUC.
> - **Regression**: predict continuous values.
>   - Examples: house price estimation; temperature forecasting.
>   - Outputs: real‑valued predictions.
>   - Metrics: MSE, RMSE, MAE, R².
