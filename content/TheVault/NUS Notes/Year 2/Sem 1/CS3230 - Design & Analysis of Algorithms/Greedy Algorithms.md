---
title: Greedy Algorithms
Date Created: 2024-10-08
Last Updated: 2025-09-28
tags:
  - CS3230
  - AlgorithmDesign
---
# What is Greedy
---
Similarly like with **divide and conquer** and **dynamic programming** we want to <span style='color:var(--mk-color-orange)'>break</span> the original problem into <span style='color:var(--mk-color-orange)'>smaller sub problems</span>.

But for a greedy algorithm, we want to do the same but we <b><mark style='background:var(--mk-color-yellow)'>only look into one specific subproblem</mark></b>, which happens to also be the <span style='color:var(--mk-color-green)'>correct solution</span>.

This will be <span style='color:var(--mk-color-green)'>very fast</span> as compared to D&C and DP, but <span style='color:var(--mk-color-red)'>provided it works</span> (*Not all problems can be greedily solved*).

We will also need to define a <span style='color:var(--mk-color-yellow)'>optimal sub structure</span>, which is essentially saying the following:
- Assume that this **solution is the most optimal**
- And lets say in actually there is <span style='color:var(--mk-color-orange)'>another more optimal solution</span>
- Then there will be a <span style='color:var(--mk-color-green)'>better subproblem</span> + $c$ which will be <span style='color:var(--mk-color-green)'>better than the proposed solution</span> in point 1 (*cut and paste*)
# Exchange Argument
---
To prove that our proposed <span style='color:var(--mk-color-teal)'>greedy algorithm</span> works we need to show that our choice of subproblem (*Singular*) is the correct one and <span style='color:var(--mk-color-green)'>yields the correct solution</span>.

This is where the<span style='color:var(--mk-color-turquoise)'> exchange argument</span> comes in. Essentially this argument shows that, <span style='color:var(--mk-color-orange)'>given a correct and optimal solution</span> to a problem, your <span style='color:var(--mk-color-yellow)'>greedy solution can replace this solution and still get the same answer</span>.

**Example using the fractional knapsack problem**:

Let $j^{*}$ be the item with the **maximum** $v_{j}/w_{j}$, thus there **exists a optimal problem containing** $min(w_{j^{*}}, W)$ of item $j^{*}$.

Let the <span style='color:var(--mk-color-green)'>optimal solution be</span> $x_{1} + x_{2} + x_{3} + \dots  + x_{n} = min(w_{j^{*}}, W)$

We can <span style='color:var(--mk-color-orange)'>rewrite the solution</span> as such, $x_{1} \times \frac{v_{1}}{w_{1}} + x_{2} \times \frac{v_{2}}{w_{2}} + \dots + x_{n} \times \frac{v_{n}}{w_{n}}$

Which is **smaller than or equals** to $x_{1} \times \frac{v_{j^{*}}}{w_{j^{*}}} + x_{2} \times \frac{v_{j^{*}}}{w_{j^{*}}} + \dots + x_{n} \times \frac{v_{j^{*}}}{w_{j^{*}}}$ (*Replace value/weight with $v_{j^*}/w_{j^*}$*).

**Simplifying** the equation, $(x_{1} + x_{2} + \dots + x_{n}) \times \frac{v_{j^{*}}}{w_{j^{*}}}$. This then just the $min(w_{j^{*}}, W) \times \frac{v_{j^{*}}}{w_{j^{*}}}$.
## Binary Encoding

In general the <span style='color:var(--mk-color-green)'>most optimal way</span> to <span style='color:var(--mk-color-orange)'>encode a text with</span> $m$ characters is $m \lceil \log_{2} n \rceil$.

There are <span style='color:var(--mk-color-orange)'>2 ways</span> to **encode characters into binary**:
1) **Fixed length** - 26 characters we just need 5 bits ($2^{5} = 32$ *unique combination*)
2) **Variable length encoding** - **Set common characters** (*frequency*) like "e" to have <span style='color:var(--mk-color-yellow)'>shorter bit length</span>

> [!warning] Issues with the Encoding Techniques
> Obviously **fixed length encoding** is <span style='color:var(--mk-color-red)'>not optimal</span> as every character uses $x$ bits.
> 
> As for **variable length encoding**, it give rise to ambiguity. Lets set the following characters to these binary string:
> - "e": 0
> - "a": 01
> - "g": 101
>   
> Now if I were to give u a binary string of, 0101, <span style='color:var(--mk-color-red)'>we have many possible answers</span>,
> 1) eg
> 2) aa

To solve these issues, <span style='color:var(--mk-color-teal)'>prefix encoding</span> can be used. Essentially, any **character's binary mapping** <span style='color:var(--mk-color-red)'>cannot be a prefix</span> of **another characters binary mapping**.

We can <span style='color:var(--mk-color-orange)'>encode this mapping</span> into a <span style='color:var(--mk-color-purple)'>binary tree structure</span>. And to prevent prefixes, all <span style='color:var(--mk-color-yellow)'>encoding must be done at the leaves</span>.

Thus the average bit length (ABL) was from $\sum_{x \in A} f(x) \cdot \vert y(x) \vert$. Where $y(x)$ is the **length of the encoding** to:
$$
ABL(y) = \sum_{x \in A} f(x) \cdot \text{depth}_{T}(x)
$$
Some <span style='color:var(--mk-color-orange)'>additional observations</span> is that the **tree must be** a <span style='color:var(--mk-color-yellow)'>full binary tree</span> where every node has 2 children (For <span style='color:var(--mk-color-green)'>optimality</span>).

**Visualising the binary tree**
![[Prefix Encoding Visualised on a Binary Tree.png|center|400]]

Here are some **observations that can be made**:
1) If $a_{i}$ is at the deepest level and $i > 2$, then we can <span style='color:var(--mk-color-yellow)'>always swap it with either</span> $a_{1}$ or $a_{2}$ and the average bit <span style='color:var(--mk-color-green)'>length will still be equals to or smaller</span> 
2) And there <span style='color:var(--mk-color-yellow)'>exist an optimal prefix encoding</span> where $a_{2}$ and $a_{1}$ are siblings and by the <span style='color:var(--mk-color-turquoise)'>exchange argument</span>, this can be replaced to get a same solution.

Thus here is where <span style='color:var(--mk-color-teal)'>Huffman's algorithm</span> comes in, **essentially we can merge the frequency** of $a_{1}$ and $a_{2}$ to make $a'$, this reduces the problem by $n - 1$ and thus we can recursively do this $n$ times by <span style='color:var(--mk-color-yellow)'>merging the 2 least frequent characters</span>.

![[Huffman's Algorithm.png|center|450]]