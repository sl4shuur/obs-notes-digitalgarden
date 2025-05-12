---
{"dg-publish":true,"permalink":"/02-kse/2-5-term/machine-learning/test-5-ensemble-learning/","tags":["kse","ai","machine-learning"],"created":"2025-04-16T00:59:25.636+03:00","updated":"2025-04-16T01:09:04.503+03:00"}
---


# Test 5. Ensemble Learning

---

$\textcolor{WildStrawberry}{\text{Question 1}}$

Explain the principle of bagging (bootstrap aggregating). How does bagging reduce variance? Outline the algorithm steps and discuss when bagging is most effective.

> [!success]+ Answer 1!  
> Bagging builds multiple models on different bootstrap samples of the training data and aggregates their predictions.
>
> - **Algorithm**:
>   1. For $b=1$ to $B$:
>      - Draw a bootstrap sample from the training set (sample with replacement).
>      - Train a base learner $h_b$ on this sample.
>   2. **Aggregate**: for regression, average $\hat y = \frac1B\sum_b h_b(x)$; for classification, majority vote.
> - **Variance reduction**: averaging uncorrelated (or weakly correlated) models lowers overall variance.
> - **Effective when**: using high‑variance learners (e.g., deep trees); less benefit for stable learners.

---

$\textcolor{WildStrawberry}{\text{Question 2}}$

Describe the random forest algorithm. How does it extend bagging? What role does feature randomness play? List key hyperparameters and their effects.

> [!success]+ Answer 2!  
> Random forest is a bagging ensemble of decision trees with random feature selection at each split.
>
> - **Extension of bagging**: in addition to bootstrap sampling, each split considers a random subset of features of size $m$ rather than all features.
> - **Feature randomness**: decorrelates trees, further reducing variance.
> - **Key hyperparameters**:
>   - **n_estimators** (number of trees): more trees → lower variance, higher cost.
>   - **max_features** (features per split): smaller → more decorrelation, higher bias.
>   - **max_depth/min_samples_leaf**: control tree complexity and overfitting.
>   - **bootstrap**: whether to use sampling with replacement.

---

$\textcolor{WildStrawberry}{\text{Question 3}}$

Explain the concept of boosting. Contrast it with bagging. Outline how AdaBoost or gradient boosting sequentially builds learners, and discuss how boosting reduces bias.

> [!success]+ Answer 3!  
> Boosting trains learners sequentially, where each new learner focuses on the errors of the combined ensemble so far.
>
> - **Contrast to bagging**: bagging trains in parallel on bootstrap samples; boosting trains sequentially on weighted data.
> - **AdaBoost**:
>   1. Initialize weights equally.
>   2. For each learner $t$:
>      - Train $h_t$ on weighted data.
>      - Compute error $\varepsilon_t$ and learner weight $\alpha_t = \tfrac12\ln\frac{1-\varepsilon_t}{\varepsilon_t}$.
>      - Update sample weights to emphasize misclassified points.
>   3. Final prediction: sign$\sum_t \alpha_t h_t(x)$.
> - **Gradient boosting**: fits each learner to the negative gradient of the loss w.r.t. current predictions.
> - **Bias reduction**: by focusing on residuals, boosting corrects systematic errors of prior learners.

---

$\textcolor{WildStrawberry}{\text{Question 4}}$

What enhancements does XGBoost introduce over vanilla gradient boosting? Describe its key algorithmic innovations and regularisation features. Which hyperparameters are most important for tuning XGBoost?

> [!success]+ Answer 4!  
> XGBoost adds system and algorithmic optimisations plus regularisation to gradient boosting:
>
> - **Innovations**:
>   - **Second‑order Taylor approximation** of loss for efficient split finding.
>   - **Weighted quantile sketch** for approximate tree learning on weighted data.
>   - **Parallel tree construction** and block‑structured data layout for speed.
>   - **Sparsity awareness** to handle missing values automatically.
> - **Regularisation**:
>   - **$\ell_1$** (alpha) and **$\ell_2$** (lambda) penalties on leaf weights.
>   - **Tree complexity** penalty (gamma) for minimum loss reduction to make a split.
> - **Key hyperparameters**:
>   - **eta** (learning rate)
>   - **max_depth**
>   - **subsample**, **colsample_bytree** (row/feature sampling)
>   - **alpha**, **lambda**, **gamma**

---

$\textcolor{WildStrawberry}{\text{Question 5}}$

Define stacking and blending. How do these meta‑ensemble methods combine base learners? Explain the procedure for creating a stacking ensemble and discuss potential pitfalls.

> [!success]+ Answer 5!  
> Stacking and blending train a “meta‑learner” on predictions of base learners to improve performance.
>
> - **Stacking**:
>   1. **Level‑0**: train multiple base models on the full training set (or via k‑fold to get out‑of‑fold predictions).
>   2. **Meta‑data**: collect base model predictions on validation folds as features.
>   3. **Level‑1**: train a meta‑learner on this meta‑data.
>   4. **Prediction**: base learners predict on new data; meta‑learner combines these.
> - **Blending**: similar but uses a hold‑out validation set instead of full k‑fold; simpler but less data‑efficient.
> - **Pitfalls**:
>   - **Overfitting** meta‑learner if using same data for base and meta training.
>   - Increased complexity and training time.
>   - Need careful cross‑validation to generate unbiased meta‑features.
