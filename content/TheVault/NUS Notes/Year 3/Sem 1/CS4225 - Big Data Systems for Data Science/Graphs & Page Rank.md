---
title: Graphs & Page Rank
Date Created: 2025-11-07
Last Updated: 2025-11-16
tags:
  - CS4225
  - DataStructures/Graphs
  - ApacheSpark/GraphProcessing
---
# Graph Data
---
If your <b><span style='color: #F0E68C'>data has relationships between each other</span></b>, you can consider storing it as a graph.

So our **nodes** will be <b><span style='color: #F0E68C'>objects</span></b> (*people, places, etc*) and the **edge** between 2 nodes represents some <b><span style='color: #F0E68C'>relationship</span></b> between them.

>[!example] Example of graph data is information networks
>A very popular network which does cross disciplinary relationships. Essentially it maps concepts between different fields.

A popular **graph database** to store data as a graph is <b><span style='color: #87CEEB'>neo4j</span></b> (*also for graph processing*), which uses <b><span style='color: #DDA0DD'>Cypher query language</span></b>.
# Page Rank
---
**Page rank** is the <b><span style='color: #F0E68C'>algorithm</span></b> used by the internet to give you the <b><span style='color: #F0E68C'>most relevant webpages</span></b> based on your search query.

You can think of the <b><span style='color: #F0E68C'>web / internet as a directed graph</span></b> where the:
- Nodes are webpages
- Edges are hyperlinks to another webpage

However <b><span style='color: var(--mk-color-red)'>not all web pages are equally important</span></b>. Knowing which pages are important is necessary for web-related tasks. Just imagine searching for YouTube but all you get is some random websites.

>[!info] Importance
>Importance is essentially the relevancy of the webpage based on the search query.
>
>So it exploits the fact that <b><span style='color: #F0E68C'>webpages which are important are more likely the webpages the user wants</span></b>.

There are some <b><span style='color: var(--mk-color-red)'>issues with page rank</span></b> which are:
- **Does not consider popularity based on specific topics**, the solution to this is [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Graphs & Page Rank.md#Topic Specific Page Rank|topic specific page rank]]
- **Uses single measure of importance**, there are other models such as <b><span style='color: #98FB98'>hubs and authorities</span></b>.
- **Susceptible to link spam**, artificial links are created to boost rank, the solution is [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Graphs & Page Rank.md#Knowing Importance|trust rank]]
## Knowing Importance

So how can we **compute the importance** of a webpage, well we can exploit the graph structure of the web. A <b><span style='color: #F0E68C'>page is more important if it has more incomming edges</span></b> (*more hyperlinks to that page*).

>[!note] Some people think of links as votes

>[!warning] A issue with this is that a user can create many dummy webpages which has hyperlinks to a main webpage, driving up its rank!

Why not add a <b><span style='color: #98FB98'>weighted vote</span></b>. It essentially means that <b><span style='color: #F0E68C'>votes from a less important page weighs less than from a important page</span></b>. 

This is a <b><span style='color: #F0E68C'>recursive definition</span></b> (*need to know the other webpages until there is no more incoming hyperlinks*)

So essentially a hyperlink from a important webpage will constitute a lot more votes.

>[!example] So even if there are many dummy pages, the weigh of this vote is smaller as compared to say Wikipedia linking to that webpage.
### Voting Formulation

![[Page Rank Voting Formulation.excalidraw.png|center|350]]

Let $r_{j}$ be the rank / importance for webpage $j$, then **its vote to a particular webpage** is computed as the <b><span style='color: #F0E68C'>importance / rank of the webpage divided by the number of out-links</span></b> (*edges pointing out*).

Then the **rank of a webpage** is given by the <b><span style='color: #F0E68C'>sum of all importance / ranks of the incoming edges</span></b>.

>[!abstract] Here you can see the recursive process
#### "Flow" Model

We can **formulate** the rank of a webpage as a **"flow" model**:
$$
r_{j} = \sum_{i \rightarrow j} \frac{r_{i}}{d_{i}}
$$
Where:
- $i \rightarrow j$ means for all nodes where it has a out link to webpage j
- $d_{i}$ is the number of out links or out-degree edges from node $i$

So by doing this we will have **n linear equations to solve**.

>[!question] Is the solution unique?
>It depends if we have <b><span style='color: #F0E68C'>n linear equations with n variables then it is unique</span></b>.
>
>But if we have <b><span style='color: var(--mk-color-red)'>less linear equations and more variables then the solution is not unique</span></b>.
>
>To solve make the solution unique we can <b><span style='color: #F0E68C'>add a additional constraint to say that all the variables must sum up to 1</span></b>. This <b><span style='color: #98FB98'>force uniqueness</span></b>.

>[!failure] It is very slow to solve the multiple flow equations for larger sized graphs like the web
<div style="page-break-after: always;"></div>

##### Power Iteration

A faster way to compute the rank is to use [[Year 1/Sem 2/MA1522 - Linear Algebra for Computing/Matrices.md#Matrix Multiplication|matrix multiplication]].  First we need to compute the [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs.md#Adjacency Matrix|adjacency matrix]].

If **for all webpages** ($i$) there is a edge going from $i \rightarrow j$ then our adjacency matrix ($M_{j, i}$) = $1 / d_{i}$, (*the number of out links*), else it will be 0.

>[!important] We read the matrix as from col it has an edge to a row.

>[!info] This matrix $M$ is a stochastic matrix
>Meaning the <b><span style='color: #F0E68C'>columns all sum up to 1</span></b>. If there are outgoing edges.

Then we need to get the <b><span style='color: #B0E0E6'>rank vector</span></b> ($r$), which is just a <b><span style='color: #F0E68C'>vector of the ranks of all webpages at that time</span></b> ($t$) of <b><span style='color: #F0E68C'>size n by 1</span></b>. And also like in our [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Graphs & Page Rank.md#"Flow" Model|flow model]], to make the solution unique we can ensure that the sum of all the ranks will be equal to 1.

Then finally our flow equations are now represented in a matrix form and can be written as such:
$$
r_{t + 1} = M  \cdot r_{t}
$$

So power iteration is to <b><span style='color: #F0E68C'>continuously</span></b> do this matrix multiplication to <b><span style='color: #F0E68C'>update the importance of each page</span></b>. 

We only **stop** when the difference between the <b><span style='color: #F0E68C'>update</span></b> from time $t$ and $t + 1$ <b><span style='color: #F0E68C'>is minimal</span></b>. So when:
$$
\vert r_{t+1}- r_{t} \vert_{1} \lt \epsilon
$$
Where:
- $\vert x \vert_{1}$ is the [[Year 2/Sem 1/DSA3361 - Inferential Data Analytics/Regularisation Techniques.md#LASSO Regression|L1 normalisation]], you <b><span style='color: #F0E68C'>can use any other vector normalisation</span></b> like Euclidean
- $\epsilon$ is our update threshold, if our update is change is smaller then we will stop

>[!important] It is not always we must meet this threshold $\epsilon$ we can also fix the number of iterations if we don't have enough processing power

>[!question] Then what is the rank of each page at time 0?
>Suppose we have $N$ pages then we can initialise each webpage rank to be $1 / N$.
>
>It <b><span style='color: var(--mk-color-red)'>cannot be 0 because if it is then our ranks will never update</span></b>.
#### Random Walk Formulation

![[PageRank Random Walk Example.png|center]]

A random walk is essentially starting at a random node at t = 0 and then make random moves based on the graph structure.

So at **time t = 0**, if we have $N$ nodes then <b><span style='color: #F0E68C'>start at a random node with equal probability</span></b> ($1 / N$).

Then at **time t = 1**, we can <b><span style='color: #F0E68C'>move to another node given the out links</span></b> (*neighbours*) with <b><span style='color: #F0E68C'>equal probability</span></b>.

>[!example] Example using our sample graph
>At t = 0 we have a 1/3 chance of starting at nodes a, m or y. So lets say we start at node a
>
>Then we have a 50% chance of moving to y or m.

So let $p(t)$ be a vector which indicates the <b><span style='color: #F0E68C'>probability of the person is at the ith node at time t</span></b>.

>[!example] Example of finding the probability at t = 1
>So lets say we want to find the probability of the person being at node a.
>
>The 2 ways are if the person start on either y or m and then they move to a.
>
>So the probability will be, $1 / 3 \times 1$ (*m to a*) $+ 1 / 3 \times 1 / 2$ (*y to a*), which will give us a probability of $1 / 2$.

So as **time goes to infinity**, the probability distribution approaches a steady state, representing a <b><span style='color: #F0E68C'>long term probability for each node which will be the page rank scores.</span></b>. This is known as <b><span style='color: #B0E0E6'>stationary distribution</span></b>.

$$
p(t + 1) = M \cdot p(t)
$$

>[!info] This is exactly the same as our "flow" formulation
>
>The more in links the node has the higher the probability that the person will arrive at that node.
# Page Rank With Teleports
---
There are 2 ways to compute the importance of a page, however there are some questions about our formula:
- Does it converge?
- Does it converge to what we want?
- Are the results reasonable?

The answer to these questions is  <b><span style='color: var(--mk-color-red)'>no</span></b>, with the methods that were introduced.

The reason why this is so is because of:
![[Dead End & Spider Trap Example.png|150]]

1) **Dead ends**

So dead ends are <b><span style='color: #F0E68C'>nodes with no out links</span></b>. This means that the random walk will reach a point where it cannot move anywhere

So after an **infinite amount of updates** it will result in the <b><span style='color: var(--mk-color-red)'>all nodes will only have a rank values of 0</span></b>.

>[!failure] Dead ends will make the matrix not stochastic 

2) **Spider traps**

A spider trap is a <b><span style='color: #F0E68C'>proper subset</span></b> (*cannot be equal to the whole graph*) where <b><span style='color: #F0E68C'>no matter which out-link you take you will remain in this subset of nodes</span></b>.

There are **2 types** of spider traps:
1) **One node** spider trap: It is where the node has one out-link pointing to itself
2) **Multiple node** spider trap: It consist of multiple nodes that follows the above constraint

So after an **infinite amount of updates** it will result in the <b><span style='color: var(--mk-color-red)'>nodes only having values within the cycle</span></b> (*the cycle absorbs all the importance*), those that are not will be close to 0.

>[!failure] With spider traps, it makes the matrix reduceable so the solution is not unique

So the <b><span style='color: #98FB98'>solution</span></b> to these 2 scenarios are <b><span style='color: #B0E0E6'>teleports</span></b>. So initialise a probability $\beta$ which denotes the <b><span style='color: #F0E68C'>probability</span></b> where the walker will <b><span style='color: #F0E68C'>follow the edge</span></b> to the next node. And $1 - \beta$ that it will <b><span style='color: #F0E68C'>teleport to a random node</span></b>.

Only for **dead ends**, we will set $\beta$ <b><span style='color: #F0E68C'>to be 1</span></b> (*or just preprocess the graph to have a out link to all other nodes*), so our walker will always teleport. We can just **adjust** the [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Graphs & Page Rank.md#Power Iteration|stochastic matrix]] to have a <b><span style='color: #F0E68C'>equal probability to jump to any of the nodes</span></b>.

>[!note] A common value for $\beta$ is 0.8 to 0.9

So here is the updated **page rank equation with teleport**:
$$
r_{j} = \sum_{i \rightarrow j}  \beta\frac{r_{i}}{d_{i}} + (1 - \beta) \frac{1}{N}
$$
Where:
- $N$ is the number of nodes or webpages
- $\beta$ is the probability that the walker follows the link at random

We can also do the same with the **matrix representation**, but now we form a matrix $A$ as follow:
$$
A = \beta M + (1 - \beta) [\frac{1}{N}]_{N \times N}
$$
Where:
- $[1 / N]_{N \times N}$ is a n by n matric where all entries are $1/N$
- $M$ is our stochastic matrix

>[!important] Then our equation will be $r = A \cdot r$.

>[!success] Teleporting helps converge faster than with no teleport if there are spider traps or dead ends
>This is because it allows the random walker to <b><span style='color: #F0E68C'>spread out the importance factors</span></b> among all the nodes in the graph.
# Topic Specific Page Rank
---
We can evaluate web pages not just according to their popularity in general but **how popular is it based on a given topic**?

We can **augment the page rank with teleport**  to only allow our walker to <b><span style='color: #F0E68C'>teleport witihin a set of relevant pages</span></b>. This is known as the <b><span style='color: #B0E0E6'>teleport set</span></b> ($S$).

>[!info] Teleport set means that if the walker can teleport to any node within this set

So all we have to do now is to **augment the formula to compute the google matrix to be** to:
$$
A_{i, j} =
\begin{cases}
\beta M_{i,j} + (1 - \beta) / |S|,  & \text{if $i \in S$} \\
\beta M_{i,j} + 0, & \text{otherwise}
\end{cases}

$$
Where:
- $S$ is our teleport set
- $i$ is our row and $j$ is the column, so it is read as from $j$ there is an edge to $i$

>[!note] This makes $A$ stochastic

>[!note] Each page in the set has a equal probability or it can be assigned different weights

>[!important] This choice of the teleport set and probability of teleport affects the rank
>If we have a **teleport set of only 1 page** it will <b><span style='color: #F0E68C'>boost its rank</span></b> compared to a set of all pagers.
>
>While having the same teleport set but with a **higher probability of teleport** will also <b><span style='color: #F0E68C'>boost the ranks within this set</span></b> as during random walk, it will teleport to these pages more frequently.
## Discovering the Topic Vector

So how do we form the teleport set based on the topic? Some <b><span style='color: #F0E68C'>websites previously provides the topics</span></b> for the different webpages (*DMOZ*).

Now it is better to **let the user choose the topic** they want to search for. They can <b><span style='color: #F0E68C'>pick from a menu</span></b> or we can let <b><span style='color: #F0E68C'>LLMs to classify the query</span></b> into a topic.

>[!failure] Heavy reliance on context
>Sometimes the query might not have enough context. For example if the user search "Computer".
>
>A fallback will be to <b><span style='color: #F0E68C'>use the user's history or bookmarks to get additional context</span></b>.
# Page Rank Implementation
---
Page rank revolves around graphs and most **graph algorithms are implemented** in such a way that it is from the <b><span style='color: #F0E68C'>view of a single vertex, performing one iteration</span></b> (*one hop*) based on messages (*weights*) <b><span style='color: #F0E68C'>from its neighbours</span></b>.

So the upcoming page rank implementation, the **user only needs to produce** a `compute` function to <b><span style='color: #F0E68C'>describe the behavior at one vertex</span></b> in one step, while the <b><span style='color: #F0E68C'>rest is abstracted away by the framework</span></b> (*scheduling / implementation details*).
## Pregel
### Computational Model

It is the <b><span style='color: #87CEEB'>graph processing system implemented by google</span></b>. Another similar but open-source implementation is <b><span style='color: #87CEEB'>Giraph</span></b> by Facebook / Meta.

In Pregel, **one computation** consist of a series of <b><span style='color: #B0E0E6'>super steps</span></b>. 1 super step is <b><span style='color: #F0E68C'>invoking the user-defined</span></b> `compute` <b><span style='color: #F0E68C'>function for each vertex</span></b>.

>[!info] Each call on the `compute` function can be done in parallel
>Although it runs in parallel, it <b><span style='color: #FFD700'>follows a synchronous execution model</span></b>. So once everything is done then the next super step can begin.

At super step $s$, a vertex can **read messages** sent to them in super step $s - 1$. It can then **send messages** (*no guarantee in ordering*) to its neighbours which will be read in super step $s + 1$.

A vertex can <b><span style='color: #F0E68C'>deactivate itself when a condition is met</span></b>. And similarity it can <b><span style='color: #F0E68C'>reawake itself when a new message is received</span></b>.

>[!important] Computation terminates when all vertices are inactive or are deactivated
>
>And how vertex gets deactivated it all depends on the `compute` function provided by the user.
### Implementation

Pregel uses a <b><span style='color: #F0E68C'>master & worker architecture</span></b>. By default, <b><span style='color: #F0E68C'>each vertices in a graph are partitioned</span></b> using <b><span style='color: #B0E0E6'>edge cuts</span></b> and <b><span style='color: #F0E68C'>assigned to workers</span></b>.

**Example of an edge cut**:
![[Edge Cut Example.png|center|200]]

>[!abstract] Workers in Pregel
>Here **computation and state management** of the portion of the graph is <b><span style='color: #F0E68C'>all done in memory</span></b>.
>
>And it also does **checkpointing** into a <b><span style='color: #F0E68C'>persistent storage</span></b>.
>
>Messages are sent within or between workers. These **messages** are <b><span style='color: #F0E68C'>buffered locally and sent as a batch</span></b> to <b><span style='color: #98FB98'>reduce network traffic</span></b>.

Pregel also has its own **fault tolerance** mechanism, and similarly it does regular checkpointing. But <b><span style='color: #F0E68C'>fault is detected through heartbeats</span></b> (*a signal*) from workers. And if a worker is corrupted, the <b><span style='color: #F0E68C'>vertices will be reassigned and reloaded from checkpoints</span></b>. 
### Page Rank in Pregel

To compute page rank in Pregel it will repeatedly do these 3 steps:
1) **Invoke** the `compute` function on all vertices
2) Aggregate the messages and **compute the page rank update**
3) Send the updated rank as a **message to outgoing neighbours**

**Page Rank code in Pregel**
![[Page Rank Algorithm in Pregel.png|center|550]]

**Another example of the Page Rank Algorithm in Pregel**:
![[Example 2 of Page Rank Algorithm in Pregel.png|center|500]]

In general our **input to the compute is a vertex and a list of messages** for that vertex.

Our termination conditions in this example is when the super step count is greater than 30, but we can also deactivate a node when the [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Graphs & Page Rank.md#Power Iteration|update is minimal]].
## Spark for Graphs

So spark created something called **GraphX**, which extends the RDDs to resilient distributed <b><span style='color: #B0E0E6'>property graphs</span></b>. And there is also **Graphframe** which is the same but for the data frame.

>[!info] Property Graphs
>It presents different views of the graphs (*in terms of vertices, edges, triplets*).

So in spark, all **vertices** are stored in a <b><span style='color: #B0E0E6'>vertex table</span></b> (*every node and their properties*) and all **edges** are stored in a [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs.md#Edge List|edge list]] and also the property of the edge (*maybe like similar to, contains relationships*).

So with these 2 tables spark can create a <b><span style='color: #B0E0E6'>triplets table</span></b>. Which is essentially the <b><span style='color: #F0E68C'>properties of 2 vertices and the relationship between them</span></b>.

>[!tldr] Computing the rank
>![[Example of Using Spark to Compute Page Rank.png|center|500]]
>
>With the triplets we can do a `group by` and a  `sum` to compute the rank of the page (*this is equivalent to the formula to compute rank*) .

Because if the nature of the **triplets**, for Spark they <b><span style='color: #F0E68C'>partition the graph using a vertex cut</span></b> (*we need the connection between the edges and the nodes*).

**Example of a vertex cut**:
![[Vertex Cut Example.png|center|150]]

So **after partitioning the graph**, our <b><span style='color: #F0E68C'>vertex & edge table will essentially be partitioned</span></b> also. In addition to this we also need a <b><span style='color: #B0E0E6'>routing table</span></b>. This routing table is there to let Spark know <b><span style='color: #F0E68C'>which vertices are in which partition</span></b>.

>[!warning] When using vertex cut, there might be 2 vertices in 2 different partitions
>This is why we need the routing table as well to know which vertices are in 2 or more partitions.

>[!failure] It is slower than Pregel and Giraph
>As Spark is using micro batch processing to do graph processing as compared to the other 2 which mainly focus on graph processing.
>
>But if your tasks are to do **all streaming, batch and graph processing**, <b><span style='color: #98FB98'>Spark can be a better choice</span></b> for its many applications.

