# Detailed Explanation of PCA

## Step 1 - Data Normalization (Centering the Data)

<img width="1046" height="546" alt="image" src="https://github.com/user-attachments/assets/d3af93f1-1aa2-4a1d-96b4-838eb21a943c" />

* Objective: The primary goal of this step is to center the data around the origin (0, 0). This is a crucial preprocessing step for PCA.
* Process: This step involves finding the center of the data. This is typically accomplished by standardizing (or centering) the data, which means calculating the mean of each feature (column) and then subtracting that mean from every data point in that feature.
* Importance: Centering the data ensures that the first principal component (PC1) correctly captures the direction of maximum variance, rather than merely the mean of the data. It ensures that all features start on an equal footing, preventing features with larger initial values from dominating the variance calculation.
* Result: The entire dataset is shifted so that the average (mean) of each variable is zero.

## Step 2 - Find the First Principal Component (PC1)
The objective of this step is to identify the new axis (line) that captures the maximum amount of spread, or variation, in the data. This direction is called the First Principal Component (PC1).

<img width="1852" height="1020" alt="image" src="https://github.com/user-attachments/assets/40e8e704-2f72-4ea7-92f2-7e9d53ce50f7" />

### The Search for Maximum Variance 📈

Trial Line Projection and Spread Calculation
The core mechanism for finding the First Principal Component (PC1) is an iterative search for the line (axis) that maximizes the variance of the projected data.

#### 1. The Trial Line and Projection
* Start with a Trial Line: The process begins with a line passing through the center of the normalized data (the origin). The algorithm starts with a random line and begins rotating it.
* Projection: For a given orientation of the line, every data point is projected onto it at a 90 degree angle (orthogonally). The original data points (dark gray) are now represented by their projections (lighter gray) lying directly on the trial line.

#### 2. Calculation of Spread (Variance)
* The spread of the projected points along the trial line is calculated to quantify the amount of variance captured by that particular line orientation.
* Distance to Center: For each projected point, the algorithm measures the distance (di) from that point back to the center of the data (the origin).

Sum of Squared Distances: The variance is calculated as the sum of the squared distances from all projected points to the center. Squaring the distances ensures that points far from the center contribute more heavily to the total variance, thus rewarding lines that
capture a wide spread of data.

$$\text{Spread} = d_1^2 + d_2^2 + d_3^2 + \cdots + d_n^2$$
​
#### Optimization: The algorithm iteratively adjusts the line's orientation to find the maximum possible sum of squared distances (maximum variance).
* For a poor trial line, the sum of squared distances (variance) is low (e.g., 4.8).
* As the line rotates to align better with the data's inherent spread, the sum of squared distances increases (e.g., to 9.4, then to 12.2).

## Step 3 - Find Subsequent Principal Components (PC2, PC3, etc.)
Once the First Principal Component (PC1) is found (the axis of maximum variance), the algorithm proceeds to find the remaining components, ensuring they are independent of the ones already found.

<img width="1157" height="628" alt="image" src="https://github.com/user-attachments/assets/7826e67f-944a-4c3a-a3aa-0bee89070d5b" />

###  The Orthogonality Constraint 📐
* Objective: To find new axes that capture the largest remaining variance in the data while being uncorrelated with all previously found components.
* Process: The Second Principal Component (PC2) is the line that captures the most variance in the data remaining after PC1 has accounted for its share.
* Key Rule: Crucially, PC2 must be orthogonal (perpendicular, at a 90 degrees angle) to PC1. This orthogonality constraint is what guarantees the independence (uncorrelated nature) of the principal components.
    * In a 2D plot, this is simply a line perpendicular to PC1, passing through the origin.
    * In higher dimensions, each new PC must be orthogonal to all preceding ones.

### Identifying the PC2 Direction
* Maximizing Remaining Variance: Among all lines perpendicular to PC1, the algorithm mathematically searches for the one onto which the data, when projected, exhibits the greatest spread.
* Eigen-decomposition: Similar to PC1, the direction of PC2 is given by the eigenvector corresponding to the second largest eigenvalue of the covariance matrix. The magnitude of the eigenvalue represents the amount of variance captured by PC2.


## Step 4 - Calculate All Principal Components
* This process is repeated to find PC3, PC4, and so on.
* Each subsequent Principal Component is found by maximizing the variance in the remaining dimensions, subject to the constraint that it must be orthogonal to all previously found PCs.
* The final result is a complete set of Principal Components, where the variance captured by each component decreases successively (Variance of PC1 ≥ Variance of PC2 ≥ Variance of PC3...).

The total number of Principal Components (PCs) that can be calculated in PCA is always equal to the number of original features (columns) or dimensions in the dataset. For example, if your original dataset has 10 columns, the PCA algorithm will calculate up to 10 
Principal Components (PC1, PC2, ..., PC10).

## Step 5: Dimensionality Reduction 📉
The objective of Dimensionality Reduction is to represent the original dataset with a smaller number of features (Principal Components) while minimizing the loss of important information (variance).

### The Process: Selecting the Components
* Review the Calculated Components: After finding all n principal components (PC1, PC2, ..., PCn, where n is the number of original features), the algorithm has a new, transformed dataset. The components are ordered by the amount of variance they capture, with PC1 having the most.
* Determine the Cut-off: This step involves deciding how many of the top components to keep and how many to discard. The discarded components are the ones that explain the least variance, which effectively reduces the dataset's dimensionality.

<img width="1006" height="804" alt="image" src="https://github.com/user-attachments/assets/0b85b318-a879-4fa5-b45e-a339b8a2b0cc" />


### Methods for Selecting Components
Data scientists use two primary methods to determine the optimal number of components (k):

#### 1. The Cumulative Explained Variance Threshold
This is the most common and objective method.

* Goal: Choose the minimum number of components (k) that retain a pre-defined, high percentage of the total variance (e.g., 90%, 95%).
* How it Works: You look at the Cumulative Explained Variance Plot (Scree Plot).
  * For example, if you require 85% of the variance:
    * PC1 to PC3 capture 74%.
    * PC1 to PC4 capture 87%.
* Since 4 components is the minimum needed to cross the 85% threshold, you would choose 4 components (k=4).

#### 2. The Elbow Rule (Scree Plot)
This method is more subjective and visual.

* Goal: Retain all components up to the "elbow"—the point where the marginal gain in variance explained by an additional component drops significantly.
* How it Works: You look at the Individual Component Variance (the bars on a scree plot). The elbow typically occurs where the bars transition from a steep drop to a relatively flat line. Components after the elbow are considered less informative noise.

#### The Final Result
By selecting k components (e.g., k=4) and discarding the rest, the original n-dimensional data is projected onto the k new principal axes. The resulting dataset has fewer columns (k≪n) but still retains the vast majority of the original data's structure and information,
achieving effective dimensionality reduction.


## Visual Explanation of Dimentional Reduction 

<img width="1213" height="632" alt="image" src="https://github.com/user-attachments/assets/3041c107-4aff-4592-904f-d6a0e8bc9a8b" />

The  illustrates above explains the successful outcome of Dimensionality Reduction using Principal Component Analysis (PCA).

* Left (Original Data): The data points are shown in a 2-dimensional space (columns/dimensions: x and y).
* Right (Reduced Data): The data has been transformed and projected onto a single axis, resulting in a 1-dimensional space (one column/dimension, which would be PC1).
* Conclusion: By using PCA, the number of dimensions (columns) in the data was reduced (from 2D to 1D) while losing as little information as possible, as the relative separation and grouping of the data points are largely maintained.

