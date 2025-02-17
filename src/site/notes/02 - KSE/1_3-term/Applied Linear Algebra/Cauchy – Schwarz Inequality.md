---
{"dg-publish":true,"permalink":"/02-kse/1-3-term/applied-linear-algebra/cauchy-schwarz-inequality/","tags":["kse","math/linal"],"created":"2025-02-17T13:08:49.930+02:00","updated":"2025-02-17T20:22:09.731+02:00"}
---


# Cauchy – Schwarz Inequality

---

For all real vectors (?) $\mathbf{x}$ and $\mathbf{y}$, the **Cauchy – Schwarz inequality** states:

$$
| \mathbf{x} \cdot \mathbf{y} | \leq \|\mathbf{x}\| \|\mathbf{y}\|
$$

This inequality is equivalent to the **triangle inequality** for a norm in a space with a scalar product...

Before we dive into proving the Cauchy – Schwarz inequality, let’s clear up an important distinction between absolute value and norm  —  two concepts that often look similar but are different in meaning.

---

## What’s the Difference Between $|x|$ and $\|x\|$?

- $|x|$ (**Absolute value**):  
  Measures the distance of a number from zero on the real number line.
- If $x$ is a single number (a scalar):
  $$
  |x| = \begin{cases}
  x, & \text{if } x \geq 0 \\[10pt]
  -x, & \text{if } x < 0
  \end{cases}
  $$
  
<strong><span style="color: var(--color-green);">Example</span></strong>: $|5| = 5$, $|-5| = 5$.

---

- $\|\mathbf{x}\|$ (**Norm**):  
  Measures the length (magnitude) of a vector in space. For a vector $\mathbf{x} = (x_1, x_2, \dots, x_n)$, the most common norm is the **Euclidean norm**:
  $$
  \|\mathbf{x}\| = \sqrt{x_1^2 + x_2^2 + \dots + x_n^2}
  $$
  
<strong><span style="color: var(--color-green);">Example</span></strong>: For $\mathbf{x} = (3,4)$,
$$
\|\mathbf{x}\| = \sqrt{3^2 + 4^2} = 5
$$

---

**Key Difference**

- $|x|$ measures the length of a single number on a line. It's just a **modulus**.
- $\|\mathbf{x}\|$ measures the length of a vector in multi-dimensional space. Norms could be **different**, but the *Euclidean norm* is the most common.

---

## Cauchy – Schwarz Inequality: The Statement

The Cauchy – Schwarz inequality says:

$$
| \mathbf{x} \cdot \mathbf{y} | \leq \|\mathbf{x}\| \|\mathbf{y}\|
$$

Where:

- $\mathbf{x} \cdot \mathbf{y}$ is the dot product of vectors $\mathbf{x}$ and $\mathbf{y}$, defined as:
  $$
  \mathbf{x} \cdot \mathbf{y} = x_1y_1 + x_2y_2 + \dots + x_ny_n
  $$
  OR
  $$
  \mathbf{x} \cdot \mathbf{y} = \|\mathbf{x}\| \|\mathbf{y}\| \cos(\theta)
  $$
  where $\theta$ is the angle between the vectors.
- $|\mathbf{x} \cdot \mathbf{y}|$ is the absolute value of the dot product (just a scalar).
- $\|\mathbf{x}\|$ and $\|\mathbf{y}\|$ are the magnitudes (lengths) of the vectors.

So, basically, looking at the **dot product formula** with $\cos(\theta)$, the Cauchy – Schwarz inequality tells us that the dot product is always **bounded by the lengths** of the vectors.
$cos(\theta)$ can never exceed 1, so the dot product can never exceed the product of the lengths.

---

## What Does It Mean?

> [!Quote] Cauchy – Schwarz inequality tells us:
> The dot product between two vectors is always smaller than or equal to the product of their lengths.

It’s like comparing the "*shadow*" of one vector on another to their total lengths. The dot product measures the alignment between vectors:

- If the vectors are in the same direction, the dot product is at its <strong><span style="color: var(--color-red);">maximum</span></strong>.
- If they are at right angles (90°), the dot product is <strong><span style="color: var(--color-cyan);">zero</span></strong>.
- If they point in opposite directions, the dot product is <strong><span style="color: var(--color-orange);">negative</span></strong> but still within the bound.

---

## Proof of the Cauchy – Schwarz Inequality

Let’s prove it step by step using a clever trick with quadratic equations:

### Step 1: Start with a General Vector Expression

For any real vectors $\mathbf{x}$ and $\mathbf{y}$, define:

$$
f(\lambda) = \|\mathbf{x} - \lambda \mathbf{y}\|^2
$$

> [!Remark] Remark
> $f(\lambda)$ is a function of a real parameter $\lambda$ that returns the norm of the difference between $\mathbf{x}$ and $\lambda \mathbf{y}$.
> In other words, it’s the **squared distance** between the vectors.

<svg xmlns="http://www.w3.org/2000/svg" version="1.1" viewBox="0 0 880.6554473736549 584.2825176683946" width="400" height="584.2825176683946" class="excalidraw-svg"><!-- svg-source:excalidraw --><metadata/><defs><style class="style-fonts">      @font-face { font-family: Excalifont; src: url(data:font/woff2;base64,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); }</style></defs><rect x="0" y="0" width="880.6554473736549" height="584.2825176683946" fill="#ffffff"/><g stroke-linecap="round"><g transform="translate(73.88107066629578 534.2848460786272) rotate(0 53.933479309081974 -202.73320897420263)"><path d="M-1.11 0.43 C16.82 -67.39, 90.03 -338.56, 108.31 -406.22 M0.51 -0.39 C18.25 -68.14, 89.65 -337.77, 107.6 -405.08" stroke="#ffd43b" stroke-width="4" fill="none"/></g><g transform="translate(73.88107066629578 534.2848460786272) rotate(0 53.933479309081974 -202.73320897420263)"><path d="M109.83 -380.18 C109.59 -388.52, 106.8 -397.1, 107.6 -405.08 M109.83 -380.18 C109.9 -386.91, 109.33 -395.77, 107.6 -405.08" stroke="#ffd43b" stroke-width="4" fill="none"/></g><g transform="translate(73.88107066629578 534.2848460786272) rotate(0 53.933479309081974 -202.73320897420263)"><path d="M93.3 -384.57 C99.1 -391.16, 102.32 -398.14, 107.6 -405.08 M93.3 -384.57 C98.17 -389.86, 102.43 -397.43, 107.6 -405.08" stroke="#ffd43b" stroke-width="4" fill="none"/></g></g><mask/><g stroke-linecap="round"><g transform="translate(74.88105540750672 534.2848460786272) rotate(0 156.43347930908197 -183.7332127888999)"><path d="M0.4 -1.06 C52.51 -62.29, 261.77 -306.16, 313.7 -367.41 M-0.85 1 C51.08 -60.02, 260.65 -304.38, 313.19 -365.84" stroke="#ffd43b" stroke-width="4" fill="none"/></g><g transform="translate(74.88105540750672 534.2848460786272) rotate(0 156.43347930908197 -183.7332127888999)"><path d="M304.41 -342.44 C306.05 -350.16, 311.32 -362.11, 313.19 -365.84 M304.41 -342.44 C306.14 -348.17, 308.39 -353.15, 313.19 -365.84" stroke="#ffd43b" stroke-width="4" fill="none"/></g><g transform="translate(74.88105540750672 534.2848460786272) rotate(0 156.43347930908197 -183.7332127888999)"><path d="M291.42 -353.56 C298.1 -357.01, 308.41 -364.64, 313.19 -365.84 M291.42 -353.56 C295.89 -356.94, 300.86 -359.59, 313.19 -365.84" stroke="#ffd43b" stroke-width="4" fill="none"/></g></g><mask/><g transform="translate(51.271474521659115 248.69735784769819) rotate(0 21.5 41.34619052593507)"><text x="0" y="58.28159016535824" font-family="Excalifont, Xiaolai, Segoe UI Emoji" font-size="66.1539048414963px" fill="#ffd43b" text-anchor="start" style="white-space: pre;" direction="ltr" dominant-baseline="alphabetic">X</text></g><g transform="translate(330.2714897804482 304.69741888285444) rotate(0 19.5 41.34619052593507)"><text x="0" y="58.28159016535824" font-family="Excalifont, Xiaolai, Segoe UI Emoji" font-size="66.1539048414963px" fill="#ffd43b" text-anchor="start" style="white-space: pre;" direction="ltr" dominant-baseline="alphabetic">y</text></g><g stroke-linecap="round"><g transform="translate(392.0692859798298 165.62203939017854) rotate(0 -105.49999237060547 -17.99999237060547)"><path d="M-0.03 -0.03 C-34.85 -5.84, -174.79 -29.67, -210.04 -35.79 M-1.51 -1.09 C-36.3 -7.2, -175.31 -32.02, -210.49 -37.8" stroke="#4dabf7" stroke-width="4" fill="none"/></g><g transform="translate(392.0692859798298 165.62203939017854) rotate(0 -105.49999237060547 -17.99999237060547)"><path d="M-185.88 -42.24 C-190.98 -39.74, -195.59 -41.33, -210.49 -37.8 M-185.88 -42.24 C-191.06 -41.57, -198.68 -40.21, -210.49 -37.8" stroke="#4dabf7" stroke-width="4" fill="none"/></g><g transform="translate(392.0692859798298 165.62203939017854) rotate(0 -105.49999237060547 -17.99999237060547)"><path d="M-188.79 -25.38 C-193.16 -26.32, -197.18 -31.34, -210.49 -37.8 M-188.79 -25.38 C-193.11 -28.77, -200.03 -31.44, -210.49 -37.8" stroke="#4dabf7" stroke-width="4" fill="none"/></g></g><mask/><g transform="translate(252.81142651930384 58.10917640812977) rotate(10.140547604308779 55.406473496380954 41.3461905259353)"><text x="0" y="58.28159016535824" font-family="Excalifont, Xiaolai, Segoe UI Emoji" font-size="66.1539048414963px" fill="#4dabf7" text-anchor="start" style="white-space: pre;" direction="ltr" dominant-baseline="alphabetic">x-y</text></g><g stroke-linecap="round"><g transform="translate(264.52302534911263 62.85173581892104) rotate(0 50.28573172433033 11.809532528831824)"><path d="M-0.28 -0.46 C16.48 3.4, 84.06 18.49, 100.73 22.57 M1.78 -1.74 C18.38 2.28, 83.12 19.62, 99.86 23.55" stroke="#4dabf7" stroke-width="4" fill="none"/></g></g><mask/><g stroke-linecap="round"><g transform="translate(49.66590574345787 251.8041109584301) rotate(0 22.4761962890625 0)"><path d="M0 -0.42 C7.61 -0.48, 38.06 -0.4, 45.47 -0.25 M-0.67 0.55 C6.93 0.56, 37.61 0.46, 45.31 0.32" stroke="#ffd43b" stroke-width="4" fill="none"/></g></g><mask/><g stroke-linecap="round"><g transform="translate(326.2373575663745 324.9469564755432) rotate(0 22.4761962890625 0)"><path d="M0.3 -0.32 C7.76 -0.37, 37.12 -0.14, 44.54 -0.11 M-0.21 0.71 C7.44 0.72, 38.12 0.58, 45.57 0.54" stroke="#ffd43b" stroke-width="4" fill="none"/></g></g><mask/><g transform="translate(507.36754454162366 195.77351389612704) rotate(0 162.14395141601562 22.5)"><text x="0" y="31.716" font-family="Excalifont, Xiaolai, Segoe UI Emoji" font-size="36px" fill="#1e1e1e" text-anchor="start" style="white-space: pre;" direction="ltr" dominant-baseline="alphabetic">vector "difference"</text></g><g stroke-linecap="round"><g transform="translate(692.2647789155603 181.3925630305007) rotate(0 -141.75457770121693 -31.329820913255617)"><path d="M0.7 -0.74 C-21.34 -7.35, -85.71 -30.4, -133.22 -40.65 C-180.74 -50.9, -259.55 -58.45, -284.41 -62.23 M-0.4 1.48 C-21.96 -4.89, -83.95 -28.45, -130.89 -39.42 C-177.82 -50.39, -256.27 -60.49, -281.99 -64.35" stroke="#1e1e1e" stroke-width="4" fill="none"/></g><g transform="translate(692.2647789155603 181.3925630305007) rotate(0 -141.75457770121693 -31.329820913255617)"><path d="M-257.52 -69.49 C-264.17 -69.41, -269.27 -68.6, -281.99 -64.35 M-257.52 -69.49 C-265.09 -68.79, -274.38 -65.83, -281.99 -64.35" stroke="#1e1e1e" stroke-width="4" fill="none"/></g><g transform="translate(692.2647789155603 181.3925630305007) rotate(0 -141.75457770121693 -31.329820913255617)"><path d="M-259.94 -52.56 C-265.91 -56.21, -270.49 -59.1, -281.99 -64.35 M-259.94 -52.56 C-266.86 -57.53, -275.34 -60.25, -281.99 -64.35" stroke="#1e1e1e" stroke-width="4" fill="none"/></g></g><mask/></svg>

Since norms are always **non-negative**, we know:

$$
f(\lambda) \geq 0 \quad \text{for all real } \lambda
$$

---

### Step 2: Expand the Norm

Using the definition of the dot product and norm:

So, basically:

$$
\|\mathbf{x}\|^2 = (\sqrt{x_1^2 + x_2^2 + \dots + x_n^2})^2 = x_1^2 + x_2^2 + \dots + x_n^2 = \mathbf{x} \cdot \mathbf{x}
$$

Similarly, we can say:

$$
f(\lambda) = (\mathbf{x} - \lambda \mathbf{y}) \cdot (\mathbf{x} - \lambda \mathbf{y})
$$

Expand the dot product:

$$
f(\lambda) = \mathbf{x} \cdot \mathbf{x} - 2\lambda(\mathbf{x} \cdot \mathbf{y}) + \lambda^2(\mathbf{y} \cdot \mathbf{y})
$$

---

### Step 3: Rewrite in a Quadratic Form

Let’s set it up as a quadratic expression in terms of $\lambda$:

$$
f(\lambda) = \|\mathbf{x}\|^2 - 2\lambda(\mathbf{x} \cdot \mathbf{y}) + \lambda^2 \|\mathbf{y}\|^2
$$

---

### Step 4: Analyze the Quadratic Inequality

Since $f(\lambda) \geq 0$ for all $\lambda$, the quadratic equation:

$$
\lambda^2 \|\mathbf{y}\|^2 - 2\lambda(\mathbf{x} \cdot \mathbf{y}) + \|\mathbf{x}\|^2 \geq 0
$$

must have no real roots or a non-positive discriminant. The discriminant ($\Delta$) for a quadratic $a\lambda^2 + b\lambda + c$ is:

$$
\Delta = b^2 - 4ac
$$

Here:

- $a = \|\mathbf{y}\|^2$
- $b = -2(\mathbf{x} \cdot \mathbf{y})$
- $c = \|\mathbf{x}\|^2$

---

### Step 5: Set the Discriminant Condition

Since $f(\lambda) \geq 0$, the discriminant must be less than or equal to zero:

$$
\Delta = (-2(\mathbf{x} \cdot \mathbf{y}))^2 - 4(\|\mathbf{y}\|^2)(\|\mathbf{x}\|^2) \leq 0
$$

---

### Step 6: Simplify the Discriminant

$$
4(\mathbf{x} \cdot \mathbf{y})^2 - 4\|\mathbf{x}\|^2 \|\mathbf{y}\|^2 \leq 0
$$

Divide both sides by 4 and a little rearrangement gives:

$$
(\mathbf{x} \cdot \mathbf{y})^2 \leq \|\mathbf{x}\|^2 \|\mathbf{y}\|^2
$$

---

### Step 7: Take the Square Root

Finally, taking the square root of both sides:

$$
| \mathbf{x} \cdot \mathbf{y} | \leq \|\mathbf{x}\| \|\mathbf{y}\|
$$

And there you have it  —  Cauchy – Schwarz <strong><span style="color: var(--color-green);">proven</span></strong>!

---

## Useful Links

- [Dot products and duality | 3Blue1Brown](https://www.youtube.com/watch?v=LyGKycYT2v0&t=621s&pp=ygUVdmVjdG9yIG11bHRpcGxpY2F0aW9u)

...

> [!quote] Links to notes, where the Cauchy – Schwarz inequality is used:
> [[02 - KSE/2_5-term/Methods of Optimization/02. Convex Sets#The Cauchy – Schwarz Inequality\|02. Convex Sets#The Cauchy – Schwarz Inequality]]
> ...
