# PCA vs. t-SNE Comparison

|Feature|	Principal Component Analysis (PCA)	|t-distributed Stochastic Neighbor Embedding (t-SNE)|
|--------|---|---|
|Method Type|	Linear dimensionality reduction.|	Non-linear dimensionality reduction.|
|Primary Objective|	Maximize Variance (preserve global structure and information content).|	Preserve Local Structure (make similar points nearby and dissimilar points far apart).|
|Use Case|	Feature Engineering (as a preprocessing step for modeling), noise reduction, and data compression.|	Visualization (creating 2D or 3D plots of high-dimensional data).|
|Preserves|	Global Variance and overall data spread.	|Local Neighborhoods and density-based clustering.|
|Output	|Principal Components that are uncorrelated (orthogonal).|	A 2D/3D map where clusters are clearly visible.|
|Interpretation	|The axes (PCs) are interpretable as linear combinations of original features.|	The axes are not interpretable; only the relative positioning of the points matters.|
|Distance Meaning|	Distances in the low-D space preserve variance (large global distances mean large differences).|	Distances between clusters are often meaningless; only the distance within a cluster is reliable.|
|Scalability|	Scales well to large datasets and high dimensions; deterministic.|	Slower and computationally intensive for large datasets; non-deterministic (results vary based on initialization).|

## When to Use Each Technique
* Use PCA when: Your primary goal is to compress data, speed up a machine learning model, or retain the overall spread (variance) of the data. It is a good first step before other methods.
* Use t-SNE when: Your primary goal is to visualize high-dimensional data, identify distinct clusters, or explore the fine-grained local relationships within the data.


