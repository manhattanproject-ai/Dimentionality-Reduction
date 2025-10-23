# When to Choose PCA for Visualization ?

PCA,by its very nature,is a dimensionality reduction technique. Yet, at times, many use PCA for visualizing high-dimensional datasets.This is done byprojecting the given data into two dimensions and visualizing it.

<img width="945" height="325" alt="image" src="https://github.com/user-attachments/assets/43f2ad8d-4707-4d77-a15d-6c6a38101e11" />

## Why PCA is Sub-Optimal for Visualization

### 1. It Preserves Variance, Not Separation
* PCA is a linear dimensionality reduction technique whose sole objective is to find a set of orthogonal axes (Principal Components) that maximize the variance of the data.
* Goal: Maximize the spread (variance) of the data onto the lower dimension.
* Problem for Visualization: Maximizing variance does not guarantee that clusters of data (different classes or groups) will be pushed far apart. If two clusters are close in the original high-dimensional space, PCA will try to keep them close if that direction maximizes variance.

### 2. Information Loss Can Distort Clusters
* As your document mentions, if you project a high-dimensional dataset onto only two or three dimensions for plotting, this visualization is only useful if the first few principal components capture most of the original data
variance.
* The Issue: If the variance is widely distributed across many dimensions (e.g., the first two components only capture 40% of the variance), the 2D plot will be highly misleading and incorrect. The true separation or
clustering that exists in the remaining 60% of the variance is completely lost in the visual representation.
* The Result: A plot that looks like a single, messy blob might actually contain several distinct, separable classes in the full-dimensional space.

## When is it not a good choice - explained visually 
For instance, in the plot below, the first two components only explain 55% of the original data variance.

<img width="1263" height="663" alt="image" src="https://github.com/user-attachments/assets/e81bcbc3-dbec-41b8-b3e6-779630358363" />

Thus, visualizing this dataset in 2D using PCA may not be a good choice because plenty of data variance is missing.

## When is it a good choice - explained visually 
In the below plot,the first two components explain 90% of the original data variance.

<img width="1258" height="629" alt="image" src="https://github.com/user-attachments/assets/ab2243e2-a3f7-4f8f-b65f-1a9a0bc9385a" />

## Summarization Why PCA is not good choice and t-SNE 
2D projections created by PCA donot consider local structure.Instead,its principalcomponents primarilyfocusonpreserving themaximumvariance.But t-SNEprojectionsprovide muchmoreclarityintodata clusters.The clusters produced
by t-SNE are well separated.But those in PCA have a significant overlap, and they hardly convey anything.

<img width="1206" height="1019" alt="image" src="https://github.com/user-attachments/assets/75054a41-85fd-4f84-89dd-ca662868193c" />
