---
title: Unsupervised Learning
Date Created: 2024-11-12
Last Updated: 2025-09-28
tags:
  - CS2109S
  - ML
---
# What is Unsupervised Learning
---
In [[Introduction to Machine Learning & Decision Trees#Types of Feedback|supervised]] learning essentially we have <span style='color:var(--mk-color-orange)'>3 high level components</span> in model training, **data, model, loss** and our <span style='color:var(--mk-color-yellow)'>data will have the response variable</span>.

In <span style='color:var(--mk-color-turquoise)'>unsupervised learning</span> however, our data will <span style='color:var(--mk-color-yellow)'>not have the response variable</span>. This forces the model to **learn from itself**, through:
1) **Clustering** - Find clusters in data
2) **Dimensionality reduction** - Find lower-dimensional representation of the data (*2D to 1D and there is a segregation*)

This **happens quite often** since obtaining response variable data can be <span style='color:var(--mk-color-red)'>very expensive</span>.
# K-means Clustering
---
It is a technique of <span style='color:var(--mk-color-yellow)'>grouping data points into different groups</span>. Each group will be represented by 1 <span style='color:var(--mk-color-turquoise)'>centroid</span>, which is a **point in the middle of the cluster**.

This <span style='color:var(--mk-color-turquoise)'>centroid</span> is essentially an <span style='color:var(--mk-color-yellow)'>aggregated sum</span> of all the vectors (*data points*) and thus is **also a vector**.
$$
\mu_{c} = \frac{1}{m_{c}} \sum^{m_{c}}_{i = 1} x^{(i)}
$$
**Where:**
- $\mu_{c}$ is centroid $c$, which is a vector
- $m_{c}$ is the number of datapoints in cluster $c$
- $x^{(i)}$ is the data point or the vector assigned to cluster $c$
## Algorithm

The <span style='color:var(--mk-color-orange)'>algorithm</span> goes as such:
1) Initialize $K$ numbers of  **random** centroids ($\mu_{i} \dots \mu_{k}$)
2) **Repeat** the following **until convergence**
	- For $i = [1, n]$, **assign each datapoint to a centroid** $c^{(i)}$ <span style='color:var(--mk-color-yellow)'>based on distance</span> (*or other means*)
	- For $k = [1, K]$, <span style='color:var(--mk-color-yellow)'>calculate the new centroid</span> based on **all the assigned datapoints to cluster** $k$

If there is a **tie**, then just pick the <span style='color:var(--mk-color-yellow)'>same cluster as the previous one</span> or the <span style='color:var(--mk-color-yellow)'>cluster that results in a lower loss</span>.

> [!question] How do we know if its converges or not?
> We can <span style='color:var(--mk-color-yellow)'>define a loss function</span>, which will act as an indicator, if the <span style='color:var(--mk-color-yellow)'>loss value does not decreases after certain number of iterations</span> we can **safely stop**.
> 
> This is because **if it oscilates, or does not change** means that the <span style='color:var(--mk-color-green)'>centroids are in the best possible location</span> (*maybe local optima*).
> 
> Another good thing about the algorithm is that it <span style='color:var(--mk-color-green)'>never increases the loss function</span>.

There is <span style='color:var(--mk-color-orange)'>another variant of this algorithm</span>. Instead of computing the weighted sum of each cluster to find the new centroid, we can just <span style='color:var(--mk-color-yellow)'>snap the centroid to one of the closest datapoints</span> (*the original data point remains*).
## Measuring Goodness

It is possible that because of the **random initialisation of the clusters** we might<span style='color:var(--mk-color-red)'> not get the ideal centroids</span> (*local optima*).

**Example:**
![[K-means Clustering Local Optima.png|center]]

But in general we want to have a **lower** <span style='color:var(--mk-color-turquoise)'>distortion</span> and this will be our<span style='color:var(--mk-color-yellow)'> loss function</span> for <span style='color:var(--mk-color-teal)'>K-means clustering</span>.
$$
\text{Distortion} = J(c^{(1)}, \dots,c^{(m)}, \mu_{1},\dots,\mu_{k}) = \frac{1}{m}\sum\limits^{m}_{i = 1} \Vert x^{(i)} - \mu_{c^{i}} \Vert^{2}
$$
Here we are just <span style='color:var(--mk-color-green)'>minimising the weighted sum</span> of the <span style='color:var(--mk-color-yellow)'>distance of all datapoints to their assigned clusters</span>.
## Picking the Best Number of Clusters

So, what is the best number of clusters, 1, 10, 1000? Well we **cannot be sure without actually trying them**. Thus 1 method to **find the best number is through** the <span style='color:var(--mk-color-turquoise)'>elbow method</span>.

Essentially we will do a <span style='color:var(--mk-color-teal)'>iterated k-means clustering</span> from 1 to $n$. Then if we plot the loss on a graph, we will find a point (*called the elbow*) that <span style='color:var(--mk-color-yellow)'>after increasing</span> $k$ it <span style='color:var(--mk-color-yellow)'>will not decrease the loss as much</span>.
# Hierarchical Clustering
---
In the event we <span style='color:var(--mk-color-red)'>cannot decide on a fixed number of clusters</span>, we can <span style='color:var(--mk-color-yellow)'>find a hierarchy of clusters instead</span>.

Here are some <span style='color:var(--mk-color-orange)'>applications</span> of <span style='color:var(--mk-color-turquoise)'>hierarchical clustering</span>:
- **Customer segmentation**
- **Gene expression analysis**
- **Recommender systems**
- **Social network analysis**

The <span style='color:var(--mk-color-orange)'>algorithm</span> is very simple:
1) Start off by making <span style='color:var(--mk-color-yellow)'>every data point a cluster</span>
2) Then **repeat the following until all points are in 1 cluster**
	- **Find a pair of clusters** that are <span style='color:var(--mk-color-yellow)'>nearest to each other</span>
	- <span style='color:var(--mk-color-yellow)'>Merge the 2</span> clusters together into 1

**Visualisation of the result of the algorithm**
![[Example of Hierarchical Clustering.png|center]]
><span style='color:var(--mk-color-charcoal)'>Note that the data above is for 1D, for 2D data we will use circles like in k-means clustering</span>

> [!question] With no centroid how to calculate the distance between clusters?
> There are many ways to do this, **look at the list below**.
> 
> ![[Ways to Calculate the Distance Between Clusters.png|center|450]]
> 
> Or you can use the <span style='color:var(--mk-color-purple)'>euclidian or manhatten distance</span> it will work as well.
> 
> Note that for **complete linkage** is not the furthest distance, but the <b><mark style='background:var(--mk-color-yellow)'>shortest of all furthest distance</mark></b>.

But this method of clustering has its own issues, one down side to is that it needs <span style='color:var(--mk-color-red)'>high space and time complexity</span> to **compute the distances and do the merging**, <span style='color:var(--mk-color-yellow)'>impractical for large datasets or high dimension data</span>.
# Dimensionality Reduction
---
With high-dimension, the <span style='color:var(--mk-color-red)'>number of features will increase exponentially</span>, this is known as the <span style='color:var(--mk-color-turquoise)'>curse of dimensionality</span>.

The **idea** behind this is to <span style='color:var(--mk-color-yellow)'>remove non-important components</span> (*dimensions*). This will deuce the dimension and **to reconstruct the original dimension**, we can just <span style='color:var(--mk-color-yellow)'>take the average of the feature that was removed</span> and add it back to <b><mark style='background:var(--mk-color-yellow)'>get a close approximate</mark></b>.
## Singular Value Decomposition

[[Diagonalisation#Single Value Decomposition|SVD]] is an equation that can **represent** <b><mark style='background:var(--mk-color-yellow)'>any matrix</mark></b> in the following form:
$$
X = U\Sigma V^{T}
$$
**Where:**
- $U$ is some **n by m matrix** and has <span style='color:var(--mk-color-yellow)'>m orthonormal columns</span> (*left singular vectors or new basis*)
- $\Sigma$ is a **m by m diagonal matrix** with the diagonals $\sigma_{j} \ge 0$ (*singular values or basis importance*)
- $V$ is a m by m matrix and has <span style='color:var(--mk-color-yellow)'>m orthonormal columns and rows</span> (*right singular vector or combiner*)

Take note that we should order the singular values ($\sigma_{j}$) in **decreasing order** (*top left to bottom right*), this is to <span style='color:var(--mk-color-yellow)'>associate the variables in order of importance</span> of the corresponding column in $U$.

> [!tldr] Intuition behind SVD
> The intuition of SVD is **defined by the following**, rotate $\times$ stretch $\times$ rotate.

> [!info] Preliminarie terms
> **Orthonormality**
> 
> This means that <span style='color:var(--mk-color-yellow)'>2 vectors are orthogonal</span>, thus $A \cdot B = 0$, however because its **orthonormal**, means that there is **1 additional property**, $A \cdot A = 1$.
> 
> **Orthonormal basis**
> It is a <span style='color:var(--mk-color-yellow)'>set of vectors that are orthogonal to one another</span>. In addition this <span style='color:var(--mk-color-yellow)'>set can express all other vectors in some bigger set</span> through a series of **linear combinations**.

**SVD Example:**
![[SVD Example.png|center]]

So how can we **reduce the number of dimensions with SVD**. The **matrix to focus on is the basis importance**. We can <span style='color:var(--mk-color-yellow)'>set the diagonals to be 0 after a certain point</span>, thus reducing the dimensions.

> [!example] Dimensionality Reduction via SVD
> ![[Dimensionality Reduction via SVD.png|center]]
> 
> If we only want to have a **dimension of 2**, then we can <span style='color:var(--mk-color-yellow)'>set the values of the diagonals</span> after $\sigma_{2}$ <span style='color:var(--mk-color-yellow)'>to be 0</span>.
> 
> The resulting matrix is the **“best” approximation** with new basis size of 𝑟 to the original matrix.

**Reduction and reconstruction using SVD**
![[Reduction & Reconstruction via SVD.png|center]]
## Principal Component Analysis

It is a **statistical application** of <span style='color:var(--mk-color-teal)'>SVD</span>, where it captures components that <span style='color:var(--mk-color-yellow)'>maximises the statistical variations of the data</span>.

> [!info] Preliminarie equations
> **Variance**
> $$
> Var(x) = \frac{\sum (x_{i} - \bar{X})^{2}}{n - 1}
> $$
> 
> **Covariance**
> $$
> Cov(x, y) = \frac{\sum (x_{i} - \bar{X})(y_{i} - \bar{Y})}{n - 1}
> $$
> 
> **Where:**
> - $\bar{X}$ is the mean of all $x$ (*variable*)
> - $\bar{Y}$ is the mean of $y$ (*response/predictor*) 

Steps to <span style='color:var(--mk-color-orange)'>carry out PCA</span>:
1) Calculate the mean ($\bar{x}$) of over all samples
2) Calculate $x - \bar{x}$ for all data samples ($X$) and this will be $\hat{X}$
3) Then the $Cov(X) = \frac{1}{m}\hat{X}\hat{X}^{T}$

>Note that by dividing by $m$ is will <span style='color:var(--mk-color-red)'>result in a biased covariance matrix</span> for an<span style='color:var(--mk-color-green)'> unbiased one</span> **divide by** $m - 1$ instead.

After getting the covariance matrix, we can **apply** [[#Singular Value Decomposition|SVD]] <span style='color:var(--mk-color-yellow)'>on this new covariance matrix</span>.

> [!info] 
> Lets say someone asked to retain at least 99% of the variance of the data, how can we ensure this in <span style='color:var(--mk-color-teal)'>PCA</span>?
> 
> Lets look at the diagonal vector $\Sigma$, we just need to ensure <span style='color:var(--mk-color-yellow)'>that the sum of</span> $r$ sigmas over the sum of all sigmas <span style='color:var(--mk-color-yellow)'>is not lower than 0.99</span>.
> 
> $$
> \frac{\sum^{r}_{i = 1} \sigma_{i}^{2}}{\sum^{m}_{i = 1} \sigma_{i}^{2}} \ge 0.99
> $$
> 
> Or <span style='color:var(--mk-color-orange)'>we can also show this as well</span>
> 
> ![[Another way of Retaining Variance.png|center]]

