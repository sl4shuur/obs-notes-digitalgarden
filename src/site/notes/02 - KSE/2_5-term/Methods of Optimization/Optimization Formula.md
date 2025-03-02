---
{"dg-publish":true,"dg-path":"KSE/Optimization Techniques/Optimization Formula.md","permalink":"/kse/optimization-techniques/optimization-formula/","tags":["kse","math/calculus"],"created":"2025-02-12T18:37:11.056+02:00","updated":"2025-02-24T12:54:47.242+02:00"}
---


# Optimization Formula

---

At its core, an **optimization problem** is about finding the best possible outcome given certain conditions. The general mathematical formulation is:

$$
\min f(x), \quad \text{where } x \in \Omega \subseteq \mathbb{R}^n
$$

Let’s go step by step to understand what each part means.

## 1. What does $x$ represent?

- $x$ is the **decision variable** (or a vector of variables).
- It represents **the choices we can make** in the optimization problem.
- Depending on the problem, $x$ could be:
  - The **quantity of items** to produce in a factory.
  - The **investment amount** in different stocks.
  - The **coordinates** of a drone trying to find the shortest path.
  - The **weights** in a machine learning model.

If there are multiple variables in our problem (e.g., multiple things to decide at once), then $x$ is a **vector**:

$$
x = (x_1, x_2, ..., x_n)
$$

For example, if you are deciding how much money to invest in **3 different assets**, your decision variable could be:

$$
x = (x_1, x_2, x_3) = \text{"Amount invested in stocks, bonds, and real estate"}
$$

---

## 2. What is $\mathbb{R}^n$?

- The symbol **$\mathbb{R}$** represents the set of **real numbers** (all numbers that are not imaginary, including decimals and fractions).
- The notation **$\mathbb{R}^n$** means an **n-dimensional space of real numbers**.
- In simple terms, $\mathbb{R}^n$ is just **a collection of n real numbers**.

💡 **Analogy**:  
Think of **$\mathbb{R}^1$** as a **number line** (1D). If you have **$\mathbb{R}^2$**, it’s a **plane** (2D, like a graph with x and y axes). When you move to **$\mathbb{R}^3$**, you’re in a **3D space**. More dimensions? Just extend the idea!

For example:

- If **$n = 1$**, then $x$ is just one number: **$x \in \mathbb{R}$** (like a temperature or price).
- If **$n = 2$**, then $x = (x_1, x_2) \in \mathbb{R}^2$ is like a coordinate on a 2D graph.
- If **$n = 3$**, then $x = (x_1, x_2, x_3) \in \mathbb{R}^3$ is a point in 3D space.
- If **$n = 100$**, then $x$ is a **100-dimensional** vector—impossible to visualize but useful in things like AI and machine learning.

---

## 3. What is $f(x)$?

- This is called the **objective function**.
- It measures **what we are trying to minimize or maximize**.
- The function **assigns a value** to each possible choice of $x$.

For example:

- In **logistics**, $f(x)$ could be **the total cost of delivering packages**.
- In **machine learning**, $f(x)$ could be **the error of a model**.
- In **finance**, $f(x)$ could be **the risk of an investment portfolio**.

If we **minimize** $f(x)$, we are looking for the **best decision** that results in the **lowest cost, error, or risk**.

---

## 4. What is $\Omega$? (Feasible Region)

This is a crucial part, and the previous explanation was too vague. Let’s refine it:

- **$\Omega$ is the set of all possible values of $x$ that satisfy certain conditions.**
- It **restricts** which choices of $x$ are valid.
- If there are **no restrictions**, then we say we have **unconstrained optimization** and $\Omega = \mathbb{R}^n$.
- If there **are restrictions**, then $\Omega$ is a **subset** of $\mathbb{R}^n$.

## Examples of $\Omega$ in Real Life

<strong><span style="color: var(--color-green);">Example 1: Packing a Suitcase (Constrained Optimization)</span></strong>

- You have a suitcase with a weight limit of **20kg**.
- You need to pack **clothes, shoes, and electronics**.
- The total weight of all items **must be less than 20kg**.
- Your feasible region **$\Omega$** is the set of all possible combinations of items that fit within this weight limit.

Mathematically, if $x_1, x_2, x_3$ represent the weights of different items, then:

$$
\Omega = \{ (x_1, x_2, x_3) \mid x_1 + x_2 + x_3 \leq 20 \}
$$

So, $\Omega$ is the set of all possible combinations of weights that **don’t exceed 20kg**. It's not the same as $\mathbb{R}^3$ because we have a **weight constraint!**.

---

<strong><span style="color: var(--color-green);">Example 2: Investment Portfolio</span></strong>

- You have **$100,000** to invest.
- You can allocate money into **stocks, bonds, and cryptocurrency**.
- The total investment cannot exceed **$100,000**.
- Your feasible region $\Omega$ is:

$$
\Omega = \{ (x_1, x_2, x_3) \mid x_1 + x_2 + x_3 \leq 100000, x_1, x_2, x_3 \geq 0 \}
$$

(We also restrict that investments **must be non-negative**, meaning you can't invest a negative amount!)

---
