---
{"dg-publish":true,"dg-path":"KSE/Optimization Techniques/How to Calculate the Subgradient.md","permalink":"/kse/optimization-techniques/how-to-calculate-the-subgradient/","tags":["kse","math/calculus"],"created":"2025-03-10T12:13:41.719+02:00","updated":"2025-03-10T14:37:43.827+02:00"}
---


# How to Calculate the Subgradient?

---

A **[[02 - KSE/2_5-term/Methods of Optimization/08. Subgradient and subdifferential\|subgradient]]** is a generalization of the gradient for **non-differentiable** convex functions. Below are key cases for finding subgradients.

---

## 1️. Subgradient of a Weighted Sum

Let $f_1(x), f_2(x), \dots, f_m(x)$ be **convex** functions on $\mathbb{R}^h$, and let $d_1, d_2, \dots, d_m \in \mathbb{R}_+$.

If we define:

$$
f(x) = \sum_{i=1}^{m} d_i f_i(x),
$$

then the subdifferential is:

$$
\partial f(x) = \sum_{i=1}^{m} d_i \partial f_i(x).
$$

🔹 **Key Insight:** The subgradient of a weighted sum of convex functions is the weighted sum of their subgradients.

---

## 2️. Subgradient of the Maximum Function

Let $f_1(x), f_2(x), \dots, f_m(x)$ be **convex** functions on $\mathbb{R}^h$, and define:

$$
f(x) = \max_i f_i(x).
$$

Then, the subdifferential is given by:

$$
\partial f(x) = \text{conv} \left( \bigcup_i \partial f_i(x) \right).
$$

where **conv** denotes the convex hull of the union of all subgradients.

### Convex Combination of Subgradients

For any set of subgradients $a_1, a_2, \dots, a_m$, their convex combination is:

$$
\text{conv} \left( \bigcup_i a_i \right) = \lambda_1 a_1 + \lambda_2 a_2 + \dots + \lambda_m a_m,
$$

where:

- $\lambda_i \geq 0$
- $\sum_{i} \lambda_i = 1$

🔹 **Key Insight:** The subgradient of $\max_i f_i(x)$ is the convex hull of the union of individual subgradients.

---

## 3️. Subgradient of a Scaled Function

If $f(x)$ is **convex** on $\mathbb{R}^h$ and we define:

$$
g(x) = d f(x), \quad d > 0,
$$

then the subdifferential satisfies:

$$
\partial (d f(x)) = d \partial f(x).
$$

🔹 **Key Insight:** Scaling a function by $d > 0$ scales its subgradients by the same factor.

---

## Summary

| Function                          | Subdifferential                                                        |
| --------------------------------- | ---------------------------------------------------------------------- |
| **Sum:** $f(x) = \sum d_i f_i(x)$ | $\partial f(x) = \sum d_i \partial f_i(x)$                             |
| **Max:** $f(x) = \max_i f_i(x)$   | $\partial f(x) = \text{conv} \left( \bigcup_i \partial f_i(x) \right)$ |
| **Scaling:** $f(x) = d f(x)$      | $\partial (d f(x)) = d \partial f(x)$                                  |

These rules are essential when dealing with **non-smooth convex optimization** problems! 🚀


## 1D Examples
### Example 1: Absolute Value Function
Consider the function:

$$
f(x) = |x|
$$

This function is **not differentiable at $x = 0$** but is **convex**. The subgradient is:

$$
\partial f(x) =
\begin{cases}
    \{1\}, & x > 0 \\
    \{-1\}, & x < 0 \\
    [-1,1], & x = 0
\end{cases}
$$

🔹 **Interpretation**: At $x = 0$, any value in $[-1,1]$ is a valid subgradient because the function has a "kink" at $x=0$.

---

### Example 2: Maximum of Two Linear Functions
Consider:

$$
f(x) = \max(2x, -x)
$$

- If $x < 0$, then $f(x) = -x$ and $\nabla f(x) = -1$.
- If $x > 0$, then $f(x) = 2x$ and $\nabla f(x) = 2$.
- If $x = 0$, then $f(x) = \max(0,0) = 0$, so:

  $$
  \partial f(0) = \text{conv}(\{-1,2\}) = [-1,2].
  $$

🔹 **Interpretation**: The function takes the gradient of the active branch, but at $x = 0$, the subgradient is any convex combination of $-1$ and $2$.

---

## 2D Examples
### Example 3: Euclidean Norm Function
Consider the function:

$$
f(x,y) = \sqrt{x^2 + y^2}
$$

which is the **Euclidean norm** (distance from the origin). The gradient is:

$$
\nabla f(x,y) = \left( \frac{x}{\sqrt{x^2 + y^2}}, \frac{y}{\sqrt{x^2 + y^2}} \right), \quad (x,y) \neq (0,0).
$$

At the origin $(0,0)$, the function is not differentiable. The subgradient is the **unit ball**:

$$
\partial f(0,0) = \{ (a,b) \ | \ a^2 + b^2 \leq 1 \}.
$$

🔹 **Interpretation**: The subgradient at the origin includes all points inside the unit disk.

<strong><span style="color: var(--color-aqua);">Why is the subgradient the unit ball?</span></strong>

Since the function is **[[02 - KSE/2_5-term/Methods of Optimization/03. Convex Functions\|convex]]**, we can use the **[[02 - KSE/2_5-term/Methods of Optimization/08. Subgradient and subdifferential\|subgradient definition]]**:  
The **subdifferential** at $(0,0)$ is the set of all vectors $(a,b)$ satisfying:

$$
f(x,y) \geq f(0,0) + \langle (a,b), (x, y) \rangle, \quad \forall (x,y).
$$

Substituting $f(0,0) = 0$:

$$
\sqrt{x^2 + y^2} \geq ax + by, \quad \forall (x,y).
$$

By the **[[02 - KSE/1_3-term/Applied Linear Algebra/Cauchy – Schwarz Inequality\|Cauchy-Schwarz inequality]]**, this holds if and only if:

$$
a^2 + b^2 \leq 1.
$$

Thus, the **subgradient at $(0,0)$ is the unit disk**:

$$
\partial f(0,0) = \{ (a,b) \ | \ a^2 + b^2 \leq 1 \}.
$$

---

### Example 4: Maximum of Two Planes
Consider:

$$
f(x,y) = \max(x, y)
$$

- If $x > y$, then $f(x,y) = x$ and $\nabla f(x,y) = (1,0)$.
- If $y > x$, then $f(x,y) = y$ and $\nabla f(x,y) = (0,1)$.
- If $x = y$, then the subgradient is:

  $$
  \partial f(x,y) = \text{conv}(\{(1,0), (0,1)\}).
  $$

which is the set of points:

$$
\lambda (1,0) + (1-\lambda)(0,1), \quad 0 \leq \lambda \leq 1.
$$

🔹 **Interpretation**: At points where $x = y$, any convex combination of $(1,0)$ and $(0,1)$ is a valid subgradient.

---

## Summary of Key Results

| **Function**       | **Subgradient $\partial f(x)$**                                                                                |
| ------------------ | -------------------------------------------------------------------------------------------------------------- |
| $f(x) = \|x\|$     | $\{-1\}$ for $x<0$, $\{1\}$ for $x>0$, $[-1,1]$ at $x=0$                                                       |
| $\max(2x, -x)$     | $\{-1\}$ for $x<0$, $\{2\}$ for $x>0$, $[-1,2]$ at $x=0$                                                       |
| $\sqrt{x^2 + y^2}$ | $\left(\frac{x}{\sqrt{x^2+y^2}}, \frac{y}{\sqrt{x^2+y^2}}\right)$ for $(x,y) \neq (0,0)$; unit ball at $(0,0)$ |
| $\max(x, y)$       | $(1,0)$ if $x > y$, $(0,1)$ if $y > x$, convex hull of $(1,0)$ and $(0,1)$ if $x=y$                            |

These examples illustrate how **subgradients generalize gradients** for **non-differentiable convex functions**. 🚀

