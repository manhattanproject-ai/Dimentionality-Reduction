# Different types of Dimentionality Reduction Technique 

<img width="1388" height="728" alt="image" src="https://github.com/user-attachments/assets/5362a14e-3a6f-4a00-8525-6743a352145a" />

Dimensionality reduction techniques are broadly categorized into three types:

## 1. Linear Discriminative Reduction 📐
These methods use linear transformations to project the high-dimensional data onto a lower-dimensional subspace. The resulting dimensions are linear combinations of the original features.

|Technique|	Goal|	Type|
|--------|---|---|
|PCA (Principal Component Analysis)|	Finds the directions (principal components) that maximize the variance in the data.|	Linear|
|LDA (Linear Discriminant Analysis)|	Finds the feature subspace that maximizes the separation (discrimination) between classes.|	Linear|
|Factor Analysis|	Identifies the underlying unobserved, or 'latent,' variables (factors) that explain the pattern of correlations among the observed variables.|Linear|

## 2. Non-Linear Discriminative Reduction 🌀
These methods, often called Manifold Learning, are used when the data structure in the high-dimensional space is a non-linear "manifold."

|Technique|	Goal|	Type|
|--------|---|---|
|t-SNE (t-distributed Stochastic Neighbor Embedding)|	Primarily used for visualization; it reduces dimensions by ensuring points that are close in the high-dimensional space remain close in the low-dimensional space.|	Non-Linear|

## 3. Feature Selection ✂️
Unlike reduction methods that create new features, feature selection techniques simply choose a subset of the original features, discarding the rest.

Feature Selection methods are further divided into three sub-categories:

|Method|	Approach	|Example Techniques|
|--------|---|---|
|Filter Method|	Ranks features based on statistical scores (e.g., correlation or chi-square) and selects the highest-scoring ones, independent of the model.|	Chi-square test, ANOVA, Correlation Based Feature Selection|
|Wrapper Method|	Uses a specific machine learning model to evaluate subsets of features. It trains and tests the model with different combinations.|	Forward Selection, Backward Elimination, RFE (Recursive Feature Elimination)|
|Embedded Method|	Performs feature selection as part of the model training process itself.|	Regularization (Lasso, Ridge, ElasticNet), Tree Based Feature Importance |


We will explore two algorithms in this module , PCA and t-sne .
