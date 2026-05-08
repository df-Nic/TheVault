---
Title: Hierarchical Clustering
Date Created: 10-March-2026
Last Updated: 25-March-2026
Tags:
  - DSA3362
  - AI/ML/C
  - AI/ML/Clustering/Hierarchical
---
# What is Hierarchical Clustering
---
It is a <b><span style='color: #FFD700'>connectivity based</span></b> clustering technique, where we <b><span style='color: #FFD700'>successively merge observation / clusters into a parent cluster</span></b> (*agglomerative hierarchical clustering*).

This technique produces a **nested sequence of clusters which can be visualised** as a <b><span style='color: #87CEEB'>dendrogram</span></b>. The leaves are the individual observations & the root cluster is at the top (*your entire dataset*).

![[Hierarchical Clustering & Dendrogram Example.excalidraw.png|center]]

>[!success] Hierarchical clustering will always push the dimension down to 2 dimensions

>[!success] Unlike k-means we do not need to worry about the number of clusters
>Because it will have clusters from 2 to n.

>[!fail] Unlike K-means or DBSCAN, in an agglomerative hierarchical clustering once an observation is assigned to a group it cannot be reallocated
>So a <b><span style='color: var(--mk-color-red)'>bad partition at the beginning cannot be undone</span></b> later on.
# Hierarchical Clustering Algorithms
---
In general instead of finding a partition to separate the data, instead we <b><span style='color: #FFD700'>merge clusters together until we have 1 cluster</span></b> (*known as the root cluster which is the entire dataset*).

>[!info] We can visualise this using a tree structure called a dendrogram

>[!warning] Hierarchical clustering is sensitive to a number of factors 
>- Number of $k$ clusters
>- Linkage method used
>- Use of scaling (It is <b><span style='color: #98FB98'>recommended to scale</span></b> for hierarchical clustering)
>- And many more...
## Types of Algorithms

There are **2 methods** for hierarchical clustering:
1) **Agglomerative** (*Bottom up*)

In **general**:
1) Start of by assigning <b><span style='color: #FFD700'>each individual data point as a cluster</span></b> (*singleton cluster*)
2) Start an iteration
3) <b><span style='color: #FFD700'>Merge 2 nearest clusters</span></b> to form a new cluster
4) <b><span style='color: #FFD700'>Recompute the distance</span></b> of the new cluster to all other clusters
5) **Repeat** steps 3-4 until we reach a <b><span style='color: #FFD700'>single root cluster</span></b>

>[!note] We will be focus on on agglomerative methods since it the most popular one
> ![[Dendrogram Example.png]]
> 
> This also shows a history of how each data point is merged into 1 root cluster there the <b><span style='color: #FFD700'>lowest merge is the first merger</span></b>. A **merge happens at some height,** which tell us the <b><span style='color: #FFD700'>distance between the 2 child clusters</span></b> before merging into 1.
> 
> The bottom most level (*the leaves*) are <b><span style='color: #FFD700'>individual observations</span></b>.
> 
> Here we also **show how this dendrogram can give us the clusters** so if we cut there is 7 clusters and any higher cuts will result in smaller number of clusters.

  2) **Divisive** (*Top down*)

In **general**:
1) Start from the <b><span style='color: #FFD700'></span>root cluster</b>
2) Start an iteration
3) <b><span style='color: #FFD700'>Take 1 cluster and split it into 2 clusters</span></b> where they are will be the least similar (*if there is a tie then do both*)
4) **Repeat** steps 3 until we we <b><span style='color: #FFD700'>only have singleton clusters</span></b>
# Linkage
---
How do we know if 2 clusters (*or 2 observations or 1 observation 1 cluster*) are **near to each other** we compute something called <b><span style='color: #87CEEB'>linkage</span></b>

There are **4 types of linkages** in hierarchical clustering:
1) **Single** linkage
2) **Complete** linkage
3) **Average** linkage
4) **Ward** linkage

Depending on what you choose, you will <b><span style='color: #FFD700'>compute the pairwise dissimilarity matrix, then fuse the smallest 2 clusters</span></b>.
## Single Linkage

Here the distance between 2 clusters is the <b><span style='color: #FFD700'>distance between the 2 closest points</span></b> between the 2 clusters (*1 point from each cluster*).

$$
d(C_{i}, C_{j}) = min(d(x, y)), x \in C_{i} \text{ and } y \in C_{j}
$$
Where:
- To compute the distance between 2 points you can use [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Clustering.md#Continuous Variables|any of the Minkowski distance]]

>[!success] Suitable for finding non-elliptical shaped clusters

>[!fail] Sensitive to noise in the data and may suffer from the chaining effect
>![[Chaining Effect Example.png|center|500]]

## Complete Linkage

Here the distance between 2 clusters is the <b><span style='color: #FFD700'>distance between the 2 furthest points</span></b> between the 2 clusters (*1 point from each cluster*).

>[!info] So instead of minimum you go for the maximum
>Then we <b><span style='color: #FFD700'>merge the clusters who has the smallest largest distance</span></b> (*find the largest pairwise distance & merge the smallest one*).

$$
d(C_{i}, C_{j}) = max(d(x,y)), x \in C_{i} \text{ and } y \in C_{j}
$$

>[!success] It avoids the chaining effect which single linkage method might face

## Average Linkage

Here the distance between 2 clusters is the <b><span style='color: #FFD700'>average distance of all pair wise distances</span></b> between the 2 clusters (*basically all pairs and then average the distance*).

Then we <b><span style='color: #FFD700'>merge 2 clusters with the smallest average linkage</span></b>.

$$
d(C_{i}, C_{j}) = \frac{1}{\vert C_{i} \vert \vert C_{j} \vert} \times \sum_{x \in C_{i}, y \in C_{j}} d(x, y)
$$
Where:
- $\vert C \vert$ is the number of points in the cluster $C$

## Centroid Linkage

Instead of computing the pairwise distances we just compute the <b><span style='color: #FFD700'>distances between clusters based on the centroid</span></b>. Then we merge the smallest distance.

## Ward Linkage

Here the distance between 2 clusters is the <b><span style='color: #FFD700'>increase in the sum of square error</span></b> from <b><span style='color: #FFD700'>having 2 clusters instead of 1 merged cluster</span></b> (*essentially is it better to merge or leave it split*).

$$
d(C_{i}, C_{j}) = \sqrt{\frac{2 \vert C_{i} \vert \vert C_{j} \vert}{\vert C_{i} \vert + \vert C_{j} \vert}} \times d(c_{i}, c_{j})
$$
Where:
- $c_{i}$ and $c_{j}$ are the centroids of the cluster
# Optimising Hierarchical Clustering
---
## Number of Clusters

For hierarchical clustering we can use, the [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Clustering.md#Finding the Optimal Number of Clusters|elbow or silhouette coefficient method]]. However for hierarchical clustering we can also <b><span style='color: #FFD700'>use the dendrogram</span></b> to select the number of clusters.

We can use **2 methods**:
1) Use a **pre-specified** height
2) Based on the **largest gap between 2 successive nodes**

>[!question] What is the largest gap
>![[Largest Gap Example.png|center]]
>
>If you look at the dendrogram, we do 1 merge at a certain height, so if the <b><span style='color: #FFD700'>difference in height</span></b> after the $i$-th merge and the $i+1$th <b><span style='color: #FFD700'>merge is the largest that means that the 2 clusters are very far apart</span></b> and we just take the number of clusters to be at the $i$-th merge.
## Suitable Linkage Method

We can use the <b><span style='color: #87CEEB'>cophenetic corelation coefficient</span></b> (*cophenetic distance*).

>[!abstract] Cophenetic distance
>
>![[Cophenetic Distance Example.excalidraw.png|center]]
>
>Between two observations is the <b><span style='color: #FFD700'>proximity</span></b> (*distance*) at which an agglomerative hierarchical clustering algorithm <b><span style='color: #FFD700'>merges them into the same cluster for the first time</span></b>.

We can generate what is known as a <b><span style='color: #87CEEB'>cophenetic distance matrix</span></b> which is the <b><span style='color: #FFD700'>pair-wise cophenetic distances</span></b>.

Using **this & the distance matrix** we can compute the <b><span style='color: #87CEEB'>CoPhenetic Corelation Coefficient</span></b> (*CPCC*). It is the <b><span style='color: #FFD700'>correlation</span></b> between the cophenetic distance matrix & the original distance matrix.

>[!success] The larger the CPCC the better the linkage method
# Hierarchical Clustering in R
---
## Executing Hierarchical Clustering

We can use the `dist` and `hclust` functions to **do hierarchical clustering** (*not caret*):

```R
# Compute the distance
dist <- dist(x = x_data, method = "euclidean") # manhattan, minkowski, canberra

# dist <- as.dist(x = gower.dist (data)) also works if we have categorical and continuous data

# To do hierarchical clustering
hc_tree <- hclust(d = dist , method = "single") # complete, average, ward .D2
```

>[!note] The `hclust` will do all iterations not just once
## Plotting The Dendrogram

We can just use the `plot` function in R to show the dendrogram:

```R
plot(hc_model)
```

You can also **visualise the merges of the clusters** using the `as.dendrogram` function in the base R package:

```R
as.dendrogram(hc_tree) %>% str()
```

## Obtaining The Clustering Results

To **get the cluster assignment** if you are using the `hclust` function, use the `cutree` function:

```R
df %>% mutate (cluster = as.factor(cutree(tree = hc_tree, k = 3))) 
# Tune k to the number of clusters you want or use h for height
# cluster is just the column name you can change it
```

To **get the number of clusters at a certain height** we can use the same `cutree` function:

```R
length(unique(cutree(hc_tree, h = 3))) # Inhead of k use h
# Basically we get the assignment at h = 3 then count the number of unique values
```

With the clusters you can get the **characteristic of the clusters** by using this:

```R
df_hclust %>%
select(columns_to_use) %>% # Use - col_name to exclude a column
group_by(cluster) %>%
summarise_all(mean) # Or anything else
```

You can also get when the observations first meet, or the **cophenetic distance matrix** using `conphenetic` function:

```R
cop <- cophenetic(hc_tree) # Inteprete it as col meets row at this distance
dcomp <- as.dendrogram(cop) # Which you can print as a dendrogram
str(dcomp) 
```

## Finding the Best Linkage to Use

We can use the distance and the cophenetic distance matrix to **compute the CPCC**, using the `cor` function:

```R
linkage <- c("single", "complete", "average", "ward .D2")
sapply (X = linkage, FUN = function(s) {
		cor(cophenetic(x = hclust(d = dist, method = s)), dist)
	}
)
```

>[!note] Essentially by computing the corelation with the cophenetic distance and the normal distance if they are highly corelated it means they agree with one another
>Thus the linkage is good. 

