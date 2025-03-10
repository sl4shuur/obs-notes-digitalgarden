---
{"dg-publish":true,"dg-path":"KSE/Optimization Techniques/Proximal GD Idea Explained.md","permalink":"/kse/optimization-techniques/proximal-gd-idea-explained/","tags":["kse","math/calculus"],"created":"2025-03-10T10:13:56.221+02:00","updated":"2025-03-10T10:58:24.942+02:00"}
---


# Proximal GD Idea Explained

---

> [!tip] Related to:
> **[[02 - KSE/2_5-term/Methods of Optimization/14. PROXIMAL GRADIENT DESCENT\|14. PROXIMAL GRADIENT DESCENT]]**

## Classical Gradient Step for Minimizing $g(x)$

If we were minimizing only $g(x)$, the standard **gradient descent step** would be derived from a **first-order approximation**:

$$
x_{t+1} = \arg\min_{y \, \in \, \mathbb{R}^n} \left( g(x_t) + \nabla g(x_t)^T (y - x_t) + \frac{1}{2\gamma} \|y - x_t\|^2 \right).
$$

Here:

- The **first two terms** are the first-order Taylor expansion of $g(y)$ around $x_t$.
- The **third term** is a quadratic regularization (proximal term) that **keeps updates close to** $x_t$ to prevent large jumps.
  Actually, this term is the <strong><span style="color: var(--color-pink);">second-order Taylor expansion</span></strong> of $g(y)$ around $x_t$.

## Adding the $h(y)$ Term

When we introduce $\textcolor{var(--color-orange)}{h(y)}$, which is possibly <strong><span style="color: var(--color-orange);">non-smooth</span></strong>, we modify the update by **keeping the gradient step for $g(x)$ the same but adding $h(y)$ explicitly**:

$$
x_{t+1} = \arg\min_{y \, \in \, \mathbb{R}^n} \left( g(x_t) + \nabla g(x_t)^T (y - x_t) + \frac{1}{2\gamma} \|y - x_t\|^2 + \textcolor{var(--color-orange)}{h(y)} \right).
$$

Now, the function consists of:

1. A **linear approximation of $g(y)$**.
2. A **quadratic proximity term**.
3. The <strong><span style="color: var(--color-orange);">non-smooth</span></strong> function $h(y)$\*\*.

## Completing the Square

Since $g(x_t)$ is **independent** of $y$, we <strong><span style="color: var(--color-red);">ignore it</span></strong> in the minimization problem. The key step is recognizing that the **first two terms** can be rewritten using the squared norm:

$$
\nabla g(x_t)^T (y - x_t) + \frac{1}{2\gamma} \|y - x_t\|^2
$$

This term is the **first-order approximation of $g(x)$ plus a regularization**, and it can be rewritten in a more compact form:

$$
\frac{1}{2\gamma} \left\| y - \left(x_t - \gamma \nabla g(x_t)\right) \right\|^2
$$

## Understanding the Completing-the-Square Step

We need to rewrite the quadratic expression:

$$
\textcolor{CornflowerBlue}{\nabla g(x_t)^T (y - x_t)} + \frac{1}{2\gamma} \| y - x_t \|^2
$$

into a squared norm form plus a constant term.

---

## Step-by-Step Breakdown

### 1. Expand the squared norm

The Euclidean norm squared is given by:

$$
\| y - x_t \|^2 = (y - x_t)^T (y - x_t)
$$

So, we rewrite the term:

$$
\frac{1}{2\gamma} \| y - x_t \|^2 = \frac{1}{2\gamma} (y - x_t)^T (y - x_t)
$$

---

### 2. Introduce a shift using $\gamma \nabla g(x_t)$

We want to introduce a shifted term in the form $y - (x_t - \gamma \nabla g(x_t))$, so we add and subtract $\gamma \nabla g(x_t)$ cleverly.

Observe that:

$$
\textcolor{CornflowerBlue}{\nabla g(x_t)^T (y - x_t)} = \frac{1}{\gamma} \textcolor{red}{\gamma \nabla g(x_t)^T}(y - x_t)
$$

This suggests rewriting the term as:

$$
\textcolor{CornflowerBlue}{\nabla g(x_t)^T (y - x_t)} = \frac{1}{\gamma} (y - x_t)^T \textcolor{red}{(\gamma \nabla g(x_t))}
$$

---

### 3. Expand the squared norm

Consider the squared term:

$$
\| y - \textcolor{Apricot}{(x_t - \gamma \nabla g(x_t))} \|^2
$$

Expanding it:

$$
(y - \textcolor{Apricot}{(x_t - \gamma \nabla g(x_t))})^T (y - \textcolor{Apricot}{(x_t - \gamma \nabla g(x_t))})
$$

Breaking it down:

$$
(y - x_t + \textcolor{Apricot}{\gamma \nabla g(x_t)})^T (y - x_t + \textcolor{Apricot}{\gamma \nabla g(x_t)})
$$

Expanding using the identity $(a+b)^T(a+b) = a^T a + 2 a^T b + b^T b$:

$$
\| y - x_t \|^2 + \textcolor{CornflowerBlue}{2 \gamma \nabla g(x_t)^T (y - x_t)} + \textcolor{SpringGreen}{\gamma^2 \|\nabla g(x_t)\|^2}
$$

Dividing everything by $2\gamma$:

$$
\frac{1}{2\gamma} \| y - x_t \|^2 + \textcolor{CornflowerBlue}{\nabla g(x_t)^T (y - x_t)} + \textcolor{SpringGreen}{\frac{\gamma}{2} \|\nabla g(x_t)\|^2}
$$

Thus:

$$
\begin{aligned}

\frac{1}{2\gamma} \| y - x_t \|^2 + \textcolor{CornflowerBlue}{\nabla g(x_t)^T (y - x_t)} + \textcolor{SpringGreen}{\frac{\gamma}{2} \|\nabla g(x_t)\|^2}

&=

\frac{1}{2\gamma} \| y - \textcolor{Apricot}{(x_t - \gamma \nabla g(x_t))} \|^2 \\

\frac{1}{2\gamma} \| y - x_t \|^2 + \textcolor{CornflowerBlue}{\nabla g(x_t)^T (y - x_t)}

&=

\frac{1}{2\gamma} \| y - \textcolor{Apricot}{(x_t - \gamma \nabla g(x_t))} \|^2 - \textcolor{SpringGreen}{\frac{\gamma}{2} \|\nabla g(x_t)\|^2}

\end{aligned}
$$

---

### 4. Rearrange the expression

Comparing with the original form:

$$
\textcolor{CornflowerBlue}{\nabla g(x_t)^T (y - x_t)} + \frac{1}{2\gamma} \| y - x_t \|^2
$$

We get:

$$
\frac{1}{2\gamma} \| y - \textcolor{Apricot}{(x_t - \gamma \nabla g(x_t))} \|^2 - \textcolor{SpringGreen}{\frac{\gamma}{2} \|\nabla g(x_t)\|^2}
$$

This is the final transformed expression!

**BUT!** The final formula looks like this:

$$
x_{t+1} = \arg\min_{y \, \in \,\mathbb{R}^n} \left( \frac{1}{2\gamma} \|y - \textcolor{Apricot}{(x_t - \gamma \nabla g(x_t))}\|^2 + \textcolor{var(--color-orange)}{h(y)} \right)
$$

This is beacuse the term $\textcolor{SpringGreen}{\frac{\gamma}{2} \|\nabla g(x_t)\|^2}$ is a constant with respect to $y$ and can <strong><span style="color: var(--color-red);">be ignored</span></strong> in the minimization problem :)