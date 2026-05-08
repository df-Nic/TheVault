---
Title: Control Flow Testing
Date Created: 30-January-2026
Last Updated: 30-January-2026
Tags:
  - CS4218
  - SWE/Testing/TestCaseFormulation
  - DataStructures/Graphs
---
# Motivation of Control Flow Testing
---
So we explored unit & integration tests and how to write them in a structured manner. But for a given program / function, there <b><span style='color: var(--mk-color-red)'>can be multiple different test inputs</span></b> to choose from.

>[!question] So how do we decide which ones to use for our tests?
>It is <b><span style='color: var(--mk-color-red)'>impossible to enumerate every single possible input</span></b>. So that our <b><span style='color: #98FB98'>testing is efficient while ensuring a robust & reliable software</span></b>.

So the aim for <b><span style='color: #87CEEB'>control flow testing</span></b> is to <b><span style='color: #FFD700'>derive inputs systematically</span></b>.

**Flow of doing control flow testing**
![[Control Flow Testing Flow.png|center]]

>[!fail] It is however not sufficient on its own to catch all bugs
# Core Concepts for Control Flow
---
>[!note] Control flow testing falls under white box testing

At the most basic level there are **2 kinds of program statements**:
1) **Assignment** statements (`x = 1`, `a = 2 * y`)
2) **Conditional** statements (`for`, `while`, `if`)

These form the structure of a program, and when <b><span style='color: #FFD700'>code executes sequentially</span></b>, it is known as the <b><span style='color: #87CEEB'>flow of control</span></b>. And with the **presence of conditional statements**, it can <b><span style='color: #FFD700'>alter the default flow</span></b>.

So the <b><span style='color: #FFD700'>sequence of statements executed from the start of a program till its exit</span></b> its known as <b><span style='color: #87CEEB'>program paths</span></b>.

>[!question] Difference between flow of control & program paths
>While they are related concepts, the **flow of control** refers to the <b><span style='color: #FFD700'>order</span></b> in which individual code is executed.
>
>While for **program path** it is the <b><span style='color: #FFD700'>full sequence of instructions taken</span></b> during execution.

There <b><span style='color: var(--mk-color-red)'>can be a large amount of paths</span></b> in a program which has its corresponding input & expected output.

>[!failure] So testing all paths is infeasible
>Take for instance a simple `while(n > 0)` it can take any integer value which results in a infinite number of paths.

>[!example] Example of a program path
>
>```java
>public static int divide(int numerator, int denominator) {
>	if (denominator == 0) {
>		throw new IllegalArgumentException(“Error!”);
>	}
>	return numerator / denominator;
>}
>```
>| numerator | denominator |       Path        |  Output   |
| :-------: | :---------: | :---------------: | :-------: |
|     4     |      2      | 2 $\rightarrow$ 5 |     2     |
|     4     |      0      | 2 $\rightarrow$ 3 | Exception |
>
> So we have 2 possible paths each with their own inputs & expected outputs.

So the idea of control flow testing is to:
1) Identify all possible execution paths through a module of program code
2) Define different levels of [[Year 3/Sem 2/CS4218 - Software Testing/Code Coverage Metrics.md|test coverage]] to help us select a set of paths (*statement, branch, decision, etc*)
3) Create & execute test cases to cover those paths

>[!question] Why do we need to define test coverage?
>Since 100% path coverage is impossible we need to <b><span style='color: #FFD700'>prioritise the paths we focus on during test case design</span></b>, this choosing of inputs is called <b><span style='color: #87CEEB'>path sensitisation</span></b>.
>
>Generally we choose paths to achieve 100% [[Year 3/Sem 2/CS4218 - Software Testing/Code Coverage Metrics.md#Statement Coverage|statement]] & [[Year 3/Sem 2/CS4218 - Software Testing/Code Coverage Metrics.md#Branch Coverage|branch]] converge.

# Control Flow Graphs
---
It is a useful graphical method to <b><span style='color: #FFD700'>identify the possible program execution paths</span></b>.

It is also known as a:
- Flow graph
- Program graph

So formally a control flow graph (*CFG*) is a: 
- Finite set of nodes ($N$) & edges ($E$).
- An edge ($i, j$) in the set of edges $E$ connects 2 nodes $n_{i}$ & $n_{j}$ in the set of nodes $N$
- Thus $G = (N, E)$ denotes a CFG with nodes $N$ and $E$ edges

>[!info] Nodes in a CFG
>They are the <b><span style='color: #FFD700'>longest possible sequence of consecutive statements in a program such that control can enter the block only at the first statement and exit from the last</span></b>.
>
>Here are some rules for a basic block:
>- No conditional statement other than at its edge (*last statement for the block*)
> - Has unique entry and exit points
> - Control always enters entry point and exits from exit point (*this is important for loops so a for loop will be in its own block*)
> - <b><span style='color: #FFD700'>No possibility of exit or halt at any point inside except at exit point</span></b>
> - Entry and exit points coincide when it contains only one statement

>[!info] Edges in a CFG
>They <b><span style='color: #FFD700'>indicate the flow of control</span></b> across basic blocks.

>[!example] Example of a CFG
> ```java
>int fn() { // Line 1
> 	int x, y, power; // Line 2
> 	float z; // Line 3
> 	input (x, y); // Line 4
> 	if (y < 0) { // Line 5
> 		power = -y; // Line 6
> 	} else { // Line 7
> 		power = y; // Line 8
> 	} // Line 9
> 	z = 1; // Line 10
> 	while (power != 0) { // Line 11
> 		z = z * x; // Line 12
> 		power = power – 1; // Line 13
> 	} // Line 14
> 	if (y < 0) { // Line 15
> 		z = 1/z; // Line 16
> 	} // Line 17
> 	return z; // Line 18
} // Line 19
>```
>
>| Block |  Lines  | Entry Point | Exit Point |
| :---: | :-----: | :---------: | :--------: |
|   1   | 2,3,4,5 |      1      |     5      |
|   2   |    6    |      6      |     6      |
|   3   |    8    |      8      |     8      |
|   4   |   10    |     10      |     10     |
|   5   |   11    |     11      |     11     |
|   6   | 12, 13  |     12      |     13     |
|   7   |   15    |     15      |     15     |
|   8   |   16    |     16      |     16     |
|   9   |   18    |     18      |     18     |
>
>This this will be our final CFG:
> ![[CFG Graph Example.png|center]]
## Paths

So given a CFG, a path is a <b><span style='color: #FFD700'>sequence of edges</span></b> through the flow graph, it can be denoted as $O, (e_{1}, e_{2}, \dots, e_{k})$. Where $O$ denotes the **start point** or **entry point**.

So if $e_{i} = (n_{p},n_{q})$ and $e_{i + 1} = (n_{r},n_{s})$ then $e_{q} = e_{r}$ since the ending node and the starting node of the 2 edges must be the same if not it is not a path.

Paths can be <b><span style='color: #98FB98'>feasible</span></b> or <b><span style='color: var(--mk-color-red)'>infeasible</span></b>.

>[!info] A feasible path is where at least 1 test case will cause this path to be traversed
> For example, if we take the CFG above a valid path is , start, 1, 3, 4, 5, 6, 5, 7, 9, end.

>[!info] A infeasible path is where there are no test cases that will cause this path to be traversed
> For example, if we take the CFG above a invalid path is , start, 1, 2, 4, 5, 7, 9, end.
> 
> The reason if we take $5 \rightarrow 7$ it means `power == 0` & `y == 0` which means it should have taken $1 \rightarrow 3$ & not $1 \rightarrow 2$.
> 
> >[!important] Even though it is a path on the graph it might not be feasible

Generally if a program has <b><span style='color: #FFD700'>0 conditional statements it has only 1 path</span></b>. But with **adding a conditional statement** it <b><span style='color: #FFD700'>increase the number of distinct paths by at least 1</span></b> (*it can have a multiplicative effect*).
## Dominator & Post Dominator

Given nodes $X$ & $Y$ in a CFG:

>[!important] X & Y are not program statements but nodes in the CFG or the basic blocks 

|           Term           |                                                                                                                                                       Definition                                                                                                                                                       |
| :----------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|         Dominate         |                                                    $X$ dominates $Y$ if <b><span style='color: #FFD700'>all possible program paths from START to</span></b> $\color{#FFD700}{Y}$ <b><span style='color: #FFD700'>must pass through</span></b> $\color{#FFD700}{X}$                                                     |
|    Strictly Dominate     |                                                         $X$ strictly dominates $Y$ if $\color{#FFD700}{X}$ <b><span style='color: #FFD700'>dominates</span></b> $\color{#FFD700}{Y}$ <b><span style='color: #FFD700'>&</span></b> $\color{#FFD700}{X \neq Y}$                                                          |
|   Immediate Dominator    |                           $X$ is a immediate dominator of $Y$ if $\color{#FFD700}{X}$ <b><span style='color: #FFD700'>is the last dominator of</span></b> $\color{#FFD700}{Y}$ along a path <b><span style='color: #FFD700'>from START to</span></b> $\color{#FFD700}{Y}$ & it cannot be $Y$                           |
|      Post-Dominate       |                                                  $X$ post-dominates $Y$ if <b><span style='color: #FFD700'>all possible program paths from</span></b> $\color{#FFD700}{Y}$  <b><span style='color: #FFD700'>to END must pass through</span></b> $\color{#FFD700}{X}$                                                   |
|  Strictly Post-Dominate  |                                                    $X$ strictly post-dominates $Y$ if $\color{#FFD700}{X}$ <b><span style='color: #FFD700'>post-dominates</span></b> $\color{#FFD700}{Y}$ <b><span style='color: #FFD700'>&</span></b> $\color{#FFD700}{X \neq Y}$                                                     |
| Immediate Post-Dominator | $X$ is a immediate post-dominator of $Y$ if $\color{#FFD700}{X}$ <b><span style='color: #FFD700'>is the first post-dominator of</span></b> $\color{#FFD700}{Y}$ along a path <b><span style='color: #FFD700'>from</span></b> $\color{#FFD700}{Y}$ <b><span style='color: #FFD700'>to END</span></b> & it cannot be $Y$ |

>[!example] Example of all the terms using a simple CFG
>![[Dominate & Post-Dominate Example.png|center|500]]

# Program Dependence Graphs
---
Program dependence graphs (*PDG*) is a graphical method to <b><span style='color: #FFD700'>visualise a program's structure & aid in debugging tests</span></b>.

It visually shows which <b><span style='color: #FFD700'>program statements are dependent on one another</span></b>.

There are **2 types of dependencies**:
1) **Data** dependence
2) **Control** dependence

>[!question] What is the difference between CFG & PDG?
>|              |                                  Control Flow Graphs                                   |                                 Program Dependence Graphs                                 |
| :----------: | :------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------: |
| Illustration |                             Control flow within a program                              |                      Data & control dependencies between statements                       |
| Application  | Control flow testing: Identity the test inputs according to the program's control flow | Understand program behaviour, debug test cases, program optimisation, test case selection |
|    Nodes     |                                 Represent basic blocks                                 |                              Represent individual statements                              |

So a <b><span style='color: #FFD700'>PDG is composed to 2 subgraphs</span></b>:
1) **Data dependence graph** (*solid arcs / lines*)
2) **Control dependencies graph** (*dashed arcs / lines*)

<b><span style='color: #FFD700'>Each node is is 1 program statement</span></b>. And this graph is just a <b><span style='color: #FFD700'>combination of data & control dependence graphs</span></b> (*so just make the 2 graphs and combine them*).
## Data Dependency Graphs

So given a graph $G$ and the nodes $N$ are the individual lines of code. Node $X$ is **data dependent** on $Y$ is **both of the conditions are true**:
1) There is a <b><span style='color: #FFD700'>variable</span></b> $\color{#FFD700}{v}$ <b><span style='color: #FFD700'>that is defined at</span></b> $\color{#FFD700}{Y}$ <b><span style='color: #FFD700'>& used at</span></b> $\color{#FFD700}{X}$.
2) There exist a <b><span style='color: #FFD700'>path of non-zero length</span></b> from $\color{#FFD700}{Y}$ <b><span style='color: #FFD700'>to</span></b> $\color{#FFD700}{X}$ along which $\color{#FFD700}{v}$ <b><span style='color: #FFD700'>is not re-defined</span></b>.

>[!info] Re-defined basically means that the variable is not reassigned to another value

>[!example] Example of a data dependence graph
>Given this code:
>```python
>def fn ():
>	sum = 0 # Line 1
>	i = 1 # Line 2
>	while (i , N): # Line 3
>		i = i + 1 # Line 4
>		sum = sum + i # Line 5
>	print(sum) # Line 6
>}
>```
>The data dependency graph will  look like:
>![[Data Dependency Graph Example.png|center|300]]
>Explanation of some of the dependency:
>
>|        Dependency        |                       Condition 1                       |                                         Condition 2                                          |
| :----------------------: | :-----------------------------------------------------: | :------------------------------------------------------------------------------------------: |
| 3 is data dependent on 2 |          Variable `i` defined at 2, used at 3           |               Path $2 \rightarrow 3$ it is of length 1 and it is not redefined               |
| 4 is data dependent on 4 | Variable `i` is defined at 4, used at 4 (*after the =*) | Path $4 \rightarrow 5 \rightarrow 3 \rightarrow 4$ it is of length 4 and it is not redefined |
| 4 is data dependent on 2 | Variable `i` is defined at 2, used at 4 (*after the =*) |        Path $2 \rightarrow 3 \rightarrow 4$ it is of length 3 and it is not redefined        |
## Control Dependency Graphs

A control dependence graph (*CDG*) shows weather a <b><span style='color: #FFD700'>statement directly determines weather another statement executes</span></b>. 

Node $Y$ is **control dependent** on $X$ is **both of the conditions are true**:
1) $\color{#FFD700}{X}$ is <b><span style='color: #FFD700'>not strictly post-dominated</span></b> by $\color{#FFD700}{Y}$. In other words **a path** that goes from $X$ to END but does not pass through $Y$
2) There is **a path** from $X$ to $Y$ such that <b><span style='color: #FFD700'>every node in the path is post dominated by</span></b> $\color{#FFD700}{Y}$ (*except X and Y themselves*). In other words for each node every path from that node to END must pass through $Y$

>[!example] Example of a control dependence graph
>Given this code:
>```python
>def fn ():
>	sum = 0 # Line 1
>	i = 1 # Line 2
>	while (i , N): # Line 3
>		i = i + 1 # Line 4
>		sum = sum + i # Line 5
>	print(sum) # Line 6
>}
>```
>The control dependency graph will  look like:
>![[Control Dependency Graph Example.png|center|300]]
>Explanation of some of the dependency:
>
>|         Dependency          |                           Condition 1                           |                                                    Condition 2                                                     |
| :-------------------------: | :-------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------: |
| 4 is control dependent on 3 | $3 \rightarrow 6 \rightarrow END$ which does not pass through 4 |                             $3 \rightarrow 4$ which makes the condition vacuously true                             |
| 5 is control dependent on 3 | $3 \rightarrow 6 \rightarrow END$ which does not pass through 5 | $3 \rightarrow 4 \rightarrow 5$ this path excluding 3 & 5, from $4 \rightarrow END$ every path must pass through 5 |
| 3 is control dependent on 3 |                             3 == 3                              |                        $3 \rightarrow 4 \rightarrow 5 \rightarrow 3$ this path excluding 3                         |

# Additional Graphs
---
There is a <b><span style='color: #87CEEB'>super control flow graph</span></b> (*SCFG*) where additional edges are added to connect the following:
- Each call site (*the person calling the function*) to the beginning of the procedure it calls
- The return statement back to the call site

>[!note] Essentially it can model control dependency between function calls

![[Super Control Flow Graph.png|center]]

This allows us to <b><span style='color: #FFD700'>do inter-procedural analysis</span></b>.

There is also a <b><span style='color: #87CEEB'>call graph</span></b> (*CG*) which <b><span style='color: #FFD700'>captures the call interactions among functions</span></b> in a program. Here each **node** <b><span style='color: #FFD700'>represents a function</span></b>, then an **edge** represents a <b><span style='color: #FFD700'>function invocation</span></b> (*function call*).

![[Call Graph.png|center]]

>[!info] An edge represents 1 function invocation
>So if the function calls the another function 2 times then there should be 2 edges.