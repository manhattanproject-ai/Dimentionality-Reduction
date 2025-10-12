# Detailed Explanation of t-SNE

## Step 1: High-Dimensional Distance Calculation (Similarity)

<img width="1849" height="925" alt="image" src="https://github.com/user-attachments/assets/cb9f0913-d872-4172-8094-3aa5c99c39f4" />

* Objective: To quantify the similarity between every single pair of data points in the original, high-dimensional space.
* Process: The algorithm first calculates the distance between any pair of data points. This is typically done using the Euclidean distance (straight-line distance).
  For example, if point A and point B are close neighbors, their distance is small (e.g., 1.5).
  If point A and point X are far apart, their distance is large (e.g., 5.3).

* Result (High-Dimensional Probability, pij): These distances are then used to define a conditional probability (pj∣i), which is the probability that point i would choose point j as its neighbor if neighbors were picked according to a Gaussian distribution
  (a normal bell curve).
  * The final high-dimensional similarity pij is the joint probability, which measures the true affinity between points i and j.
  * A high probability score means the points are considered very similar and are likely neighbors in the high-dimensional space.

## Step 2: High-Dimensional Similarity (pij)
The objective of this step is to transform the calculated distances from Step 1 into a joint probability distribution that accurately reflects the data's local structure in the high-dimensional space.

<img width="1832" height="941" alt="image" src="https://github.com/user-attachments/assets/8d2a0b1c-97e9-4059-b220-1cc46e7c77d5" />

### The Core Idea: Gaussian Distribution and Probabilities

* Defining Conditional Probability (pj∣i): For every point i, t-SNE models the similarity to its neighbors using a Gaussian distribution (Normal Distribution) centered at i. This creates a conditional probability pj∣i , which is the probability that point i would select
   point j as its neighbor.
* Density Awareness: The Gaussian model makes t-SNE density-aware.
    * Dense Region (e.g., A & B): If two points (A and B) are very close in a dense area, their distance is small (e.g., 1.5), resulting in a high affinity/probability that they are neighbors.
    * Sparse Region (e.g., X & Z): If a point (Z) is in a sparse area, even a moderately distant point (Q) can be considered a neighbor because there are few other points nearby. Thus, the affinity between Z and Q can still be high despite a larger distance (e.g., 3.2).

### The Role of Perplexity
* The variance of the Gaussian distribution for each point is chosen such that the entropy (or uncertainty) of the conditional probability distribution equals a user-defined hyperparameter called Perplexity.
* Perplexity determines the effective number of neighbors each point considers. A larger perplexity forces the algorithm to consider a wider neighborhood (more global structure), while a smaller perplexity focuses only on immediate neighbors (more local structure).

### Final Similarity (pij)
The final high-dimensional similarity pij is the joint probability, which is derived from the conditional probabilities to ensure that pij = pji (similarity is symmetric). This pij matrix serves as the target distribution that the low-dimensional representation must match
during the optimization phase (Step 4).

## Step 3: Low-Dimensional Initialization 🎲

<img width="702" height="503" alt="image" src="https://github.com/user-attachments/assets/c5bd59b4-6808-4fc7-b189-2cdf580ae9d4" />

* Objective: To establish the initial arrangement for the data points in the target visualization space before the optimization process begins.
* Process: The data points are assigned random coordinates in the desired low-dimensional space.
  * For a 2D t-SNE plot (the most common for visualization), each point is given a random (x,y) coordinate.
  * For a 3D plot, each point is given a random (x,y,z) coordinate.
* Result: This random placement creates the starting configuration for the map. This initial arrangement will be iteratively adjusted in the next step (Optimization) to match the high-dimensional similarities (pij) calculated in the previous steps.

Essentially, this step simply sets up the board for the game; the real work of clustering and matching the high-dimensional structure happens next.

<img width="1890" height="913" alt="image" src="https://github.com/user-attachments/assets/a3c119ac-aa5a-4ff0-8478-eb49289f0938" />

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


## Dimentionality Reduction Visualization : Converting a 3D into 2D 

<img width="1868" height="937" alt="image" src="https://github.com/user-attachments/assets/c85a6383-0b5d-42c6-9173-d421547a645a" />

