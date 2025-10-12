# How t-SNE works ?

While PCA is a linear method focused on preserving variance, t-SNE is a non-linear method primarily focused on preserving the local structure of the data, making it excellent for visualization.

Here are the five key steps and objectives of the t-SNE algorithm:

## Step 1. High-Dimensional Distance Calculation (Similarity) 🌐

* Objective: To determine how similar every data point is to every other data point in the original high-dimensional space.
* Process: The algorithm first calculates the Euclidean distance (or other distance metrics) between all pairs of data points.
* Result: A distance matrix that forms the basis for defining high-dimensional similarity (pij).

## Step 2. High-Dimensional Similarity (pij) 🌐

* Objective: To convert the high-dimensional distances into a probability distribution that represents how likely each point is a neighbor of another.
* Process: The calculated distances are converted into a probability/affinity score. It uses a Gaussian distribution centered at each data point. A high score (pij) means the two points are likely neighbors.
* Perplexity: A critical hyperparameter here is Perplexity, which relates to the effective number of neighbors each point considers. It is crucial for balancing the focus on local and global aspects of the data.

## Step 3. Low-Dimensional Initialization 🌐

* Objective: To create a canvas where the high-dimensional data will be mapped, usually for visualization.
* Process: Before the actual mapping begins, the data points are randomly placed (initialized) into the desired low-dimensional space (typically 2D or 3D). This random starting arrangement is the starting point for the optimization process.

## Step 4. Iterative Optimization (Minimizing the Kullback-Leibler Divergence) 🌐

* Objective: To move the low-dimensional points iteratively so that their similarity distribution matches the high-dimensional similarity distribution as closely as possible. This is the core of the algorithm.
* Process:
  * Low-Dimensional Similarity (qij): In the low-dimensional space, the algorithm calculates a new similarity score (qij) between points using a Student's t-distribution (hence the 't' in t-SNE).
  * Optimization: The algorithm uses an optimization technique (like gradient descent) to minimize the Kullback-Leibler (KL) Divergence between the high-dimensional probabilities (pij) and the low-dimensional probabilities (qij).
  * Result: Points that were close neighbors in the high-dimensional space are moved closer together in the low-dimensional map.

## Step 5. Convergence 🌐

* Objective: To finalize the low-dimensional representation once the points stop moving significantly.
* Process: The optimization stops when the positions of the data points in the low-dimensional space have stabilized and no longer change significantly with each iteration.
* Result: The final t-SNE plot, which is an optimized 2D or 3D map where distinct clusters of data from the high-dimensional space are visually separated.
