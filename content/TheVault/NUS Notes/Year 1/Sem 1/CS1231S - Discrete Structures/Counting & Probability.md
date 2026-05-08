---
Title: Counting & Probability
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1231S
  - Math/Probability
  - Math/Logic
---
# Definitions
---
**Random Event**
> It means that when something happens, <span style='color:#f7b731'>one outcome</span> from the set of outcomes is <span style='color:#f7b731'>sure to occur</span> but it is <span style='color:#f7b731'>impossible to predict with certainty</span>

**Sample Space**
> Set of all possible outcomes of a random process or experiment

**Event**
> A subset of a sample space

**Equally Likely Probability Formula**
> S is a finite sample space where all outcomes are equally likely and E is an event in S, thus the probability of E is denoted as P(E)

$$P(E) = \frac{\vert E \vert}{\vert S \vert} = \frac{\text{Total number of outcomes in E}}{\text{Total number of outcomes in S}}$$ 
**Theorem 9.1.1 The Number of Elements in a List**
> If m and n are integers and $m \le n$ and the <span style='color:#f7b731'>numbers between m and n are all present</span>, then there are $n - m + 1$ integers from m to n <span style='color:#f7b731'>inclusive</span>

# Possibility Tree
---
A <span style='color:#0fb9b1'>tree structure</span> is a useful tool for keeping systematic track of all possibilities in situations in which events happen in order.

## Multiplication / Product Rule

If an operation which consist on k steps and can be performed in n ways for each kth step, then the entire operation can be performed in $$n_{1}\times n_{2} \times n_{3} \times \dots \times n_{k}$$
# Permutations
---
A <span style='color:#0fb9b1'>permutation</span> of a <span style='color:#f7b731'>set of objects is an ordering of the objects in a row</span>. For example, the set of elements a, b, and c has six permutations. It is also called <span style='color:#0fb9b1'>r-permutation</span>.

**Theorem 9.2.2 Permutations**
> The number of permutations of a set with n ($n \ge 1$) elements is $n!$

Note that $0! = 1$
## Permutations of Selected Elements

An <span style='color:#0fb9b1'>r-permutation</span> of a set of <span style='color:#f7b731'>n elements</span> is an <mark class="hltr-orange">ordered selection</mark> of <span style='color:#f7b731'>r elements taken from the set</span>

The number of r-permutations of a set of n elements is denoted $P(n, r)$. If <span style='color:#f7b731'>repetition is allowed</span> it will be $n^{k}$

**Theorem 9.2.3 r-permutations from a set of n elements**
> If n and r are integers and $1 \le r \le n$, then the number of r-permutations of a set of n elements is given by the given formula 

$$P(n,r) = n(n-1)(n-2) \dots (n-r+1) \text{ or } P(n,r) = \frac{n!}{(n-1)!}$$
# Counting Elements of Disjoint Sets
---
## Addition / Sum Rule

The <span style='color:#0fb9b1'>addition rule</span> (or sum rule) states that the number of elements in a union of <span style='color:#f7b731'>mutually disjoint finite sets</span> equals the <span style='color:#f7b731'>sum of the number of elements in each of the component sets</span>

**Theorem 9.3.1 The Addition / Sum Rule**
> Suppose a finite set A equals the union of k distinct mutually disjoint subsets $A_{1}, A_{2}, \dots, A_{k}$ then $\vert A \vert = \vert A_{1} \vert + \vert A_{2}\vert + \dots + \vert A_{k} \vert$

## Difference Rule

The <span style='color:#0fb9b1'>difference rule</span> allows the computation of the number of elements that are in <span style='color:#f7b731'>one set and not in another set</span>

**Theorem 9.3.2 The Difference Rule**
> If $A \subseteq A$ then $\vert A \backslash B \vert = \vert A \vert - \vert B \vert$ 

**Formula for the Probability of a complement event**
> If S is a finite sample space and A is an event in S, then $P(\bar A) = 1 - P(A)$

## Inclusion / Exclusion Rule

The <span style='color:#0fb9b1'>addition rule</span> <span style='color:#f7b731'>did not account for sets that overlap one another</span> thus to get an accurate number of elements in 2 sets, it is necessary to subtract the number of elements in both the sets

**Theorem 9.3.3 The Inclusion / Exclusion Rule for 2 or 3 sets**
>  $\vert A \cup B \vert = \vert A \vert + \vert B \vert - \vert A \cap B \vert$ 
>  $\vert A \cup B \cup C \vert = \vert A \vert + \vert B \vert + \vert C \vert - \vert A \cap B \vert - \vert A \cap C \vert - \vert B \cap C \vert + \vert A \cap B \cap C \vert$ 

# Pigeonhole Principle (PHP)
---
This principle states that if $n$ pigeons fly into $m$ pigeonholes and $n \gt m$, then <span style='color:#f7b731'>at least one hole must contain two or more pigeons</span>.

Therefore the actual definition of the principle is
> A function from <span style='color:#f7b731'>one finite set to a smaller finite set cannot be one-to-one</span>: There must be at least 2 elements in the domain that have the same image in the co-domain.

**Generalized PHP**
> For any function f from a finite set $X$ with $n$ elements to a finite set $Y$ with $m$ elements and for any positive integer $k$, if $k \lt n/m$, then there is some $y \in Y$ such that $y$ is the image of at least $k + 1$ distinct elements of $X$

**Contrapositive Generalized PHP**
> For any function $f$ from a finite set $X$ with $n$ elements to a finite set $Y$ with $m$ elements and for any positive integer $k$, if for each $y \in Y, f^{–1}({y})$ has at most $k$ elements, then $X$ has at most $km$ elements; in other words, $n \le km$.

The contrapositive principle is stating that if each element in the co-domain has $n$ items and there are $m$ elements in the co-domain, then the domain will have at most $xy$ elements. As <span style='color:#eb3b5a'>if there is more then it will not be a function</span> any more as some $x$ will not be mapped to some $y$
## Application to Decimal Expansions

**Terminating Decimal** : 3.654 
**Repeating Decimal** : $2.81\overline {246} = 2.81246246246246\dots$ 

If there is one <span style='color:#f7b731'>remainder</span> during long division that is <span style='color:#f7b731'>equals to 0</span> then the decimal terminated. Else it is a repeating decimal

# Combinations
---
Also called <span style='color:#0fb9b1'>r-combination</span> is a subset of $r$ out of the $n$ elements in the set. It is basically <span style='color:#f7b731'>how many subsets of a particular size can be formed from a set</span>, where <mark class="hltr-orange">order does not matter</mark>

The symbol to denote this is ${n \choose r}$ which can be read as n choose r. Another symbol is $C(n,r)$ or any other symbol with $C$.

**Theorem 9.5.1 Formula for ${n \choose r}$**
> The general formula to calculate the number of combinations is given by the following

$${n \choose r} = \frac{P(n,r)}{r!} = \frac{n!}{r!(n-r)!}$$

Where:
1)  $n$ and $r$ are non-negative integers
2)  $r \le n$

**Theorem 9.5.2 Permutations with sets of indistinguishable objects**
> Suppose a collection of $n$ objects where $n_k$ are <span style='color:#f7b731'>all the elements of type k and are indistinguishable</span>.  Then the number of distinguishable permutations (no repeat) is

$$\frac{n!}{n_{1}!  n_{2}!  \dots n_{k}!}$$
Where:
1) $n_{k}$ is the number of repeated elements of the same type

## MultiSet

It is an <span style='color:#0fb9b1'>r-combination</span> with <span style='color:#f7b731'>repetition allowed</span>, or multiset of size r, chosen from a set X of n elements is an unordered selection of elements taken from X with repetition allowed.

Now the r can be bigger than n

If $X = \{x_1,x_2,\dots,x_n\}$, we write an r-combination with repetition allowed as $[x_{i1},x_{i2},\dots,x_{ir}]$ where each $x_{ij}$ is in $X$ and some of the $x_{ij}$ may equal each other.

**Theorem 9.6.1 Number of r-combinations with repetition allowed**
> The number of <span style='color:#f7b731'>r-combination with repetition allowed</span> (multisets of size r) that can be selected from a set of n elements is

$$r+n-1 \choose r$$

# Pascal Formula
---

**Theorem 9.7.1 Pascal's Formula**
> Let $n$ and $r$ be positive integers, $r \le n$ then;

$${n+1 \choose r} = {n \choose r-1} + {n \choose r}$$

This can be proof using <span style='color:#0fb9b1'>combinatorial proof</span>, which is mainly used in P&C. This includes 2 types of proofs
- Bijective Proof
	The same as proving that two sets $𝑋$ and $𝑌$ have the <span style='color:#f7b731'>same cardinality by deriving a bijective function</span> that maps each element in $𝑋$ to each element in $𝑌$

- Proof by Double Counting
	Counting the number of elements in two different ways to obtain the different expressions in the identity

The proof for **theorem 9.7.1** is as follows;

1. ${n+1 \choose r}$: choosing subsets of r elements from a set $A$ of $n+1$ elements
2. Let $x$ be an element in $A$. A subset may or may not have $x$
3. Case 1: If the subset has $x$, then there are ${n \choose r - 1}$ ways of choosing these subsets
4. Case 2: If the subset does not have $x$, then there are  ${n \choose r}$ ways of choosing these subsets
5. Therefore, there are ${n \choose r - 1} + {n \choose r}$ ways of choosing subset of $r$ elements from $n+1$ elements

**Lecture 11 Example 8 on Slide 29**
> For all non-negative integers $n$ and $r$ with $r \le n$, by interpreting it as saying that a set $A$ with $n$ elements has <span style='color:#f7b731'>exactly as many subsets</span> of size $r$ as it has subsets of size $n – r$

$${n \choose r} = {n \choose n-r}$$
$$k{n \choose k} = n{n-1 \choose k-1} \text{ for } 0 \le k \le n$$
Think of the above as either choose, $k$ elements from n and then choose one from the selected $k$ elements, or choose one of the n elements first then choose the remaining $k - 1$ from $n - 1$ elements. This is known as <span style='color:#0fb9b1'>double counting</span>

# Binominal Theorem
---
It is a formula which gives an <span style='color:#f7b731'>expression for the powers of a binomial</span> $(a + b)^{n}$ $$(a + b)^{n}= \sum_{k=0}^{n} {n \choose k} a^{n-k}b^{k} = a^{n} + {n \choose 1}a^{n-1}b^{1} + {n \choose 2}a^{n-2}b^{2} + \dots +{n \choose n-1}a^{1}b^{n-1} + b^{n}$$
Where :
- $n$ is some real integer
- $a$ and $b$ are all real numbers
- ${n \choose r}$ is the <span style='color:#0fb9b1'>binominal coefficient</span>

# Probability Axioms and Expected Values
---

**Probability Axioms**
> Let $S$ be a sample space. A <span style='color:#0fb9b1'>probability function</span> $P$ from the <span style='color:#f7b731'>set of all events</span> in $S$ <span style='color:#f7b731'>to the set of real numbers </span>satisfies the following axioms: 

For all events A and B in S;
1)  $0 \le P(A) \le 1$
2)  $P(\emptyset) = 0$ and $P(S) = 1$
3)  If $A$ and $B$ are disjoint events ($A \cap B = \emptyset$) then $P(A \cup B) = P(A) + P(B)$

**Probability of a Compliment Event**
> if A is any event in a sample space S then, $P(\bar A) = 1 - P(A)$

**Probability of a General Union of Two events**
> $P(A \cup B) = P(A) + P(B) - P(A \cap B)$ This is a more general formula

**Probability of something is twice as likely**
> If something is twice as likely, just treat it as 2 items and change accordingly
## Expected Value

Suppose the possible <span style='color:#f7b731'>outcomes of an experiment</span>, or random process, are <span style='color:#f7b731'>real numbers</span> $a_{1},a_{2},a_{3},\dots,a_{n}$ which <span style='color:#f7b731'>occur with probabilities</span> $p_{1},p_{2},p_{3},\dots,p_{n}$ respectively. The <span style='color:#0fb9b1'>expected value</span> of the process is $$\sum_{k=1}^{n}a_{k}p_{k} = a_{1}p_{1} + a_{2}p_{2} + \dots + a_{n}p_{n}$$
## Linearity of Expectation

The expected value of the sum of random variables is equal to the <mark class="hltr-orange">sum of their individual expected values</mark>, regardless of whether they are independent. Thus;
$$E[X + Y] = E[X] + E[Y]$$

Where :
- $E$ is the expected value

In a more general form $$E\left[\sum_{i = 1}^{n} c_{i} \cdot X_{i}\right]= \sum\limits_{i=1}^{n} (c_{i} \cdot E[X_{i}])$$
Where :
-  $E$ is the expected value
-  $c_{i}$ is some constants

# Conditional Probability
---
Let $A$ and $B$ be events in a sample space $S$. If $P(A)\neq 0$, then the <span style='color:#0fb9b1'>conditional probability </span>of $B$ given $A$, denoted  $P(B|A)$, is $$P(B|A) = \frac{P(A \cap B)}{P(A)}$$
With this basic manipulation, the $P(A)$ can be found as well

# Bayes Theorem

**Theorem 9.9.1 Bayes' Theorem**
> Suppose that a sample space $S$ is a <span style='color:#f7b731'>union of mutually disjoint events</span> $B_{1} , B_{2}, B_{3}, \dots, B_{n}$. Suppose $A$ is an event in $S$, and suppose $A$ and all the $B_{i}$ have non-zero probabilities then; 

$$P(B_{k}|A) = \frac{P(A|B_{k}) \cdot P(B_{k})}{P(A|B_{1}) \cdot P(B_{1}) + \dots + P(A|B_{n}) \cdot P(B_{n})}$$
Where :
- $k$ is an integer between $1 \le k \le n$

**False Positive**
> It is a result that indicates that something has happen but actually it did not

**False negative**
> It is a result that indicates that something has not happen but actually did

# Independents Events

Let $A$ and $B$ be the events in a sample space $S$, then $A$ and $B$ are <span style='color:#0fb9b1'>independent</span>, if and only if, $$P(A \cap B) = P(A) \cdot P(B)$$
## Pairwise Independent / Mutually Independent

Let $A$, $B$ and $C$ be the events in the sample space $S$ then they are <span style='color:#0fb9b1'>pairwise independent</span> if and only if 
1) $P(A \cap B) = P(A) \cdot P(B)$
2) $P(A \cap C) = P(A) \cdot P(C)$
3) $P(B \cap C) = P(B) \cdot P(C)$

Then if they are <span style='color:#0fb9b1'>mutually independent</span> if and only if <mark class="hltr-orange">they satisfy all the above 3 points</mark> and if, and only if, the probability of the <span style='color:#f7b731'>intersection of any subset of the events</span> is the <span style='color:#f7b731'>product of the probabilities of the events in the subset</span>
4) $P(A \cap B \cap C) = P(A) \cdot P(B) \cdot P(C)$

An **example** of an event that is pairwise independent but is not mutually independent

Let 
- $A$ be the sum of throwing 2 dice to be 7
- $B$ be the first dice to be 3
- $C$ be the second dice to be 4

$P(A) = P(B) = P(C) = \frac{1}{6}$
$P(A \cap B) = P(A) \cdot P(B) = \frac{1}{36}$
$P(A \cap C) = P(A) \cdot P(C) = \frac{1}{36}$
$P(B \cap C) = P(B) \cdot P(C) = \frac{1}{36}$

Therefore, from the example above they are <span style='color:#0fb9b1'>pairwise independent</span>, however, $P(A \cap B \cap C) = \frac{1}{36}$ but $P(A) \cdot P(B) \cdot P(C) = \frac{1}{216}$ Therefore it is <span style='color:#eb3b5a'>not mutually independent </span>

The reason for this is that <span style='color:#f7b731'>the probability for one of the events will be 1 given the other 2 events</span>. For example if A and B happens then C is guarantee to happen as to get a 7 from 3 is only the number 4