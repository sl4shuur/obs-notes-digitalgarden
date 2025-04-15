---
{"dg-publish":true,"dg-path":"KSE/Machine Learning/Test 3. Deep Learning.md","permalink":"/kse/machine-learning/test-3-deep-learning/","tags":["kse","ai","machine-learning"],"created":"2025-04-16T00:58:19.517+03:00","updated":"2025-04-16T01:05:32.787+03:00"}
---


# Test 3. Deep Learning

---

$\textcolor{WildStrawberry}{\text{Question 1}}$

Describe the computational model of an artificial neuron. Write its mathematical equation. Explain the roles of the input features, weights, bias, and how the neuron’s output is produced.

> [!success]+ Answer 1!  
> An artificial neuron computes a weighted sum of inputs plus a bias, then applies an activation:
>
> $$
> > z = \sum_{i=1}^d w_i x_i + b,\quad y = \phi(z)
> $$
>
> - **Inputs** $x_i$: feature values.
> - **Weights** $w_i$: scale each input’s contribution.
> - **Bias** $b$: allows shifting the activation threshold.
> - **Activation** $\phi$: nonlinearly transforms $z$ into the neuron’s output $y$.

---

$\textcolor{WildStrawberry}{\text{Question 2}}$

Explain the forward pass in a feedforward neural network. How are activations computed layer by layer? Illustrate with a two‑layer (one hidden, one output) network.

> [!success]+ Answer 2!  
> In a forward pass, each layer’s outputs become the next layer’s inputs:
>
> 1. **Hidden layer**:
>    $$
>    >    z^{(1)} = W^{(1)} x + b^{(1)},\quad a^{(1)} = \phi\bigl(z^{(1)}\bigr)
>    $$
> 2. **Output layer**:
>    $$
>    >    z^{(2)} = W^{(2)} a^{(1)} + b^{(2)},\quad \hat y = \psi\bigl(z^{(2)}\bigr)
>    $$
>
> - $W^{(l)},b^{(l)}$: weights and biases of layer $l$.
> - $\phi,\psi$: activation functions (e.g., ReLU in hidden, softmax in output).

---

$\textcolor{WildStrawberry}{\text{Question 3}}$

Compare common activation functions—sigmoid, tanh, ReLU, and Leaky ReLU. For each, give its formula, output range, and discuss advantages and drawbacks. When might you choose one over another?

> [!success]+ Answer 3!
>
> - **Sigmoid**: $\sigma(z)=1/(1+e^{-z})$, range $(0,1)$.
>   - Pros: smooth, interpretable as probability.
>   - Cons: vanishing gradients for $|z|\gg0$.
> - **Tanh**: $\tanh(z)=(e^z-e^{-z})/(e^z+e^{-z})$, range $(-1,1)$.
>   - Pros: zero‑centered.
>   - Cons: still suffers vanishing gradients.
> - **ReLU**: $\max(0,z)$, range $[0,\infty)$.
>   - Pros: sparse activation, mitigates vanishing gradient.
>   - Cons: “dying ReLU” (units stuck at zero).
> - **Leaky ReLU**: $\max(αz,z)$ with small $α>0$, range $(-\infty,\infty)$.
>   - Pros: alleviates dying ReLU.
>   - Cons: adds a small negative slope hyperparameter.
> - **Choice**: ReLU/Leaky ReLU in deep nets for faster training; sigmoid/tanh in output layers for bounded outputs.

---

$\textcolor{WildStrawberry}{\text{Question 4}}$

Describe gradient descent optimization. Derive the weight‑update rule for a parameter $w$ given loss $L(w)$. Contrast batch, stochastic, and mini‑batch gradient descent, and name key hyperparameters.

> [!success]+ Answer 4!
>
> - **Update rule**:
>   $$
>   >   w \leftarrow w - \eta\,\frac{\partial L}{\partial w}
>   $$
>   where $\eta$ is the learning rate.
> - **Variants**:
>   - **Batch GD**: use all $n$ examples to compute gradient (stable but slow).
>   - **Stochastic GD**: update per example (noisy but fast).
>   - **Mini‑batch GD**: update per batch of size $m$ (balance of noise and speed).
> - **Hyperparameters**:
>   - Learning rate $\eta$
>   - Batch size $m$
>   - Momentum, decay schedules

---

$\textcolor{WildStrawberry}{\text{Question 5}}$

Explain the backpropagation algorithm. How does it use the chain rule to compute gradients for all weights in a multilayer network? Outline the main steps.

> [!success]+ Answer 5!
>
> 1. **Forward pass**: compute and cache activations $a^{(l)}$ and pre‑activations $z^{(l)}$.
> 2. **Output error**:  
>    $\delta^{(L)} = \nabla_{a}L \odot \phi'(z^{(L)})$.
> 3. **Backpropagate**: for $l=L-1,\dots,1$,
>    $$
>    >    \delta^{(l)} = \bigl(W^{(l+1)T}\delta^{(l+1)}\bigr)\odot \phi'(z^{(l)})
>    $$
> 4. **Gradient**:  
>    $\frac{\partial L}{\partial W^{(l)}} = \delta^{(l)}\,a^{(l-1)T},\quad \frac{\partial L}{\partial b^{(l)}} = \delta^{(l)}$.
> 5. **Update** weights via gradient descent.

---

$\textcolor{WildStrawberry}{\text{Question 6}}$

Define the vanishing gradient problem. Why does it occur in deep networks? What strategies (architectural or algorithmic) help mitigate it?

> [!success]+ Answer 6!
>
> - **Vanishing gradients**: gradients shrink exponentially as they backpropagate through many layers, slowing or stalling learning in early layers.
> - **Causes**:
>   - Activation derivatives $<1$ (e.g. sigmoid, tanh).
>   - Poor weight initialization.
> - **Mitigations**:
>   - Use ReLU or its variants.
>   - He or Xavier initialization.
>   - Batch normalization.
>   - Residual connections (ResNets).

---

$\textcolor{WildStrawberry}{\text{Question 7}}$

Outline the typical training loop for a neural network. What are the key steps performed each epoch and per batch? How do you integrate data loading, forward pass, loss computation, backward pass, and parameter updates?

> [!success]+ Answer 7!  
> **For each epoch**:
>
> 1. **Shuffle** training data.
> 2. **For each batch**:
>    - Load inputs $X$ and labels $y$.
>    - **Forward pass**: compute $\hat y = f(X)$.
>    - **Compute loss**: $L(\hat y,y)$.
>    - **Backward pass**: compute gradients $\nabla_\theta L$.
>    - **Update** parameters $\theta \leftarrow \theta - \eta\nabla_\theta L$.
> 3. **Validation**: evaluate on hold‑out set.
> 4. **Logging**: track metrics, adjust learning rate or early stop.

---

$\textcolor{WildStrawberry}{\text{Question 8}}$

Describe the core components of a convolutional neural network (CNN). What is a convolutional layer? Explain the convolution operation, receptive field, pooling layers, and how CNNs exploit spatial structure.

> [!success]+ Answer 8!
>
> - **Convolutional layer**: applies learnable filters $K$ over input feature maps via sliding-window dot products:
>   $$
>   >   (I * K)(i,j) = \sum_{u,v} I(i+u,j+v)\,K(u,v)
>   $$
> - **Receptive field**: region of input influencing a given output unit.
> - **Pooling layer**: down‑samples feature maps (e.g. max or average) to reduce spatial size and introduce invariance.
> - **Spatial exploitation**: weight sharing (same filter across locations) and local connectivity capture translational features efficiently.
