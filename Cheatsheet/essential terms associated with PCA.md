# Essential terms associated with PCA

## 1. Principal Component (PC) 📐

<img width="2240" height="1262" alt="image" src="https://github.com/user-attachments/assets/0c251af4-4df9-4e94-8b78-2af36a7ef4c9" />


The Principal Component (PC) is the core concept of PCA, representing a new coordinate axis that captures the maximum possible variance (information) from your original data.

### Principal Component Explained
A Principal Component is a straight line (or a hyper-plane in higher dimensions) that is fit to the data, ensuring that:

* It is the direction along which the data varies the most (maximum variance).
* It is orthogonal (perpendicular) to all other Principal Components.
* In simpler terms, PCA rotates the original coordinate system (e.g., the X and Y axes) to find a better, more informative set of axes.

|PC Property	|Description|
|--------|---|
|PC 1 (First Principal Component)|	The axis that captures the largest amount of variance in the dataset. This is the most important new dimension.|
|PC 2 (Second Principal Component)|	The axis that captures the second-largest amount of variance, while being uncorrelated (perpendicular) to PC 1.|

### Detailed Example with Student Activity Data
Imagine you have student data with two features: X (Time spent watching TV Shows) and Y (Time spent playing Video Games). Since most students who watch a lot of TV also play a lot of games, these two original features are highly correlated.

#### 1. The Original Axes (X and Y)
If you measure the variance along the original X-axis and Y-axis, you capture some spread, but much of the true spread of the data is diagonal.

#### 2. The New Axes (PC 1 and PC 2) 📐
PCA finds two new axes, PC 1 and PC 2, through the data:

* PC 1 (Axis of Maximum Variance): This component runs along the main diagonal, where the data is most spread out.
   * Interpretation: PC 1 represents the combined concept of "Overall Screen Time" or "Student Laziness." It captures the majority of the variation in the dataset. If we were to perform dimensionality reduction, we would choose to keep PC 1.
* PC 2 (Axis of Residual Variance): This component is perpendicular to PC 1. It captures the small amount of variation remaining after PC 1 has accounted for the majority of the spread.
   * Interpretation: PC 2 might capture a very small, remaining difference, such as "Preference for TV over Games," which is a small variation relative to the overall screen time.

Dimensionality Reduction
By projecting the 2-dimensional data (X, Y) onto the 1-dimensional PC 1, we lose very little information (variance) while effectively compressing the data from two features into one, solving the correlation and the curse of dimensionality.

## 2. Eigenvector (x) and Eigenvalue (λ) in PCA 📊

<img width="1184" height="530" alt="image" src="https://github.com/user-attachments/assets/c1e8f6ff-3fee-49ab-8fb0-977974ec1a9e" />

Definition and Core Relationship
Eigenvectors and Eigenvalues are special properties of a square matrix, which in PCA is the Covariance Matrix of your data. Their relationship is defined by the equation:

A x = λ x

Where:

* A is the Covariance Matrix of the dataset (a square matrix).
* x is the Eigenvector.
* λ is the Eigenvalue.

The equation means that when the Covariance Matrix (A) acts upon a special vector (x), the result is simply a scaled version of that same vector, without changing its direction.

### Eigenvector (Principal Direction) 🧭
* Definition: The Eigenvectors of the covariance matrix are the Principal Components (PCs). They are the directions (axes) in the data that capture the maximum amount of variance.
* Role in PCA: They define the orientation of the new coordinate system. In the example of student TV time and video game time, the first eigenvector (PC 1) is the specific diagonal line along which the data is most spread out.

### Eigenvalue (Magnitude of Variance) 🔢
* Definition: The Eigenvalues are the numerical magnitudes associated with each eigenvector.
* Role in PCA: They represent the amount of variance (or information) that the corresponding Principal Component captures. A larger eigenvalue means that the eigenvector is a more important component for describing the data.

### Why are they Required for PCA?
Eigenvectors and Eigenvalues are the only way to mathematically determine the optimal new axes for dimensionality reduction:

1. Finding Maximum Variance :
   * PCA's goal is to maximize variance, and mathematically, the eigenvectors of the covariance matrix point exactly along the directions of maximum variance. By calculating them, we automatically find the best possible new axes (PC1, PC2, etc.).

2. Ordering and Selection : 
  * The calculated eigenvalues allow us to rank the Principal Components:
  * The eigenvector with the largest eigenvalue is always PC 1 (the most informative component).
  * The eigenvector with the second-largest eigenvalue is PC 2, and so on.
  * This ranking allows for dimensionality reduction. You can decide to keep, for example, only the PCs whose corresponding eigenvalues sum up to 95% of the total variance, effectively discarding the least important (smallest eigenvalue) dimensions.

### Example Analogy: Finding the Longest Spread
Imagine your data is an oval-shaped cloud of points.

* Covariance Matrix (A): This matrix describes how the data is scattered, including its shape and orientation.
* Eigenvector (PC): This is the long axis of the oval. It shows the direction in which the data is most stretched—the direction of maximum variance.
* Eigenvalue (λ): This is the length of the long axis. It quantifies exactly how much variance exists along that direction.

If the first eigenvalue is 100 and the second is 5, you know the first Principal Component (PC 1) contains far more information than the second (PC 2), justifying the reduction from 2 dimensions to 1.

## 3. Explained Variance (Information Retention) 💡

<img width="1038" height="833" alt="image" src="https://github.com/user-attachments/assets/6e1f09a7-2413-4425-a8ef-ba845db68611" />

Explained Variance in Principal Component Analysis (PCA) is the measure of how much of the total information (variability) in the original dataset is retained by a specific Principal Component (PC) or a selected group of PCs. It is the key metric used to determine how 
effective the dimensionality reduction is and to select the optimal number of components to keep.

### Explained Variance vs. Explained Variance Ratio
PCA produces two closely related variance measures for each component:

|Term|	Definition|	Calculation|	Role in PCA|
|--------|---|---|---|
|Explained Variance|	The absolute amount of variance (equal to the eigenvalue) captured by a Principal Component.|	Equal to the λ (eigenvalue) of the component.|	Useful for comparing variance between components.|
|Explained Variance Ratio|	The proportion (percentage) of the total variance in the dataset captured by a Principal Component.|	Ratio = (Sum of all Eigenvalues / Eigenvalue of PC)| Most common metric for selecting components.|


Example: Deciding How Many Components to Keep
Imagine you have a dataset with 100 features and perform PCA to extract all 100 Principal Components.

1. Individual Explained Variance Ratio:

    * PC1: Explains 50% of the total variance (λ1 /∑λi = 0.50).
    * PC2: Explains 20% of the total variance (λ2 /∑λi = 0.20).
    * PC3: Explains 10% of the total variance (λ3 /∑λi =0.10).
    
    ...and so on for the remaining 97 components.

2. Cumulative Explained Variance Ratio (Information Retention): This is the running sum of the individual ratios.

|Number of Components (k)|	Individual Ratio|	Cumulative Explained Variance|	Information Retention|
|--------|---|---|---|
|1 (PC1)|	50%|	50%|	The PC 1 alone retains half the information.|
|2 (PC1 + PC2)|	20%|	70%	|The first two PCs retain 70% of the information.|
|3 (PC1 + PC2 + PC3)|	10%|	80%	|The first three PCs retain 80% of the information.|

3. The Decision Point
* Using this metric, you can set a target threshold for information retention (e.g., 90% or 95%). If your goal is to retain at least 80% of the original information, you would only need to keep 3 Principal Components instead of the original 100 features. This achieves
   a massive dimensionality reduction while minimizing the loss of data variability.


## 4. Scree Plot 📊

<img width="1038" height="833" alt="image" src="https://github.com/user-attachments/assets/6e1f09a7-2413-4425-a8ef-ba845db68611" />

* Definition: A line plot that graphs the eigenvalues (or the explained variance) of the Principal Components in descending order against the index number of the principal component.
* Role in PCA: It is a visual tool used to determine the optimal number of components to retain. Users look for the "elbow point" on the plot—the point after which the line flattens out—as subsequent components contribute very little additional explained variance.
