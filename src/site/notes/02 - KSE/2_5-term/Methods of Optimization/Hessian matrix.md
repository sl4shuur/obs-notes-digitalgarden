---
{"dg-publish":true,"dg-path":"KSE/Optimization Techniques/Hessian matrix.md","permalink":"/kse/optimization-techniques/hessian-matrix/","tags":["kse","math/calculus"],"created":"2025-03-03T14:49:52.484+02:00","updated":"2025-03-09T17:50:04.513+02:00"}
---

# Hessian matrix

---

## Hessian matrix: Understanding the second-order behavior of functions  

The Hessian matrix is a mathematical tool used to analyze the **curvature** of a function. It helps us determine whether a function is <strong><span style="color: var(--color-red);">convex</span></strong>, <strong><span style="color: var(--color-cyan);">concave</span></strong>, or <strong><span style="color: var(--color-aqua);">neither</span></strong> by looking at its **second-order derivatives**. In optimization, the Hessian is particularly useful because it tells us if a function has a **unique minimum** and whether standard optimization methods (like gradient descent) will work efficiently.  

![convex and concave functions.png|500](/img/user/assets/convex%20and%20concave%20functions.png)

---

### What is the Hessian matrix  

The Hessian of a function $f: \mathbb{R}^n \to \mathbb{R}$ is a **square matrix** containing all the **second-order partial derivatives** of the function. It is written as:  

$$
H_f(x) = \nabla^2 f(x) =
\begin{bmatrix}
\frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x_1}^2} & \frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x_1} \partial \textcolor{var(--color-cyan)}{x_2}} & \dots & \frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x_1} \partial \textcolor{var(--color-yellow)}{x_n}} \\
\frac{\partial^2 f}{\partial \textcolor{var(--color-cyan)}{x_2} \partial \textcolor{var(--color-red)}{x_1}} & \frac{\partial^2 f}{\partial \textcolor{var(--color-cyan)}{x_2}^2} & \dots & \frac{\partial^2 f}{\partial \textcolor{var(--color-cyan)}{x_2} \partial \textcolor{var(--color-yellow)}{x_n}} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial^2 f}{\partial \textcolor{var(--color-yellow)}{x_n} \partial \textcolor{var(--color-red)}{x_1}} & \frac{\partial^2 f}{\partial \textcolor{var(--color-yellow)}{x_n} \partial \textcolor{var(--color-cyan)}{x_2}} & \dots & \frac{\partial^2 f}{\partial \textcolor{var(--color-yellow)}{x_n}^2}
\end{bmatrix}
$$

Each entry of this matrix represents the **rate of change** of one partial derivative with respect to another variable. The **diagonal elements** represent how the function curves along each coordinate direction, while the **off-diagonal elements** describe how the curvature changes between different variables.  

---

### Why is the Hessian important  

The Hessian matrix is used to:

- **Determine convexity**: If the Hessian satisfies certain conditions, the function is convex.  
- **Classify critical points**: It tells us whether a point is a **local minimum, maximum, or a saddle point**.  
- **Optimize functions**: In machine learning, economics, and physics, the Hessian is used to efficiently minimize or maximize functions.  

---

## Understanding the Hessian in one dimension (1D case)  

In **one dimension**, the Hessian reduces to a single <strong><span style="color: var(--color-aqua);">second derivative</span></strong>:  

$$
H_f(x) = \frac{d^2 f}{dx^2}
$$  

Here’s how to interpret it:

- If $\frac{d^2 f}{dx^2} > 0$, the function is **convex** (curves upwards like a bowl).  
- If $\frac{d^2 f}{dx^2} < 0$, the function is **concave** (curves downward like an upside-down bowl).  
- If $\frac{d^2 f}{dx^2} = 0$, the function might be linear or have an **inflection point** (a change in curvature).  

![Convex And Concave Functions And Inflection Points General.png|500](/img/user/assets/Convex%20And%20Concave%20Functions%20And%20Inflection%20Points%20General.png)

### Example 1: quadratic function  

Consider the function  

$$
f(x) = x^2
$$  

Its **first derivative** is:  

$$
\frac{d f}{dx} = 2x
$$  

Its **second derivative** is:  

$$
\frac{d^2 f}{dx^2} = 2
$$  

Since $2 > 0$, the function is **convex** — its graph forms a **parabolic bowl** that always curves upwards.

![Convex And Concave Functions And Inflection Points Good Example.png|400](/img/user/assets/Convex%20And%20Concave%20Functions%20And%20Inflection%20Points%20Good%20Example.png)

---

### Example 2: cubic function  

Consider the function  

$$
f(x) = x^3
$$  

The **first derivative** is:  

$$
\frac{d f}{dx} = 3x^2
$$  

The **second derivative** is:  

$$
\frac{d^2 f}{dx^2} = 6x
$$  

This function is **not convex everywhere** because the second derivative depends on $x$:

- For $x > 0$, we have $\frac{d^2 f}{dx^2} > 0$, so it is convex.  
- For $x < 0$, we have $\frac{d^2 f}{dx^2} < 0$, so it is concave.  
- At $x = 0$, $\frac{d^2 f}{dx^2} = 0$, meaning the function has an **inflection point** where it transitions from concave to convex.  

![Convex And Concave Functions And Inflection Points Bad Example.png|400](/img/user/assets/Convex%20And%20Concave%20Functions%20And%20Inflection%20Points%20Bad%20Example.png)

This shows that **convexity is not just about checking one point** — it must hold <strong><span style="color: var(--color-red);">everywhere</span></strong>.  

---

## Understanding the Hessian in two dimensions (2D case)  

For a function of two variables $f(x, y)$, the Hessian is a $2 \times 2$ matrix:  

$$
H_f(x, y) =
\begin{bmatrix}
\frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x}^2} & \frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x} \partial \textcolor{var(--color-cyan)}{y}} \\
\frac{\partial^2 f}{\partial \textcolor{var(--color-cyan)}{y} \partial \textcolor{var(--color-red)}{x}} & \frac{\partial^2 f}{\partial \textcolor{var(--color-cyan)}{y}^2}
\end{bmatrix}
$$  

To determine convexity, we check if this matrix is **positive semidefinite** using the **leading principal minors test** (or checking all eigenvalues 🤷‍♀️):  

1. The first leading principal minor (the first diagonal element) must be **nonnegative**:  

   $$
   \frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x}^2} \geq 0
   $$  

2. The determinant of the Hessian matrix must be **nonnegative**:  

   $$
   \det(H_f) =
   \left( \frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x}^2} \right) \left( \frac{\partial^2 f}{\partial \textcolor{var(--color-cyan)}{y}^2} \right) - \left( \frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x} \partial \textcolor{var(--color-cyan)}{y}} \right)^2 \geq 0
   $$

These two conditions ensure that the function is **convex** in two dimensions.  

---

### Example 1: convex function in 2D  

Consider:  

$$
f(x, y) = x^2 + y^2
$$  

First, compute the second derivatives:  

$$ \frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x}^2} = 2, \quad \frac{\partial^2 f}{\partial \textcolor{var(--color-cyan)}{y}^2} = 2, \quad \frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x} \partial \textcolor{var(--color-cyan)}{y}} = 0 $$  

The Hessian matrix is:  

$$
H_f(x, y) =
\begin{bmatrix}
2 & 0 \\
0 & 2
\end{bmatrix}
$$  

Check the conditions:  

- The **first leading principal minor** is **$2 \geq 0$** ✅  
- The **determinant** is **$2 \cdot 2 - 0^2 = 4 \geq 0$** ✅  

Since both conditions hold, the function is **convex**.  

![Paraboloid.png](/img/user/assets/Paraboloid.png)

<strong><span style="color: var(--color-aqua);">Geometric intuition:</span></strong>
This function represents a **bowl-shaped surface** in 3D, confirming convexity.  

---

### Example 2: non-convex function in 2D  

Consider:  

$$
f(x, y) = x^2 - y^2
$$  

The Hessian matrix is:  

$$
H_f(x, y) =
\begin{bmatrix}
2 & 0 \\
0 & -2
\end{bmatrix}
$$  

Check the conditions:  

- The first leading principal minor is **$2 \geq 0$** ✅  
- The determinant is **$2 \cdot (-2) - 0^2 = -4$**, which is **negative** ❌  

![Hyperbolic Paraboloid.png](/img/user/assets/Hyperbolic%20Paraboloid.png)

Since the determinant is negative, the Hessian is <strong><span style="color: var(--color-red);">not positive semidefinite</span></strong>, meaning the function is **not convex** — it has a <strong><span style="color: var(--color-aqua);">saddle point</span></strong>.  

---

## Summary of the Hessian Matrix and Convexity

| Dimension | Hessian Form | Convexity Condition |
|-----------|------------|--------------------|
| 1D | $\frac{d^2 f}{d\textcolor{var(--color-red)}{x}^2}$ | $\frac{d^2 f}{d\textcolor{var(--color-red)}{x}^2} \geq 0$ |
| 2D | $\begin{bmatrix} \frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x}^2} & \frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x} \partial \textcolor{var(--color-cyan)}{y}} \\ \frac{\partial^2 f}{\partial \textcolor{var(--color-cyan)}{y} \partial \textcolor{var(--color-red)}{x}} & \frac{\partial^2 f}{\partial \textcolor{var(--color-cyan)}{y}^2} \end{bmatrix}$ | Determinant test: $D > 0$, $\frac{\partial^2 f}{\partial \textcolor{var(--color-red)}{x}^2} > 0$ |
| nD | $\nabla^2 f(x)$ | Matrix is **positive semidefinite** |

So, basically the idea of nD case is the same as 2D case, we need to proove that the Hessian matrix is **positive semidefinite**. We can choose any method to do that: <strong><span style="color: var(--color-cyan);">minors test</span></strong> or <strong><span style="color: var(--color-green);">eigenvalues test</span></strong>.

---

## Final Takeaways

- The **Hessian matrix** captures the **second-order behavior** of a function.
- In **one dimension**, convexity is determined by checking if $\frac{d^2 f}{d\textcolor{var(--color-red)}{x}^2} \geq 0$.
- In **higher dimensions**, the function is convex if the **Hessian matrix is positive semidefinite**.
- The **determinant test** helps determine convexity in 2D.
- The Hessian is widely used in **machine learning, physics, and optimization algorithms** to ensure stability and efficiency.
