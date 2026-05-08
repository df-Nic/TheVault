---
Title: Dynamic Programming
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - Algorithms/DynamicProgramming
---
Dynamic Programming is a way to trade space for a better time complexity.

Basically, we have a table which we can compute from top to bottom to give us our result. This will take **O(n)**.

```Python
def dp_choose(n,k):
	row = [1] * (k+1)
	table = []

	for i in range(n+1): # Make a table with all 1's
		table.append(row.copy())

	for j in range(1,k+1): # Fill the first row with 0s
		table[0][j]

	for i in range(1,n+1): # Fill the rest of the table
		for j in range(1,k+1):
			table[i][j] = table[i-1][j-1] + /
							table[i-1][j]

	return table[n][k]
```

**Difference between memoization and dynamic programming**

- DP required more computations
- Programmers need to know which entries need to be computed
- DP can be more space efficient for some problems.