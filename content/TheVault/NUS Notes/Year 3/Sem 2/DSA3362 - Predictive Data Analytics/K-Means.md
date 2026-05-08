---
Title: K-Means
Date Created: 18-March-2026
Last Updated: 23-April-2026
Tags:
  - DSA3362
  - AI/ML/Clustering/K-Means
---
# K-Means
---
It is a <b><span style='color: #FFD700'>centroid based</span></b> clustering technique, where <b><span style='color: #FFD700'>K is the number of clusters</span></b>.

Its **aim** is to partition the data in K clusters such that **sum of squared distances** from observations to their assigned cluster centres (*centroids*) is <b><span style='color: #98FB98'>minimised</span></b>. And to make our clusters well formed, we also need to ensure <b><span style='color: #98FB98'>clusters are far apart from other clusters</span></b> (*maximise sum of squares between clusters*).

>[!info] This centroid based clustering technique is also known as an optimisation partitioning technique
> As we are optimising by some clustering technique (*minimisning sum of sqaures distance*).

>[!note] When analysing K-means groupings, we can use auxiliary variables which were not used in the grouping of the clusters
>Variables not used can be used to profile the groupings.

>[!fail] Is is not good in handling categorical variables

>[!fail] Need to know how many groups you want or how many clusters
>This can be solved using the [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Unsupervised Learning.md#Picking the Best Number of Clusters|elbow method]].
>
>In R you can plot the total within sum of squares against the number of clusters.

# Optimizing K-Means
---
## Finding the Optimal Number of Clusters

We can use **a few methods**:
1) **Elbow** method

Essentially we do a <b><span style='color: #FFD700'>iterative enumeration of the number of clusters</span></b>. At each iteration we compute the <b><span style='color: #FFD700'>total within SSE</span></b> and plot a graph.

Then <b><span style='color: #FFD700'>find the elbow or turning point</span></b>, that will be the optimal cluster size.

>[!fail] We need to indicate the max of the number of clusters for grid search

>[!question] Why not find the smallest SSE?
> This is because the extreme case of when <b><span style='color: var(--mk-color-red)'>every observation is its own cluster the total SSE will be 0</span></b> which is not optimal or what we want. 

To **do this in R**:

```R
n <- 5
wss <- numeric(n) # Within Sum of Squares
k <- numeric(n)
for (i in 1:n){
	algo <- kmeans(x = dat[,2:3], centers = i, nstart = 3, algorithm = "Hartigan-Wong")
	wss[i] <- algo$tot.withinss
	k[i] <- i
}
plot(x = k, y = wss, type = "l",
	xlab = "Number of clusters, K",
	ylab = "Within-Cluster Sum of Squares",
	col = "blue")
points(x = k, y = wss, pch = 16, col = "blue")
```

2) **Silhouette** method

**Same as the elbow method** but instead of SSE we use the [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Clustering.md#Silhouette Coefficient|overall silhouette coefficient]].

>[!note] You need to import the `cluster` library

We can do this in R using the `silhouette()` function:

```R
# x is your data used for clustering & you can change the distance calculation
dist_matrix <- dist(scale(x, center = T, scale = T), method = "euclidean")
sil <- silhouette(model$cluster, dis = dist_matrix)

kable(df1)
```

>[!info] Different clustering techniques will yield different silhouette score but the interpretation will be the same

3) **Pseudo-f** method

Also known as the <b><span style='color: #87CEEB'>Calinski-Harabasz index</span></b>, compares the between-cluster sum of squares (*SSb*) with within sum of squares (*SSw*).

$$
\text{pseudo-F} = \frac{SSb / (k - 1)}{SSw / (n - k)} 
$$
Where:
- $n$ is the number of observations (*data points*)
- $k$ is the number of clusters

>[!important] We are not looking for a turning point unlike in K-means but we are looking for a peak
> Because this means that, partitions are <b><span style='color: #98FB98'>well-separated clusters</span></b> (*large SSb*) and <b><span style='color: #98FB98'>homogeneous clusters</span></b> (*small SSw*).

# K-means Algorithm
---
Here is the **algorithm** for k-means:
1) Choose <b><span style='color: #FFD700'>k data points to be our initial centroids</span></b>
2) Assign <b><span style='color: #FFD700'>all other datapoints to the nearest centroid</span></b> based on distance (*sum of squares or Euclidian distance or anything else*)
3) Compute the <b><span style='color: #FFD700'>new centroid by computing the average of all data points</span></b>
4) **Repeat** step 2 to 3 with the new centroids until there is <b><span style='color: #FFD700'>no change or the change is minimal</span></b> for the centroids (*or max number of iterations has been hit*)

>[!info] You can also terminate after some number of iterations of updating our centroids

**Factors that affect the final clustering**:
- **Initialisation** of our centroids
- Partition algorithm used (*k-means vs k-medoids*)
- Proximity measures (*distances*)
- The value for k (*number of clusters*)
- `nStart` (*which creates n number sets of initial centroids*)
- Seed
- Position of k-means code from the `set.seed()` code (*like set.seed followed by 2 k-means*)
- **Scaling** (*min-max or z-score*)

For **min-max scaling** (*also known as range scaling*) the **formula** is as such:
$$
rg(x_{if}) = \frac{x_{if} - min(f)}{max(f) - min(f)}
$$
Where:
- $f$ is the column or variable
- $i$ is the i-th data point

For **z-score** scaling the **formula** is:
$$
z(x_{if}) = \frac{x_{if} - \mu(f)}{\sigma(f)}
$$
Where:
- $\mu(f)$ is the average of the column
- $\sigma(f)$ is the standard deviation of the column

>[!abstract] K-mediods & Fuzzy
>There are 2 more different algorithms. **K-medoids** is the same as k-means but now you <b><span style='color: #FFD700'>center around one data point which is the most representative around that cluster</span></b> (*meaning the centroid will always be one of the datapoints*). This and k-means are considered as <b><span style='color: #87CEEB'>hard clustering</span></b>. Then it will do a swap & see if this new medoid results in a lower cost.
>
>As for **fuzzy**, instead of saying this object is in cluster 1, it <b><span style='color: #FFD700'>gives the probabilities of the object bring in each cluster</span></b>. Fuzzy is considered <b><span style='color: #87CEEB'>soft clustering</span></b> (*because it gives a probability*).
# K-means in R
---
## Scaling

We can do **z-scaling** using the `scale` function in R:

```R
# Assumption that Y is at the last column
df[,-1] <- scale(df[,-1], center = T, scale = T) # Change to all the variables you want to scale

# If we have a mixed types of data, categorical and continuous we can scale like this
df %>% mutate_if(is.numeric , scale) %>%
	mutate_if(is.numeric, as.numeric)
```

This means mean = 0 and standard deviation = 1 for center = true & scale = true.
## Executing K-means

We can **execute the k-means algorithm** in R as well using the `kmeans` function:
```R
# x are the variables you want to use
# Change centers to k
kmeans(x = df[,-1], centers = 2, nstart = 3, algorithm = c("Hartigan-Wong")) # Frogy, MacQueen, Lloyd
```

>[!important] `kmeans` has randomness due to the initialisation of k centroids so remember to use `set.seed()`

>[!note] By default `kmeans` uses the Hartigan-Wong algorithm

You can also use `NbClust` which **finds the best number of clusters** for you without gird searching or doing the elbow method:

>[!note] You need to import the `NbClust` library

```R
NbClust(data = df, distance = "euclidean", min.nc = 2, max.nc = 10, method = "kmeans")
# min.nc is the min number of clusters and max.nc is the max
```

Then to **extract out the cluster assignments**:

```R
df_kmeans <- df %>% 
	mutate (c2 = as.factor(kmeans(x=df[,-1],centers = 2)$cluster))
```

There are also other things you can extract as well from `kmeans` model:
- `$size` (*size of each cluster*)
- `$centers` (*centroids*)
- `$cluster` (*clustering for each observation*)
- `$totss` (*total sum of square*)
- `$withinss` (*sum of squares within each cluster*)
- `$tot.withinss` (*total sum of squares within each cluster*)
- `$betweenss` which is `$totss` -`$tot.withinss` 

Just note that if you scale the data, the centroids are also scaled, to **reverse the scaling**:

```R
center_means <- attr(df_scaled, "scaled:center")
center_sds <- attr(df_scaled, "scaled:scale")

scaled_centroid <- kmeans$centers[cluster_number, ]
unscaled_centroid <- (scaled_centroid * center_sds) + center_means
# OR if you want to do everything in 1 shot
scaled_centroids <- kmeans$centers
t(t(scaled_centroids) * center_sds + center_means)
```
## Showing Cluster Statistics

We can get some **information about individual clusters** using the following:

```R
df %>%
	select(- y_col) %>%
	mutate(k2 = kmeans(x = df[,-1], centers=2)$cluster) %>% # This line is to append the cluster assignment to the rows
	group_by(k2) %>%
	summarise_all(mean)
```

Here you will get the average values of all the variables used which can give you a sense of what the datapoints in general have in common for each cluster.
## Executing K-medoids & Fuzzy

>[!note] You need to import the `cluster` library

We will use the function `pam` (*partitioning around medoids, meaning median*) for k-medoids and `fanny` for fuzzy

```R
md <- pam(x = data, k = 2, metric = "euclidean")
fz <- fanny(x = data, k = 2, metric = "euclidean")
# K is the number of clusters and metric is the proximity measure to use
```

>[!info] There is also `clara` for k-medoids which is faster than `pam`

