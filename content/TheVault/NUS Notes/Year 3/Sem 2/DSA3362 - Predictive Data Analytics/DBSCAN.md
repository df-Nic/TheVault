---
Title: DBSCAN
Date Created: 17-March-2026
Last Updated: 01-April-2026
Tags:
  - DSA3362
  - AI/ML/Clustering/DBSCAN
---
# Why DBSCAN?
---
It is known as <b><span style='color: #87CEEB'>Density-Based Spatial Clustering of Applications with Noise</span></b>. It is a <b><span style='color: #FFD700'>desnsity based</span></b> clustering technique, where it forms clusters from <b><span style='color: #FFD700'>density reachable observations</span></b> which are closely packed together.

>[!question] Why do we need DBSCAN
>As [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Clustering.md#K-means|K-means]] & [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Hierarchical Clustering.md|hierarchical clustering]] are designed to <b><span style='color: #FFD700'>find spherical shaped clusters</span></b>. Thus they <b><span style='color: var(--mk-color-red)'>cannot find clusters of arbitrary shapes</span></b>.

It <b><span style='color: #FFD700'>separates regions of high density using regions of low density</span></b>.

>[!success] Unlike k-means & hierarchical clustering, DBSCAN can discover clusters of arbitrary shapes
>
>A workaround if you want to use k-means or hierarchical clustering is to set a higher K and use judgement to treat different clusters as 1.

>[!abstract] Density
>**Center-based density** of a point is the <b><span style='color: #FFD700'>number of points</span></b> (*including the center itself*) <b><span style='color: #FFD700'>within some radius</span></b> which we denote as $\epsilon$ (*number of observations or data points*) of the point.
>
>The **area in which this point radius covers** is called the <b><span style='color: #87CEEB'>epsilon neighbourhood</span></b>.

>[!abstract] High density
>We can denote a <b><span style='color: #FFD700'>threshold</span></b> called `minPts` which indicates if the points epsilon neighbourhood is of high density or low density.
# Core Terms In DBSCAN
---
We need to know what is a **core**, **border** & **noise points**.

>[!abstract] Core point
>A core point is when a point has at least `minPts` points within its epsilon neighbourhood. Basically it is a <b><span style='color: #FFD700'>high density point</span></b>.

>[!abstract] Border point
>It is <b><span style='color: #FFD700'>not a core point</span></b>, but <b><span style='color: #FFD700'>within some epsilon neighbourhood of some core point</span></b>.

>[!abstract] Noise point
>It is <b><span style='color: #FFD700'>neither core nor border point</span></b> (*these are your outliers*).
>
>And they are all clustered in a special cluster, which is <b><span style='color: #FFD700'>cluster 0</span></b>.

So putting it all together:
![[DBSCAN Terminology Example.png|center]]
# DBSCAN Algorithm
---
Here is the **DBSCAN algorithm**, but first define the epsilon and the `minPts`, then do the following:
1) With the parameters of epsilon and `minPts` <b><span style='color: #FFD700'>label all points</span></b> (*data points*) as either core, border or noise points
2) For **all pairs of core points**, put an <b><span style='color: #FFD700'>edge between them if there are within 1 epsilon of each other</span></b>
3) Make each collection of <b><span style='color: #FFD700'>core points that are connected as 1 cluster</span></b>
4) Then **assign each border point** to one of the clusters of its <b><span style='color: #FFD700'>associated core points</span></b> (*can take the nearest one*)

>[!important] We do not need to specify the number of clusters for DBSCAN as it automatically determines it

>[!success] DBSCAN will automatically point out possible outliers
>The desirable amount of noise will be usually be between 1 - 30%

So what **affects the final clusters**:
- The value for epsilon ($\epsilon$)
- The number of `minPts`
- The use of [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Clustering.md#Scaling|scaling]] (*range or z-score*)

>[!info] Choosing the right epsilon & `minPts`
>For `minPts`, it is either through domain knowledge or set $minPts \ge p + 1$ where $p$ is the number of variables in the dataset.
>
>Lets denote the number for `minPts` as $m$.
>
>Compute the m-distance (*distance to the m-th nearest neighbour)* for all points. We expect to see a <b><span style='color: #FFD700'>sharp change at the value</span></b> (*difference of distance of m - 1 and m*) of m-distance that corresponds to a suitable value of epsilon.
# DBSCAN In R
---
## Finding The Right Epsilon

>[!note] You need to import the `dbscan` library

To **find the right epsilon** we can use the `kNNdistplot` function:

```R
kNNdistplot(as.matrix(df[,2:7]), k=7) # Change the values inside [] to the cols you are using and k to be the number of minPts
```

In the plot we are <b><span style='color: #FFD700'>looking for the knee</span></b>.
## Executing DBSCAN

>[!note] You need to import the `dbscan` library

We can **implement the DBSCAN** algorithm in R using the `dbscan` function:

```R
# Remember to scale
dbclust <- dbscan (x = data, eps = 30, minPts = 3) # Change eps and minPts to fit your requirements
# Note that x can be a dataframe which it will use euclidean distance or you can pass in a custom distance matrix

dbclust # printing will show the number of clusters & noise points
```
## Getting The Cluster Assignments

To get the **cluster assignments** if we are using the `dbscan` function when we can just look in the `cluster` variable:

```R
dbclust$cluster # This will give all the cluster assignments

# If you want to append it to your dataframe
df <- df %>% mutate(col_name = dbclust$cluster)
```
## Visualising the Clusters

This works for **any of the clustering methods**, but is only for **2d variables**:

```R
# as.factor shows the noise points else it will not show
plot(df$col1, df$col2, pch = 16, col = as.factor(df$cluster_col))
```