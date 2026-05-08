---
title: All Pair Shortest Path
Date Created: 2023-07-25
tags:
  - CS2040
  - Algorithms
  - Graphs
---
Is to find all the shortest paths of all vertices to all other vertices

This is known as parameter of the graph.


We can get APSP by using a SSP algorithm on all vertices. 

**Floyd Warshall**

Instead of a distance array, it will use a 2D distance matrix

Set all `D[i][i]` = 0 and set `D[i][j]` = weight(i,j)

If some path from i to j is longer than from i to k to j, then replace the shortest path


The K for loop at the start will include additional intermediate vertices for each iteration

To print the shortest path just use a 2D predecessor matrix, when initializing all the columns in the row will be the row index

Thus need to also check of `D[i][j]` != INF