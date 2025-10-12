# How PCA Works

The goal of Principal Component Analysis (PCA) is a linear dimensionality reduction technique that transforms the data into a new coordinate system such that the greatest variance by any projection lies on the first coordinate (the first Principal Component, or PC1), the second greatest variance on the second coordinate (PC2), and so on. This process minimizes the information loss while reducing the number of features.

The five key steps of the PCA algorithm are outlined below:

## Step 1. Data Normalization (Centering the Data) 🌐
* Objective: To ensure that all features (variables) contribute equally to the PCA and to make the origin the center of the data.
* Process: The first step involves finding the center of the data. This is typically done by standardizing (or centering) the data, which means subtracting the mean of each feature from all its data points.
* Result: The data is centered around the origin (0, 0).

## Step 2. Find the First Principal Component (PC1) 🌐
* Objective: To identify the new axis (direction) that captures the maximum amount of variance in the data.
* Process: The algorithm finds a line or vector onto which the data can be projected, such that the spread of the projected data points is maximized. This direction is the First Principal Component (PC1).
* Result: The PC1 direction, which corresponds to the eigenvector with the largest eigenvalue, holds the greatest amount of information (variance).

## Step 3. Find Subsequent Principal Components (PC2, PC3, etc.) 🌐
* Objective: To find new axes that capture the next largest amounts of variance from the remaining uncaptured data, ensuring they are independent of the previously found components.
* Process: After finding PC1, the algorithm finds the next best axis for capturing variance, which is the Second Principal Component (PC2).
* Constraint: PC2 is always orthogonal (perpendicular) to PC1. The process continues for PC3, PC4, and so on, with each new PC being orthogonal to all previous ones.

## Step 4. Calculate All Principal Components
* Objective: To obtain a full set of new, uncorrelated features that are ordered by their importance (how much variance they capture).
* Process: The algorithm repeats the process (steps 2 and 3) until it has found one principal component for every original dimension. These components are derived from the eigenvectors and their associated eigenvalues of the data's covariance matrix.
* Result: A set of new, wrapped-up features (the PCs) is created, ordered by the amount of variance (information) they retain.

## Step 5. Dimensionality Reduction
* Objective: To represent your data with a much smaller number of features while preserving the essential information.
* Process: This is the practical step where you choose a subset of the most important principal components (e.g., just PC1 and PC2) to represent your data. You discard the components that capture the least variance, effectively reducing the dimensionality of your dataset.
* Selection Method: This choice is often guided by the Explained Variance Plot (Scree Plot), where you select components until a desired level of cumulative variance is reached (e.g., 90% information retained).
