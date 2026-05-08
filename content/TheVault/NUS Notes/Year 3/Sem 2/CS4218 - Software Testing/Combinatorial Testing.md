---
Title: Combinatorial Testing
Date Created: 18-February-2026
Last Updated: 01-May-2026
Tags:
  - CS4218
  - SWE/Testing/CombinatorialTesting
---
# Motivation Behind Combinatorial Testing
---
Rarely will a program or function accepts only 1 input variable. For each test case, we need 1 value for each input variable.

Certain **faults** (*critical ones event*) **occur** due to <b><span style='color: #FFD700'>specific interactions between values of different variables</span></b>.

Many of our **previous test generation techniques fail to consider these interactions**:
- [[Year 3/Sem 2/CS4218 - Software Testing/Test Generation Techniques.md#Equivalence Partitioning (EP)|Equivalence partitioning]]

It raises the possibility of a large number of subdomains in the partition. The number of <b><span style='color: var(--mk-color-red)'>subdomains in a partition of the input domain increases with number and type of input variables</span></b>, and especially with multidimensional partitioning.

There is also <b><span style='color: var(--mk-color-red)'>no guideline on how to select values</span></b> within subdomains which might result in us <b><span style='color: var(--mk-color-red)'>not catching interactions faults</span></b> between inputs.

- [[Year 3/Sem 2/CS4218 - Software Testing/Test Generation Techniques.md#Boundary Value Analysis (BVA)|Boundary value analysis]]

Here we only focus on values at the boundary, which implies <b><span style='color: var(--mk-color-red)'>other interactions</span></b> within the input domain (*partition*) is <b><span style='color: var(--mk-color-red)'>untested</span></b>.
# What is Combinatorial Testing
---
We want to <b><span style='color: #FFD700'>identify test configurations</span></b> to allow us to consider <b><span style='color: #FFD700'>interactions between parameters</span></b>.

We also want to <b><span style='color: #FFD700'>keep our test set small</span></b> even with a large number of variables.

>[!success] Reduce cost in software testing

>[!success] Increase effectiveness in software testing

A software application works in a variety of **environments** (*hardware + software*) which includes a combinations of:
- OS
- Network connection
- Hardware platform

If we assign a specific value to each factor, we will get a <b><span style='color: #87CEEB'>test configuration</span></b>. And we want to <b><span style='color: #FFD700'>test as many test configurations as possible</span></b> (*behaviour differs based on environment*).

>[!success] Boost reliability across environments
>Different combinations of factors can result in different program behaviours.

>[!abstract] Test configuration vs test set
>A **test set** is a collection of test cases. A **test configuration** however is a <b><span style='color: #FFD700'>combination of factors corresponding to hardware & software for the application to operate</span></b>.
>
>So for **each test configuration**, we will have a **set of possible test cases** (*input & expected output*).
>
>>[!example] Example of a test configuration
>Lets say we want to test if a login field works on a web application accessed via iphone.
>>
> >Here is our possible **test configurations**:
> >
>>|   OS   | Browser |
| :----: | :-----: |
| iOS 15 | Safari  |
| iOS 15 | Chrome  |
|  ...   |   ...   |
>>
>>Then our **possible test set**:
>>
>>| Username Input | Password Input |    Expected Output    |
| :------------: | :------------: | :-------------------: |
|      bob1      |    Password    |  "Login successful."  |
|      bob1      | WrongPassword  | "Incorrect password." |
|      ...       |      ...       |          ...          |
# Input Modeling
---
Before going into the process or technique of combinatorial testing, we need to <b><span style='color: #FFD700'>model the input & configuration space</span></b>.
## Input Space & Configuration Space

The **input space** of a program ($p$) consist of <b><span style='color: #FFD700'>k-tuples of values that can be an input</span></b> during execution.

>[!example] Consider a program that takes 2 integers where $x \gt 0$ and $y \gt 0$ as inputs
>Then our input space is the set of all pairs of positive non-zero integers.

**Configuration space** of a program ($p$) consist of <b><span style='color: #FFD700'>all possible setting of the environment variables</span></b> which the program could be used in.

>[!example] Consider a program that can execute under Windows OS & MacOS and is able to print to a local or a networked printer
>
>Then our configuration space will be a triplet (x, y, z) where  x represents an operating system, y a browser, and z a local or a networked printer.
## Factors & Levels

**Factor** (*or test parameters or values*) are just one of the many <b><span style='color: #FFD700'>inputs</span></b> (*test parameters or values*) that the program accepts.

We can assign a factor a value which we can denote as $c_{i}$ (*between 1 to n*).

A **level** is a particular <b><span style='color: #FFD700'>value that can be assigned to this factor</span></b>, then we denote $\vert F \vert$ to be the <b><span style='color: #FFD700'>number of levels</span></b> for a factor $F$.
### Factor Combinations

So a <b><span style='color: #FFD700'>set of values for each factor</span></b> is known as a <b><span style='color: #87CEEB'>factor combination</span></b>.

>[!example] Example of a factor combination
> A program has 2 input variables X and Y. During execution, the input variables X and Y may each assume a value from the set {a, b, c} and {d, e, f} respectively.
> 
> So we have **2 factors** (*X & Y*) and we have **3 levels for each factor** (*X has 3 possible values so does Y*).
> 
> And we have a total of **9 factor combinations** ($3^{2}$), some examples are:
> - {a, f}
> - {b, e}
> - {c, d}
# Combinatorial Test Design
---
Each **factor combination is 1 test case**, but doing <b><span style='color: var(--mk-color-red)'>exhaustive testing might be impractical</span></b>. If we have 15 factors and 4 levels each that is about 1 billion test cases ($4^{15}$). So our **goal is to reduce the number of testcases**.

Combinatorial test design **process**:

![[Combinatorial Test Design Process.excalidraw.png|center]]

>[!note] Combinatorial object
>It is just an array of levels & factors, it is also known as a <b><span style='color: #87CEEB'>factor covering design</span></b>.

>[!note] Steps after modeling can be automated

>[!info] Modeling of the input or environment is not exclusive
>You can <b><span style='color: #FFD700'>model both or just 1</span></b> depending on the application under test.

So after generating our test cases, the **tester must**:
- Determine the <b><span style='color: #FFD700'>sequence in which inputs are applied</span></b> to the program under test
- Determine the <b><span style='color: #FFD700'>order in which the test are applied</span></b> (*combinatorial test does not specify the order*)
## Fault Model

With our test cases we aim to identify <b><span style='color: #87CEEB'>interaction faults</span></b>.

>[!abstract] Interaction fault
> It is triggered when a certain <b><span style='color: #FFD700'>combination of 1 or more input values</span></b> which cause the program to <b><span style='color: #FFD700'>enter an invalid state</span></b>.
> 
> >[!important] This invalid state must propagate to a point in the program execution where it is observable
### T-Way Interaction Faults

For any arbitrary value of $t$ the faults are known as t-way interaction faults:
- If **t = 1** this is known as a <b><span style='color: #FFD700'>simple fault</span></b>
- If **t = 2** this is known as <b><span style='color: #FFD700'>pairwise interaction faults</span></b>
- And so on...

>[!important] So essentially $t$ denotes the number of variables which cause the fault.

>[!example] Example of a pairwise interaction fault
>Assume we have the following python code:
>```python
>def fn (x:int, y:int, z:int):
>	if (x == x1 and y == y2):
>		return f(x, y, z)
>	elif (x == x2 and y = y1):
>		return g(x, y)
>	else:
>		return f(x, y, z) + g(x, y)
>```
>Assuming that if `x = x1` and `y = y1` the output should be `f(x, y, z) - g(x, y)`. So the interaction between x and y trigger this fault.
>
>Notice that the input to the function is 3 but to trigger the fault t = 2.

>[!warning] Not all combinations of values for the variables will catch the issue
>Maybe we are testing x + y but we coded x - y, so if x and y are 0 then we cannot reveal the fault.
## Fault Vector

Lets define some variables, let:
- $k$ be the **number of factors** (*variables*) ($f_{1}, f_{2}, \dots, f_{k}$)
- Let $q_{i}$ be a particular **level** for variable $i$ where $1 \le i \le k$
- Let $V$ be a **vector of factor levels**,  each row denoted a combination of possible values ($l_{1}, \dots l_{k}$) where $l_{i}$ with $1 \le i \le k$, is a specific level for the corresponding factor

This vector $V$ is also known as a <b><span style='color: #87CEEB'>run</span></b>.

A **run** is a <b><span style='color: #87CEEB'>fault vector</span></b> for the program is during <b><span style='color: #FFD700'>execution of a test case derived from the run triggers a fault</span></b>.

So $V$ is considered as a <b><span style='color: #87CEEB'>t-fault vector</span></b> for any $t \le k$ <b><span style='color: #FFD700'>elements that are needed to trigger a fault</span></b>. So this t-way fault vector for a program triggers a t-way fault in the same program.

>[!example] Example of a fault vector
>Assume we have the following python code:
>```python
>def fn (x:int, y:int, z:int):
>	p = (x + y) * z # The fault here is it should be -
>	if (p >= 0):
>		return f(x, y, z)
>	else:
>		return g(x, y)
>```
>Assume that $x \in \{-1, 1\}$, $y \in \{-1, 0\}$ & $z \in \{0, 1\}$. For all possible combinations we have **8 runs**. Then our fault vectors (*3-way*) will look like:
>
>| S/N |  x  |  y  |  z  | $x + y \neq x - y$ | $z \neq 0$ | Reveal Fault |
| :-: | :-: | :-: | :-: | :----------------: | :--------: | :----------: |
|  1  |  1  |  0  |  1  |         F          |     T      |      F       |
|  2  |  1  |  0  |  0  |         F          |     F      |      F       |
|  3  |  1  | -1  |  1  |         T          |     T      |      T       |
|  4  |  1  | -1  |  0  |         T          |     F      |      F       |
|  5  | -1  |  0  |  1  |         F          |     T      |      F       |
|  6  | -1  |  0  |  0  |         F          |     F      |      F       |
|  7  | -1  | -1  |  1  |         T          |     T      |      T       |
|  8  | -1  | -1  |  0  |         T          |     F      |      F       |

>[!goal] So the goal is to generate enough runs to reveal all t-way faults

>[!important] Even with k inputs we do not always need to find k-way faults
>Some times we can find lower level runs where $t \lt k$ because the other inputs are redundant regardless of value to trigger the fault.

# Combinatorial Testing Techniques
---
## Pairwise Design

Also known as <b><span style='color: #87CEEB'>all pairs testing</span></b>. Here we <b><span style='color: #FFD700'>focus on 2-way interaction faults</span></b>.

Pairwise design aims to provide a <b><span style='color: #98FB98'>smart & efficient</span></b> approach to test combination of pairs of input parameters. Here we do not do exhaustive testing but try and <b><span style='color: #FFD700'>increase our detection to defects while minimising test cases</span></b>.

>[!note] It follows a fundamental principle that most defects are caused by the interaction of 2 parameters

Each **selected combination** is at <b><span style='color: #FFD700'>least 1 test input or test configuration</span></b>.

>[!goal] The goal of pairwise design is to choose tests such that each pair appears in at least 1 test
### General Case Of Pairwise Testing With Binary Factors

>[!example] Example of pairwise design with binary factors
>Lets say we have 3 variables with binary values, then we have **8 possible combinations** We can reduce this to 4 test cases so all pairs appear once:
>- $(x_{1}, y_{1}, z_{2})$
>- $(x_{1}, y_{2}, z_{1})$
>- $(x_{2}, y_{1}, z_{1})$
>- $(x_{2}, y_{2}, z_{2})$
>  
>  These 4 cases if you can see covers any possible pairs of values for any 2 of the 3 input variables.
>  
>  And just nice this is also known as a <b><span style='color: #87CEEB'>balance design</span></b>, because <b><span style='color: #FFD700'>each variable value occurs exactly the same number of times</span></b>, which means <b><span style='color: #FFD700'>all the pairs appear the same number of times also</span></b>.

Lets **generalise** this with any $n$ number of factors but they still only take binary values. We define $S_{2k - 1}$ to be a set of <b><span style='color: #FFD700'>binary strings</span></b> (*1 or 0*) of <b><span style='color: #FFD700'>length 2k - 1</span></b> with <b><span style='color: #FFD700'>exactly k, 1s</span></b>.

When we choose exactly $2k - 1 \choose k$ strings chosen inside $S_{2k - 1}$. We are essentially choosing k positions out of 2k-1 positions of where the value 1 can be.

Recall that:
$$
{2k - 1 \choose k}  = \frac{(2k-1)!}{(2k - 1 - k)! (k!)}
$$
Where:
- $2k - 1$ is the <b><span style='color: #FFD700'>number of test cases</span></b>
- The resulting value will be the <b><span style='color: #FFD700'>number of factors we can have to test all possible pairs</span></b> with $2k - 1$ tests

>[!idea] Just iterate k and find a output that is larger than or equal to the number of factors you have
### General Case Of Pairwise Testing

Lets go through this with an **example**, suppose we have the following parameters and the possible values:

| Parameter |      Possible Values      |
| :-------: | :-----------------------: |
|    $w$    |     $w_{1}$, $w_{2}$      |
|    $x$    | $x_{1}$, $x_{2}$, $x_{3}$ |
|    $y$    |     $y_{1}$, $y_{2}$      |
|    $z$    | $z_{1}$, $z_{2}$, $z_{3}$ |
Now we <b><span style='color: #FFD700'>create a table where the rows is the number of test cases & the columns are the factors</span></b>.

Then we do the following steps:
1) Take the <b><span style='color: #FFD700'>parameter with the largest number of possible values</span></b> (*levels*)
2) Fill up the table such that:
	- If it is the **first variable** of the table <b><span style='color: #FFD700'>repeat each value</span></b> $x$ time where $x$ is the <b><span style='color: #FFD700'>number of possible values for the next smallest factor</span></b>
	- If it is **not the first** then <b><span style='color: #FFD700'>fill up the column</span></b> such that <b><span style='color: #FFD700'>all pairs with the previously filled up variables have been covered</span></b>
3) Repeat step 1 until all variables have been selected & all pairs are tested

>[!note] If there is a tie with the largest number of possible values than pick either one

>[!warning] Just multiplying the levels of the first 2 factors with the most number of levels does not always give the minimum number of test cases

So based on our example, we should get:

| Test Case |    z    |    x    |    w    |    y    |
| :-------: | :-----: | :-----: | :-----: | :-----: |
|     1     | $z_{1}$ | $x_{1}$ | $w_{1}$ | $y_{1}$ |
|     2     | $z_{1}$ | $x_{2}$ | $w_{2}$ | $y_{2}$ |
|     3     | $z_{1}$ | $x_{3}$ | $w_{1}$ | $y_{1}$ |
|     4     | $z_{2}$ | $x_{1}$ | $w_{2}$ | $y_{2}$ |
|     5     | $z_{2}$ | $x_{2}$ | $w_{1}$ | $y_{1}$ |
|     6     | $z_{2}$ | $x_{3}$ | $w_{2}$ | $y_{2}$ |
|     7     | $z_{3}$ | $x_{1}$ | $w_{1}$ | $y_{1}$ |
|     8     | $z_{3}$ | $x_{2}$ | $w_{2}$ | $y_{1}$ |
|     9     | $z_{3}$ | $x_{3}$ | $w_{1}$ | $y_{2}$ |
>[!important] The test cases may be different but the number will be the same

>[!important] These test cases & all test case generation techniques is to generate positive testcases
>Those invalid test cases you consider even without the test generation output.
## Orthogonal Array

An orthogonal array is a $N \times k$ matrix (*k is the number of factors*) which entries are from a finite set of $S$ symbols such that <b><span style='color: #FFD700'>any N by t subsequence contains each t-tuple exactly the same number of times</span></b>.

>[!note] $N$ is the number of runs 

>[!note] $t$ is the strength of the orthogonal array

We denote this array as $OA(N, k, s, t)$ or $L_{N}(s^{k})$ which can be translated to $N$ runs where $k$ factors take on any values in the set of $s$.

>[!example] Example of an orthogonal array
>| Run | $F_{1}$ | $F_{2}$ | $F_{3}$ |
| :-: | :-----: | :-----: | :-----: |
|  1  |    1    |    1    |    1    |
|  2  |    1    |    2    |    2    |
|  3  |    2    |    1    |    2    |
|  4  |    2    |    2    |    1    |
>
>Given this example:
>$N = 4$
>$k = 3$
>$s = 2$ because there are 2 unique values
>$t = 2$ if we take any $4 \times 2$ subarray, each 2-tuple appears the same number of times
>
>So this is a $OA(4, 3, 2, 2)$ or $L_{4}(2^{3})$

The <b><span style='color: #87CEEB'>index of an orthogonal array</span></b> is denoted by $\color{#FFD700}{\lambda = N/s^{t}}$, which tells us <b><span style='color: #FFD700'>how many unique t sized tuples appears in a subarray</span></b>.

>[!important] Here we assume all factors have the same number of levels

>[!success] To find the number $t$ which causes the faults just see which runs the $t$ size tuples appears in all the runs that causes the problem
### Mixed Level Orthogonal Arrays

In most cases **factors** will have <b><span style='color: #FFD700'>varying number of levels</span></b>. We denote these arrays as $MA(N, s_{1}^{k1}, s_{2}^{k2}, \dots, s_{p}^{kp}, t)$, where $k_{i}$ is the number of factors which has $s_{i}$ number of levels. So $p$ is the maximum number of levels for any given factor.

So the **sum of factors** is just $\sum_{i = 1}^{p}k_{i}$

>[!note] If we have to choose which of the orthogonal arrays (*mixed or not*), just pick the one with the smallest number of runs that satisfies our function
>If there are excess variables of factors it is alright, when writing our tests just leave them blank or use a dummy value.

The formula to **compute** $\lambda$ is <b><span style='color: var(--mk-color-red)'>different from the normal orthogonal array</span></b>. But the balance property that <b><span style='color: #FFD700'>any N by t subarray contains each t-tuple exactly the same number of times</span></b> (*which is equal to* $\lambda$).

>[!example] Example of a mixed orthogonal arrays
>|Run|Factor A (4-Level)|Factor B (2-Level)|Factor C (2-Level)|Factor D (2-Level)|Factor E (2-Level)|
|:---:|:---:|:---:|:---:|:---:|:---:|
|1|1|1|1|1|1|
|2|1|2|2|2|2|
|3|2|1|1|2|2|
|4|2|2|2|1|1|
|5|3|1|2|1|2|
|6|3|2|1|2|1|
|7|4|1|2|2|1|
|8|4|2|1|1|2|
>
>Here we have $MA(8, 2^{4}, 4^{1}, 2)$, so any 2 columns we can see the same number of pairs.


