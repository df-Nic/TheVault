---
title: Data Mining
Date Created: 2025-09-05
Last Updated: 2025-09-28
tags:
  - CS4225
  - BigData/DataMining
---

# Similarity Search
---
A **similarity search** is a problem in which we want to <b><span style='color:var(--mk-color-yellow)'>find something similar between objects</span></b>.

We can either find all documents or **compute similarity of all pairs** (*all pairs similarity*).

>[!examples] Examples of real life similarity search use cases
>- Customer who purchase similar products, for personalised advertisements
>- Users who visit similar websites, grouping people based on interest

We define similarity as <b><span style='color:var(--mk-color-turquoise)'>near neighbours</span></b>, points that are <b><span style='color:var(--mk-color-yellow)'>small distance apart</span></b>.

>[!info] Distance measure
>When we calculate distance in a 2 dimension space we use the x & y coordinates ($d(x, y$).

>[!success] The smaller then distance the more similar 2 objects are
>This is known as <b><span style='color:var(--mk-color-turquoise)'>similarity measures</span></b>, which are the **opposite of distance measures**.
## Similarity Metrics

### Euclidean Distance

The most standard distance measure is **straight line distance** or the <b><span style='color:var(--mk-color-turquoise)'>Euclidean distance</span></b>.

Between 2 points the formula for **calculating the straight distance** is:
$$
d(a, b) = \sqrt{\sum^{D}_{i = 1} (a_{i} - b_{i}) ^{2}}
$$
Where:
- a and b are 2 points of the same dimension
- $D$ is the dimension that the points are in (*2, 3, 4, n*)
- $a_{i}$ and $b_{i}$ is the value at that particular coordinate index
### Manhattan Distance

Another distance we can calculate is the <b><span style='color:var(--mk-color-turquoise)'>Manhattan distance</span></b>. Unlike straight line distance where we can traverse diagonal, we can <b><span style='color:var(--mk-color-yellow)'>only move vertical or horizontal</span></b>

Between 2 points the formula for **calculating the Manhattan distance** is:
$$
d(a, b) = \sum^{D}_{i = 1} \vert a_{i} - b_{i}\vert
$$
<div style="page-break-after: always;"></div>

Where:
- a and b are 2 points of the same dimension
- $D$ is the dimension that the points are in (*2, 3, 4, n*)
- $a_{i}$ and $b_{i}$ is the value at that particular coordinate index
### Cosine Similarity

Instead of viewing the points as vectors and computing the magnitude, we can <b><span style='color:var(--mk-color-yellow)'>check the orientation</span></b> (*angle*) between them. This is known as <b><span style='color:var(--mk-color-turquoise)'>cosine similarity</span></b>.

Between 2 vectors the formula for **calculating the cosine similarity** is:
$$
d(a, b) =  \cos{\theta} = \frac{a \cdot b}{\Vert a \Vert \cdot \Vert b \Vert}
$$
Where:
- a and b are 2 vectors
- $a \cdot b$ is the [[Orthogonality#Dot Product|dot product]] of the 2 vectors

>[!important] Cosine similarity only considers direction
>If you scale either vector by a constant it does not change.

There are **3 classifications** in cosine similarity, if the value is:
- **1** - It means they are <b><span style='color:var(--mk-color-yellow)'>related</span></b>
- **0** - It means they are <b><span style='color:var(--mk-color-yellow)'>unrelated</span></b>
- **-1** - It means they <b><span style='color:var(--mk-color-yellow)'>contradict one another</span></b>
### Jaccard Similarity

We use <b><span style='color:var(--mk-color-turquoise)'>Jaccard similarity</span></b>, when we are <b><span style='color:var(--mk-color-yellow)'>dealing with a set of items</span></b>.

>[!info] It is essentially the set of all similar items over all unique items

Between 2 sets the formula for **calculating the Jaccard similarity** is:
$$
sJaccard(a, b) = \vert \frac{a \cap b}{a \cup b} \vert
$$
Where:
- a and b are 2 sets

Then the <b><span style='color:var(--mk-color-turquoise)'>Jaccard distance</span></b> it is just $1 - sJaccard(A, B)$
## Finding Similar Documents

So how can we convert a medium and find out if they are similar or not. There are **2 essential steps** and they are <b><span style='color:var(--mk-color-turquoise)'>shingling</span></b> & <b><span style='color:var(--mk-color-turquoise)'>min-hashing</span></b>.

>[!note] The big picture is a document will go through shingling then through the min hash & then do a similarity comparison
<div style="page-break-after: always;"></div>

### Shingling

Shingling is the <b><span style='color:var(--mk-color-yellow)'>conversion of documents into sets of short phrases</span></b> called shingles.

It can vary in size and they are referenced as a <b><span style='color:var(--mk-color-turquoise)'>k-shingle</span></b> (*or k-gram*). This means that in a single, it <b><span style='color:var(--mk-color-yellow)'>consists of k tokens</span></b>.

>[!example] Example of a 2-shingle
>Given a document, "the cat is glad"
>
>We will have this set of 2-shingles $S(D_{1})$ = {"the cat", "cat is", "s=is glad"}

Foe **every document** they will have its **own set of shingles** which we can **represent in a matrix**, where:
- The **row** represents the unique shingles
- The **column** represents the document

>[!info] If the matrix at index $i$ and $j$ is 1, that means that shingle at index $i$ is in document $D_{j}$.

With this we can use the [[Data Mining#Jaccard Similarity|Jaccard similarity]] to **measure the similarity** but just taking the <b><span style='color:var(--mk-color-yellow)'>set of shingles between 2 documents</span></b>.
### Min-Hashing

After forming shingles, we can <b><span style='color:var(--mk-color-yellow)'>hash them</span></b> into a more understandable format. And this **hash must be small enough to fit into RAM**.

>[!important] Similar shingles must be hashed to the same value
>
>If not then the hash function does not work properly.

>[!success] Much more efficient than comparing all pairs
>
>Min hash gives a <b><span style='color:var(--mk-color-green)'>fast approximation</span></b> of the result using Jaccard similarities.

>[!example] Example of executing a min hash
>Assume we have 3 shingles, the cat, cat is, is glad.
>
>We just put each of them into a hash function. Suppose they return 12, 74 and 48 respectively then we will return 12.

How does this concept helps in finding that 2 documents are similar. The <b><span style='color:var(--mk-color-yellow)'>probability that 2 documents have the same min hash will be higher if they are similar</span></b>.

This is where this property comes in, where the <b><span style='color:var(--mk-color-yellow)'>probability of the min hash being the same is equal to the</span></b>   [[Data Mining#Jaccard Similarity|Jaccard similarity]],

>[!question] Why is this property true
>
>Lets look at 2 documents if they have 2 shingles which are the same and a total of 4 unique shingles, then the probability any shingle being the smallest hash value is 1/4.
>
>Since there are 2 similar shingles, then we have a probability of 50%.

>[!important] Important characteristics of the hash function
>The **assignment of hash values** has to be <b><span style='color:var(--mk-color-yellow)'>random</span></b>, if <b><span style='color:var(--mk-color-red)'>not the probability is not even</span></b>.
>
>And secondly the hash function should <b><span style='color:var(--mk-color-yellow)'>have enough buckets to prevent collisions</span></b>.
### Putting It All Together

So all the documents will go through shingling, then each single will be passed into the min hash, the <b><span style='color:var(--mk-color-yellow)'>documents with high similarity</span></b> are called <b><span style='color:var(--mk-color-turquoise)'>candidate pairs</span></b>.

We can either just use the candidate pairs or check one by one if they are actually similar.

>[!note] Some might use more than 1 hash function
>In practice we can <b><span style='color:var(--mk-color-yellow)'>use multiple hash functions</span></b> and generate $N$ signatures.
>
>Then for 2 documents to be **similar** they must have a <b><span style='color:var(--mk-color-yellow)'>significant number of candidate pairs</span></b>.

So how can we translate this to [[MapReduce|MapReduce]]?
1) **Map**
The map will take in a document and <b><span style='color:var(--mk-color-yellow)'>extract the shingles</span></b> . Then it will <b><span style='color:var(--mk-color-yellow)'>hash each shingle</span></b> and <b><span style='color:var(--mk-color-yellow)'>take the min hash</span></b>.

It will then emit a pair of min hash value and the document id.

2) **Reduce**
It will receive all documents with the same hash value and then <b><span style='color:var(--mk-color-yellow)'>generate all candidate pairs</span></b>.

>[!note] It is optional but the reducer can compare each pair to check if they are actually similar
# Clustering
---
The goal of clustering is we want to <b><span style='color:var(--mk-color-yellow)'>separate unlabelled data into groups of similar points</span></b>.

>[!important] Clusters should have high intra-cluster similarity, and low inter-cluster similarity
>
>**High intra-cluster** - Means that **points** within the cluster should be as <b><span style='color:var(--mk-color-yellow)'>close as possible</span></b>.
>
>**Low inter-cluster** - Means that between and 2 **clusters** it should be as <b><span style='color:var(--mk-color-yellow)'>far away as possible</span></b> (*substantially different*).
## K-Means Algorithm

This [[Unsupervised Learning#K-means Clustering|algorithm]] will <b><span style='color:var(--mk-color-yellow)'>group points into clusters</span></b>.

```cpp
vector<int> kMeans(Data, k) {
	vector<int> assignment; // Store the assignment of clusters for each point
	centroids = pickRandomCentroids(k); // Pick k random centroids
	while (true) {
		newAssignment = assign(data, centroids); // Assign all points to the nearest cluster
		if (newAssignment == assignment) {
			break;
		}
		updateCentroids(centroids, newAssignment); // Move the clusters to the average of all the assigned points
	}
	
	return assignment;
}
```

>[!note] K-means always converge
>
>But the final output depends on the initialisation of the centroids.

### MapReduce Implementation of K-Means

![[K-Means MapReduce Implementation.png|center|350]]

First we will have a `Configure` function which will <b><span style='color:var(--mk-color-yellow)'>load in the clusters from some file</span></b>. This is not related to the map or the reducer phases.

Now our `Map` function will do 2 things:
- <b><span style='color:var(--mk-color-yellow)'>Assign</span></b> the point to one of the <b><span style='color:var(--mk-color-yellow)'>nearest cluster</span></b>
- This is **not necessary**, but it will extend the coordinates of the point by <b><span style='color:var(--mk-color-yellow)'>adding a 1 behind</span></b> (*used for counting*)
- It will emit a pair of cluster and the point

Now the `Reducer` function 
- It will **initialise a point sum** which is a vector of <b><span style='color:var(--mk-color-yellow)'>n-dimension + a counter</span></b> of zeros ($[0, 0, 0]$ *for x, y, count - 2D*).
- Then after summing all the points it will <b><span style='color:var(--mk-color-yellow)'>compute the new centroid</span></b> by taking the average (*the count is at the back*)
- Then it will <b><span style='color:var(--mk-color-yellow)'>emit a pair of the old and new centroid</span></b>

>[!failure] There is a issue with this and is the network traffic from the `Map` function
>
>The `Map` functions <b><span style='color:var(--mk-color-red)'>emits each point data once</span></b>. And this happens for every iteration.

We can **solve the issue** above by using a [[MapReduce#Combiner|in-mapper combiner]] to **store the sum** of all the points in the cluster (*key*).  The rest of the implementation is the same, just that once all the mappers are done we need a `Close` function to emit all key value pairs in the HashMap.

So instead of sending all points over the network we <b><span style='color:var(--mk-color-green)'>only send over k number of data points</span></b>, where **k is the number of clusters**.