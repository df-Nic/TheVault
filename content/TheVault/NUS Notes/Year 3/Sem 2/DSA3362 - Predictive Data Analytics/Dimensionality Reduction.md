---
Title: Dimensionality Reduction
Date Created: 20-March-2026
Last Updated: 20-March-2026
Tags:
  - DSA3362
  - AI/ML/DimensionalityReduction
---
# Why Dimensionality Reduction?
---
In unsupervised learning we are discovering interesting patterns or structure in unlabeled data, we can use clustering to group our data.

Another technique is <b><span style='color: #87CEEB'>dimensionality reduction</span></b> where the goal is to <b><span style='color: #FFD700'>convert a large number of variables into a smaller number while retaining as much information as possible</span></b>.

>[!abstract] Dimension
>When we talk about dimensions we are talking about <b><span style='color: #FFD700'>the number of variables</span></b>. 
>
> It also means that we can plot our variables in a n-dimension grid where n is the number of variables.
>
>>[!example] If we have only weight then our dataset if only 1 dimension. If we have weight and age then its 2 dimension and so on

So with **higher dimension** for information? Well that is not the case and there are some **downsides**:
1) <b><span style='color: var(--mk-color-red)'>Hard to visualise</span></b> high dimensional space
2) <b><span style='color: var(--mk-color-red)'>Computational cost</span></b> as models tend to work slower with higher dimensional dataset
3) <b><span style='color: var(--mk-color-red)'>Data sparsity</span></b>, more dimensions means data is more sparse (*more space between points*) thus less information gained

>[!danger] Curse of Dimensionality
>As dimensions increase, data becomes sparse, making it difficult to find patterns, causing distances between points to become nearly indistinguishable, and often leading to severe overfitting in machine learning models.

>[!success] How can dimensionality reduction help
>- Reduce high computational time
>- Mitigate data sparsity
>- Allow for effective data visualisation
>- Facilitate subsequent data analysis, such as clustering, regression

There are **2 common techniques** used:
- [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Principle Component Analysis.md|Principle component analysis]] (*PCA*)
- Factor analysis (*FA*)
