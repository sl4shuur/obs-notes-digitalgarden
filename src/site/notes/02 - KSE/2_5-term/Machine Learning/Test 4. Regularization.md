---
{"dg-publish":true,"dg-path":"KSE/Machine Learning/Test 4. Regularization.md","permalink":"/kse/machine-learning/test-4-regularization/","tags":["kse","ai","machine-learning"],"created":"2025-04-16T00:58:53.350+03:00","updated":"2025-05-12T15:49:40.294+03:00"}
---


# Test 4. Regularization

---

$\textcolor{WildStrawberry}{\text{Question 1}}$

Define L1 and L2 regularization. Write their penalty terms and explain how each influences model weights. Discuss the geometric interpretation of both and when you might prefer one over the other.

> [!success]+ Answer 1!
>
> - **L1 penalty**: $\lambda\sum_j|w_j|$
>   - Encourages **sparsity**—many weights driven exactly to zero.
>   - Geometry: diamond‑shaped constraint region, corners align with axes → solutions on axes.
> - **L2 penalty**: $\tfrac{\lambda}{2}\sum_j w_j^2$
>   - Encourages **small** but nonzero weights.
>   - Geometry: circular (ellipsoidal) constraint region → smooth shrinkage.
> - **Preference**:
>   - Use **L1** when you want feature selection or interpretability.
>   - Use **L2** when you want to shrink weights smoothly and handle multicollinearity.

---

$\textcolor{WildStrawberry}{\text{Question 2}}$

Describe Lasso regression. Provide its optimization objective. Explain how Lasso can perform variable selection and discuss methods for choosing the regularisation parameter $\lambda$.

> [!success]+ Answer 2!
>
> - **Objective**:
>   $$
>   >   \min_{w}\;\frac{1}{2n}\sum_{i=1}^n\bigl(y^{(i)}-w^T x^{(i)}\bigr)^2 + \lambda\sum_j|w_j|
>   $$
> - **Variable selection**: the L1 penalty drives some coefficients exactly to zero, effectively selecting a subset of features.
> - **Choosing $\lambda$**:
>   - **Cross‑validation** (e.g. k‑fold) to balance bias–variance.
>   - **Information criteria** (AIC, BIC) when model likelihood is known.
>   - **Regularisation path** (LARS algorithm) to inspect coefficient trajectories.

---

$\textcolor{WildStrawberry}{\text{Question 3}}$

Describe Ridge regression. Provide its optimization objective and derive the closed‑form solution. Discuss how Ridge addresses multicollinearity and affects the bias–variance trade‑off.

> [!success]+ Answer 3!
>
> - **Objective**:
>   $$
>   >   \min_{w}\;\frac{1}{2n}\sum_{i=1}^n\bigl(y^{(i)}-w^T x^{(i)}\bigr)^2 + \frac{\lambda}{2}\sum_j w_j^2
>   $$
> - **Closed‑form**:
>   $$
>   >   w = (X^T X + \lambda I)^{-1}X^T y
>   $$
> - **Multicollinearity**: adding $\lambda I$ ensures $X^T X + \lambda I$ is invertible, stabilizing estimates.
> - **Bias–variance**: increases bias (shrinks coefficients) but reduces variance, often lowering overall error on unseen data.

---

$\textcolor{WildStrawberry}{\text{Question 4}}$

Explain weight decay in the context of neural network training. Show how weight decay modifies the standard gradient descent update. How is weight decay equivalent to L2 regularisation, and what implementation differences should you be aware of?

> [!success]+ Answer 4!
>
> - **Standard GD**: $w \leftarrow w - \eta\,\nabla_w L$
> - **With weight decay**:
>   $$
>   >   w \leftarrow w - \eta\bigl(\nabla_w L + \lambda w\bigr)
>   \quad\Longleftrightarrow\quad
>   w \leftarrow (1 - \eta\lambda)w - \eta\,\nabla_w L
>   $$
> - **Equivalence**: the extra $\lambda w$ term is exactly the gradient of $\tfrac{\lambda}{2}\|w\|^2$.
> - **Implementation**:
>   - Some optimizers (e.g. AdamW) decouple weight decay from adaptive learning rates to avoid bias.
>   - Ensure you apply decay to weights only, not to biases or batch‑norm parameters.

---

$\textcolor{WildStrawberry}{\text{Question 5}}$

Describe dropout regularisation. For a given layer, explain what happens during training and inference. What problem does dropout address, and how does it approximate model averaging? How do you choose an appropriate dropout rate?

> [!success]+ Answer 5!
>
> - **Training**: randomly “drop” each neuron with probability $p$, i.e., multiply activations by Bernoulli mask $m_i\sim\mathrm{Bern}(1-p)$.
> - **Inference**: scale activations by $1-p$ (or use inverted dropout at training time).
> - **Addresses**: co‑adaptation of neurons, reduces overfitting by forcing redundant representations.
> - **Model averaging**: dropout samples a subnetwork each batch; inference approximates averaging over all $2^n$ subnetworks.
> - **Choosing $p$**: common values 0.2–0.5; tune via validation—higher for large fully‑connected layers, lower for convolutional layers.

---

$\textcolor{WildStrawberry}{\text{Question 6}}$

Explain data augmentation as a regularisation technique. Give examples for image and text data. How does augmentation reduce overfitting, and how do you integrate it into the training pipeline?

> [!success]+ Answer 6!
>
> - **Concept**: synthetically increase dataset size by applying label‑preserving transformations.
> - **Image examples**: random crops, flips, rotations, color jitter, Gaussian noise.
> - **Text examples**: synonym replacement, random insertion/deletion, back‑translation.
> - **Effect**: exposes model to varied inputs, making it more robust and reducing overfitting.
> - **Integration**: apply augmentations on‑the‑fly during data loading (e.g., in PyTorch `Dataset` or TensorFlow `tf.data`), ensuring each epoch sees new variants.
