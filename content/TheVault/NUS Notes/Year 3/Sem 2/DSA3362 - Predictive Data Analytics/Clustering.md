---
Title: Clustering
Date Created: 25-February-2026
Last Updated: 24-April-2026
Tags:
  - DSA3362
  - AI/ML/Clustering/K-Means
---
# Clustering
---
We mentioned that [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Supervised Learning.md#Supervised & Unsupervised Learning|unsupervised learning]] is discovering interesting patterns or structures in <b><span style='color: #FFD700'>unlabelled data</span></b>.

Generally there are **2 methods** of unsupervised learning:
1) **Clustering**, <b><span style='color: #FFD700'>observations in 1 cluster are similar than observations in other clusters</span></b> (*think of a cluster as group*)
2) **Dimensionality reduction**
## Proximity Measures

How can we **compute the distance between 2 points** or <b><span style='color: #87CEEB'>dissimilarity</span></b>? It depends on the type of data what we are dealing with.

>[!important] It does not matter if its continuous or categorical, if the distance matrix can be computed it is fine
### Continuous Variables

For continuous values we can compute the <b><span style='color: #FFD700'>Minkowski distance</span></b> (*a generalised formula*):
$$
D(x_{i}, x_{j}) = \left (\sum^{d}_{l = 1} \vert x_{il} - x_{jl} \vert^{p} \right)^{1/p}
$$
Where:
- $D$ stands for distance
- $d$ is the number of dimensions (*2 dimension is 2 points, 3 dimension is 3 and so on*) or in a data table stand, it is the number of columns

>[!note] All your distance measures like Euclidian and Manhattan are all from Minkowski distance

>[!warning] Features with large values will dominate other features, thus the dissimilarity might depend on these features
>So to handle this, <b><span style='color: #98FB98'>scaling</span></b> is done to variables (*don't need to scale if everything is the same unit*). There many types of scaling:
>1) **z-score** scaling
>$$
>x_{il} = \frac{x^{*}_{il} - m_{l}}{s_{l}}
>$$
>Where:
>- $x^{*}_{il}$ is the original value of column $l$ for a the $i$-th datapoint
>- $m_{l}$ is the mean (*average*) of column $l$
>- $s_{l}$ is the standard deviation of column $l$
>
>
>>[!fail] But z-score is not good if there are a lot of outliers
>
>2) **Min max** scaling
>Here we scale based on the minimum and maximum values which is <b><span style='color: #98FB98'>better when dealing with outliers</span></b>.
>$$
>x_{il} = \frac{x^{*}_{il} - min(l)}{max(l) - min(l)}
>$$
>Where:
>- $max/min(l)$ is the maximum or minimum values for the column <b><span style='color: #FFD700'>before scaling</span></b> (*original values*)

Here are some proximity measures for continuous values:
- Euclidean distance
- Manhattan distance
- Mahalanobis distance
- Person correlation coefficient
- Cosine similarity
### Discrete Variables

For discrete variables, lets assume we are dealing with categories of **binary values**:
- $n_{11}$ will be the number of columns where the <b><span style='color: #FFD700'>2 data points has the value to be 1</span></b> (*present*)
- $n_{00}$ will be the number of columns where the <b><span style='color: #FFD700'>2 data points has the value to be 0</span></b> (*absent*)
- $n_{10}$ and $n_{01}$ will be the number of columns where the <b><span style='color: #FFD700'>2 datapoints has opposing binary values</span></b>

With this we can compute the dissimilarly using the following formulas  
1) **Hamming distance**

Number of <b><span style='color: #FFD700'>positions at which the corresponding values are different</span></b>.

>[!note] You need to import the `e1071` library

$$
D(x_{i},x_{j}) = 1 - S(x_{i},x_{j}) = 1 - \frac{n_{11} + n_{00}}{n_{11} + n_{00} + w(n_{01} + n_{01})}
$$
Where:
- $S$ stands for similarity
- $w$ is a weight & for invariant similarity typically $w = 1$

We can do this in R by using the `hamming.distance` function:

```R
hamming.distance(as.matrix(data))
```

2) **Jaccard distance**
$$
D(x_{i},x_{j}) = 1 - S(x_{i},x_{j}) = 1 - \frac{n_{11}}{n_{11} + w(n_{01} + n_{01})}
$$

We can do this in R as well, but first do <b><span style='color: #FFD700'>encode the values as either 0 or 1</span></b>.

```R
df <- df %>% mutate (Math = recode(Math , "Pass" = 1 , "Fail" = 0) ,
Science = recode (Science, "Pass" = 1 , "Fail" = 0))

dist (x = df_x_cols, method = "binary", diag = TRUE , upper = TRUE)
```

>[!important] To choose which label to encode 1 or 0 will give different results
> It is <b><span style='color: #FFD700'>asymmetric</span></b>, thus to choose is usually done by experts. But as a recommendation, encode the label with less information as 0.

### Mixed Variables

So far the distance measures shown all rely that all columns between 2 data points are either discrete or continuous. But what if **there is a mix**?

Then we compute using <b><span style='color: #87CEEB'>Gower's distance</span></b>:

>[!note] You need to import the `StatMatch` library

$$
D(x_{i},x_{j}) = \frac{\sum^{d}_{l = 1} \delta_{ijl} \times S_{ijl}}{\sum^{d}_{l = 1} \delta_{ijl}}
$$
Where:
$$
\delta_{ijl} =
\begin{cases}
1,  & \text{if $x_{ij}$ and $x_{jl}$ is non-missing} \\
0, & \text{otherwise}
\end{cases}
$$
This $\delta$ is a <b><span style='color: #FFD700'>weight to say whether to include the column or not</span></b>.

Then for $S_{ijl}$:
- For a **continuous variable**
$$
S_{ijl} = \frac{\vert x_{il} - x_{jl} \vert}{R_{t}}
$$
Where:
- $R_{t}$ is the range of the column so its just $max(l) - min(l)$

>[!info] This is just the Manhattan distance after standardization.

- For a **discrete variable**
$$
S_{ijl} =
\begin{cases}
0,  & \text{if $x_{i} = x_{j}$} \\
1, & \text{if $x_{i} \neq x_{j}$}
\end{cases}
$$

We can do this in R by using the `gower.dist` function:

```R
gower.dist(data)
```
## Clustering Techniques

There are **3 main clustering techniques**:
1) [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/K-Means.md|K-means]]
2) [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Hierarchical Clustering.md|Hierarchical]]
3) [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/DBSCAN.md|DBSCAN]]
# Clustering Evaluation
---
Since there are <b><span style='color: var(--mk-color-red)'>no true label</span></b> since clustering is an **unsupervised learning** method, we have to use these measurements:
- Cluster **cohesion**, which is how <b><span style='color: #FFD700'>closely related observations in a cluster are</span></b> (*minimising total within SSE*)
- Cluster **separation**, which is how <b><span style='color: #FFD700'>distinct a cluster is from other clusters</span></b> (*maximising total SSB*)

![[Separation & Cohesion .png|center]]

>[!important] By minimising total SSE it is the same as maximising total SSB
## Computing Cohesion

So given a cluster $C_{i}$, the **formula to compute cohesion** is as follows:
$$
\text{cohesion}(C_{i}) = \sum_{x \in C_{i}} \\\Vert x - c_{i} \Vert
$$
Where:
- $c_{i}$ (*small c*) is the centroid of the given cluster
- $\Vert x - c_{i} \Vert$, is any [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Clustering.md#Continuous Variables|distance formula]]

If we <b><span style='color: #FFD700'>do not have the centroid</span></b>, we can compute the **pairwise distance and average** it:
$$
\text{cohesion}(C_{i}) = \frac{1}{\vert C_{i} \vert } \sum_{x, y \in C_{i}} \Vert x - y \Vert 
$$
Where:
- $\vert C_{i} \vert$ is the number of points within the cluster $C_{i}$
- $\Vert x - y \Vert$, is any [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Clustering.md#Continuous Variables|distance formula]]

Now what if we want to **quantify the cohesion of all clusters**, then we take the <b><span style='color: #87CEEB'>total sum of square error</span></b>:
$$
SSE = \sum_{i}\sum_{x \in C_{i}} \Vert x - c_{i} \Vert^{2}
$$

>[!note] You can change to use the pairwise distance, square it and then average it but the formula remains the same
## Computing Separation

We can compute separation by simply taking the **distance between 2 cluster centroids**:
$$
\text{separation}(C_{i}, C_{j}) = \\\Vert c_{i} - c_{j} \Vert
$$
Where:
- $c_{i}$ (*small c*) or $c_{j}$ is the centroid of the given cluster $i$ and $j$ respectively

You can also take into **respect from the center of the entire dataset**:
$$
\text{separation}(C_{i}) = \\\Vert c_{i} - c \Vert
$$
Where:
- $c$ is the centroid of the entire dataset

Then to **quantify the separation of all clusters**, then we take the between <b><span style='color: #87CEEB'>group sum of square error</span></b> (*SSB*):
$$
SSB = \sum_{i} \vert C_{i} \vert \Vert c_{i} - c \Vert^{2}
$$
>[!info] We multiply by the cluster size because we want to give more weight to larger clusters
## Silhouette Coefficient

Here we want to **evaluate** the model on a <b><span style='color: #FFD700'>single point</span></b> (*can be a cluster or the entire dataset*) and <b><span style='color: #FFD700'>use a combine measure of cohesion & separation</span></b>.
### Single Observation

For a single observation $x$ we do the following:
1) Compute **average distance to all other observations in the same cluster** ($a_{c}$), <b><span style='color: #FFD700'>this is cohesion</span></b>

$$
a_{x}= \frac{1}{\vert C_{i} \vert - 1} \sum_{y \in C_{i}, y \neq x} \Vert x - y \Vert
$$
>[!success] We want $a_{x}$ to be as close to 0 as possible

Where:
- $\vert C_{i} \vert$ is the number of points within the cluster $C_{i}$
- $\Vert x - y \Vert$, is any [[Year 3/Sem 2/DSA3362 - Predictive Data Analytics/Clustering.md#Continuous Variables|distance formula]]

2) Then compute the **minimum average distance** from this observation to **all other observations that are not in the same cluster** ($b_{x}$), <b><span style='color: #FFD700'>this is separation</span></b>
$$
b_{x} = \text{min}_{j \neq i} \frac{1}{\vert C_{j} \vert} \sum_{z \in C_{j}} \Vert x - z \Vert
$$

>[!note] Here we are just finding the distance to 1 cluster that yields the smallest average distance from this 1 observation to all the observations in that 1 cluster

3) Then compute the **silhouette coefficient**

$$
s_{x} = \frac{b_{x} - a_{x}}{max(a_{x}, b_{x})}
$$
>[!success] To have a good clustering we want the difference to be large
>We **divide by the denominator** is because we want to <b><span style='color: #FFD700'>normalise</span></b> the final value to be <b><span style='color: #FFD700'>between -1 and 1 inclusive</span></b>.
>
>If it is <b><span style='color: #98FB98'>near to 1 the better the clustering model</span></b> (*0 is neutral*).

>[!abstract] Then for a singleton cluster and the entire dataset we can just repeat what we did
>For a **singleton cluster**, we average the silhouette coefficient of <b><span style='color: #FFD700'>all observations within the cluster</span></b>. This is known as the <b><span style='color: #87CEEB'>silhouette coefficient of a cluster</span></b>
>
>For the **entire dataset**, we average the silhouette coefficient of <b><span style='color: #FFD700'>all observations</span></b>. This is known as the <b><span style='color: #87CEEB'>overall silhouette coefficient</span></b>.
>
>**With the overall silhouette coefficient** you can plot against the number of clusters & take the <b><span style='color: #FFD700'>peak or elbow</span></b> for the **best number of clusters**.
# What to Choose?

There is no hard rule to say this algorithm is better, but here are some **guidelines**:
1) **Type of clustering**
	- When <b><span style='color: #FFD700'>hierarchical structure</span></b> is desired (e.g., creating a biological taxonomy), hierarchical clustering is preferred2
	- In the case of clustering for <b><span style='color: #FFD700'>summarisation</span></b>, k-means would be typically used
2) **Type of clusters**
	- K-means and some hierarchical clustering (complete/Ward linkage) algorithms tend to <b><span style='color: #FFD700'>produce globular clusters</span></b> in which observations are <b><span style='color: #FFD700'>close to each other</span></b>
	- DBSCAN, as well as single linkage clustering, would produce <b><span style='color: #FFD700'>clusters in which observations are not very similar</span></b> to one another (e.g., segmenting a geographical area based on type of land cover)
3) **Characteristics of datasets and attributes**
	 - K-means can only be used when <b><span style='color: #FFD700'>cluster centroids can be meaningfully calculated</span></b>
	 - Hierarchical clustering and DBSCAN can be applied <b><span style='color: #FFD700'>as long as some distance measures can be computed</span></b>
4) **Noise and outliers**
	- K-means and some hierarchical clustering algorithms would be <b><span style='color: #FFD700'>sensitive to noise and outliers</span></b>, while DBSCAN could <b><span style='color: #FFD700'>detect possible outliers</span></b>
	- This issue may be quite difficult, as their definition is not clear and what is noise or an outlier to one analyst may be interesting to another one
