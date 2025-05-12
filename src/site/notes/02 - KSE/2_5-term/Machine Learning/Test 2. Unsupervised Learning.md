---
{"dg-publish":true,"permalink":"/02-kse/2-5-term/machine-learning/test-2-unsupervised-learning/","tags":["kse","ai","machine-learning"],"created":"2025-04-16T00:58:03.312+03:00","updated":"2025-04-16T01:05:26.994+03:00"}
---


# Test 2. Unsupervised Learning

---

$\textcolor{WildStrawberry}{\text{Question 1}}$

Explain Principal Component Analysis (PCA). What is the objective of PCA? Describe how you compute principal components and how you decide how many to keep. What are the limitations of PCA?

> [!success]+ Answer 1!  
> PCA seeks an orthogonal linear transformation that projects data onto directions of maximum variance.
>
> - **Objective**: find eigenvectors of the covariance matrix $Σ = \tfrac1n X^T X$ corresponding to the largest eigenvalues.
> - **Computation**:
>   1. Center the data.
>   2. Compute $Σ$.
>   3. Perform eigen‑decomposition or SVD: $Σ = VΛV^T$.
>   4. Principal components = columns of $V$; variances = diagonal entries of $Λ$.
> - **Choosing components**: use cumulative explained variance (e.g. keep top k s.t. ≥ 90% variance) or a scree plot (“elbow”).
> - **Limitations**:
>   - Captures only **linear** structure.
>   - Sensitive to outliers and scaling.
>   - Components may be hard to interpret.

---

$\textcolor{WildStrawberry}{\text{Question 2}}$

Explain Uniform Manifold Approximation and Projection (UMAP). How does UMAP differ from t‑SNE in approach and performance? What are its main parameters and advantages?

> [!success]+ Answer 2!  
> UMAP constructs a weighted k‑nearest‑neighbour graph in high‑D, builds a fuzzy simplicial set, and optimizes a low‑D embedding by minimizing cross‑entropy between high‑D and low‑D fuzzy sets.
>
> - **Differences from t‑SNE**:
>   - Preserves more **global** structure.
>   - Faster and scales better to large datasets.
>   - Embedding distances are more interpretable.
> - **Main parameters**:
>   - **n_neighbors** (local vs. global balance)
>   - **min_dist** (tightness of clusters)
>   - **metric** (distance function in high‑D)
> - **Advantages**:
>   - Speed and scalability
>   - Better global topology preservation
>   - Supports supervised and semi‑supervised extensions

---

$\textcolor{WildStrawberry}{\text{Question 3}}$

Describe t‑Distributed Stochastic Neighbor Embedding (t‑SNE). How does it model pairwise similarities in high and low dimensions? What are the key hyperparameters, and what pitfalls should you watch out for?

> [!success]+ Answer 3!  
> t‑SNE converts pairwise distances into conditional probabilities $p_{j|i}$ in high‑D (Gaussian kernel) and $q_{j|i}$ in low‑D (Student’s t‑kernel), then minimizes the KL divergence $KL(P\|Q)$.
>
> - **Key steps**:
>   1. Compute high‑D affinities $p_{ij}$.
>   2. Initialize low‑D points (random or PCA).
>   3. Use gradient descent to minimize $\sum p_{ij}\log\frac{p_{ij}}{q_{ij}}$.
> - **Hyperparameters**:
>   - **Perplexity** (controls effective neighborhood size)
>   - **Learning rate**
>   - **Number of iterations**
> - **Pitfalls**:
>   - Doesn’t preserve global structure
>   - Results vary with random seed and perplexity
>   - Computationally expensive on large datasets

---

$\textcolor{WildStrawberry}{\text{Question 4}}$

Describe the k‑means clustering algorithm. What objective does k‑means minimize? Outline the standard algorithm steps and discuss methods for choosing $k$. What are common failure modes?

> [!success]+ Answer 4!  
> k‑means minimizes the within‑cluster sum of squares:
>
> $$
> > \min_{C}\sum_{i=1}^k\sum_{x\in C_i}\|x - μ_i\|^2
> $$
>
> - **Algorithm**:
>   1. Initialize k centroids (random or k‑means++).
>   2. **Assign** each point to its nearest centroid.
>   3. **Update** centroids as cluster means.
>   4. Repeat until convergence.
> - **Choosing k**:
>   - **Elbow method** (plot SSE vs. k)
>   - **Silhouette score**
>   - Domain knowledge
> - **Failure modes**:
>   - Sensitive to initialization (use k‑means++)
>   - Assumes **spherical**, equally‑sized clusters
>   - Poor with **non‑convex** shapes or outliers

---

$\textcolor{WildStrawberry}{\text{Question 5}}$

Explain hierarchical clustering. Contrast agglomerative and divisive approaches. What linkage criteria exist, and how do they affect the resulting dendrogram? How do you decide where to cut the tree?

> [!success]+ Answer 5!
>
> - **Agglomerative**: start with each point as its own cluster, iteratively merge the closest pair.
> - **Divisive**: start with one cluster, recursively split.
> - **Linkage criteria**:
>   - **Single** (min distance) → chain effect, elongated clusters
>   - **Complete** (max distance) → compact clusters
>   - **Average** (mean distance) → compromise
>   - **Ward’s** (minimize variance) → spherical clusters
> - **Cutting the tree**:
>   - Choose a distance threshold
>   - Specify desired number of clusters
>   - Use inconsistency or silhouette analysis

---

$\textcolor{WildStrawberry}{\text{Question 6}}$

Describe DBSCAN. What are core, border, and noise points? How do the parameters $\varepsilon$ and min_samples influence clustering? When is DBSCAN preferred over k‑means?

> [!success]+ Answer 6!  
> DBSCAN groups points based on density:
>
> - **Core point**: ≥ min_samples within radius $\varepsilon$
> - **Border point**: < min_samples within $\varepsilon$ but in neighborhood of a core point
> - **Noise**: neither core nor border
> - **Parameters**:
>   - **$\varepsilon$** (neighborhood radius): too small → many noise points; too large → clusters merge
>   - **min_samples**: minimum density threshold; higher values → stricter cluster definition
> - **Preferred when**:
>   - Clusters are **arbitrary-shaped**
>   - You want to identify **noise/outliers**
>   - Data has varying cluster densities (with careful parameter tuning)
