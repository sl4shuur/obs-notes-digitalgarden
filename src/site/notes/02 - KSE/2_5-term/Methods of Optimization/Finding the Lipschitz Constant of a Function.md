---
{"dg-publish":true,"dg-path":"KSE/Optimization Techniques/Finding the Lipschitz Constant of a Function.md","permalink":"/kse/optimization-techniques/finding-the-lipschitz-constant-of-a-function/","tags":["kse","math/calculus"],"created":"2025-03-09T21:12:13.030+02:00","updated":"2025-03-10T09:21:49.294+02:00"}
---


# Finding the Lipschitz Constant of a Function

---

We've already explored **[[02 - KSE/2_5-term/Methods of Optimization/07. Lipschitz Functions\|Lipschitz functions]]**, which have a bounded rate of change. Now, let's focus on **how to find the Lipschitz constant**—the key parameter that determines how "steep" a function can be.

---

## What is the Lipschitz Constant?

A function $f:\mathbb{R}^n \to \mathbb{R}$ is **Lipschitz continuous** with **constant $B$** if there exists a **finite** number $B \geq 0$ such that:

$$
|f(x) - f(y)| \leq B \|x - y\|, \quad \forall x, y \in D(f).
$$

The **Lipschitz constant** $B$ is the **smallest possible** value that satisfies this inequality for all $x, y$. It essentially tells us **how fast the function can change**—a small $B$ means slow growth, while a large $B$ means faster variation.

---

## Finding the Lipschitz Constant for a Function

There are different ways to compute the Lipschitz constant depending on whether we are dealing with:

1. Lipschitz continuity of <strong><span style="color: var(--color-purple);">function values</span></strong> ($B$)
2. Lipschitz continuity of the <strong><span style="color: var(--color-aqua);">gradient</span></strong> (smoothness condition, $L$)

---

## 1. Lipschitz Constant for Function Values

To find the Lipschitz constant $B$ for a function $f$, we evaluate:

$$
B = \sup_{x \neq y} \frac{|f(x) - f(y)|}{\|x - y\|}
$$

This means that **$B$ is the maximum rate of change** of the function over all possible pairs of points.

> [!tip] Recall:
> The **[[02 - KSE/1_2-term/Discrete Mathematics concepts/Supremum\|supremum]]** (or **least upper bound**) of a set is the **smallest number** that is greater than or equal to all elements in the set.

### Example 1

$f(x) = x^2$ on $\mathbb{R}$

To find the Lipschitz constant $B$, we compute:

$$
B = \sup_{x \neq y} \frac{|x^2 - y^2|}{|x - y|}
$$

Using the **difference of squares** identity:

$$
\frac{|x^2 - y^2|}{|x - y|} = |x + y|.
$$

Since $|x + y|$ can be arbitrarily large as $x, y \to \infty$, **$f(x) = x^2$ is not Lipschitz on $\mathbb{R}$**. However, on a **bounded domain**, say $[-a, a]$, we get:

$$
B = \sup_{x, y \in [-a, a]} |x + y| = 2a.
$$

Thus, $f(x) = x^2$ is **Lipschitz on a bounded interval**, with $B = 2a$.

---

## 2. Lipschitz Constant for the Gradient (Smoothness Constant)

A function is **$L$-smooth** (i.e., its gradient is Lipschitz) if:

$$
\|\nabla f(x) - \nabla f(y)\| \leq L \|x - y\|, \quad \forall x, y \in \mathbb{R}^n.
$$

To find **$L$**, we compute:

$$
L = \sup_{x} \|\mathbb{J}f(x)\|
$$

where **$\mathbb{J}f(x)$** is the **Jacobian** (matrix of <strong><span style="color: var(--color-aqua);">partial derivatives</span></strong>) of $f$ at $x$.

### Example 2

$f(x) = \frac{1}{2} x^2$

1. Compute the gradient:
   $$
   \nabla f(x) = x.
   $$
2. Compute the Lipschitz constant of the gradient:
   $$
   L = \sup_x |\nabla f(x)|.
   $$

Since $|\nabla f(x)| = |x|$ grows indefinitely, **$f(x)$ is not smooth on $\mathbb{R}$**. But on a **bounded domain** $[-a, a]$, we get:

$$
L = \sup_{x \in [-a, a]} |x| = a.
$$

So, for a bounded interval, the function is **$a$-smooth**.

---

## Lipschitz Constant from the Hessian

For **twice-differentiable functions**, the Lipschitz constant of the gradient can be found using the **Hessian matrix** $H_f(x)$. The **Lipschitz constant $L$** is given by:

$$
L = \sup_x \lambda_{\max}(H_f(x)),
$$

where **$\lambda_{\max}(H_f(x))$** is the <strong><span style="color: var(--color-cyan);">largest eigenvalue</span></strong> of the **[[02 - KSE/2_5-term/Methods of Optimization/Hessian matrix\|Hessian matrix]]**.

### Example 3

$f(x) = x^2 + y^2$

The Hessian is:

$$
H_f(x, y) =
\begin{bmatrix}
2 & 0 \\
0 & 2
\end{bmatrix}.
$$

The eigenvalues of this matrix are **both 2**, so:

$$
L = 2.
$$

This means $f(x) = x^2 + y^2$ is **2-smooth**.

---

## Summary

| Type of Lipschitz Constant              | Formula                                                 | Meaning                                   |
| --------------------------------------- | ------------------------------------------------------- | ----------------------------------------- |
| **Lipschitz function values ($B$)**     | $B = \sup_{x \neq y} \frac{\|f(x) - f(y)\|}{\|x - y\|}$ | Controls how fast function values change. |
| **Lipschitz gradient ($L$-smoothness)** | $L = \sup_x \|\mathbb{J}f(x)\|$                         | Controls how fast the gradient changes.   |
| **Hessian-based Lipschitz constant**    | $L = \sup_x \lambda_{\max}(H_f(x))$                     | Controls the curvature of the function.   |
