---
title: Constraint Satisfaction Problems
Date Created: 2025-08-13
Last Updated: 2025-09-28
tags:
  - CS3263
  - AI
  - Graphs
  - CSP
---
# Constraint Satisfaction Problems
---
## States

A state can be defined as the <b><span style='color:var(--mk-color-yellow)'>current or possible statuses</span></b> of a given environment (*Chess pieces positioning or current board in tic tac toe*).

There are **3 types of states:**

1) **Atomic**
An atomic state is represented as a <b><span style='color:var(--mk-color-yellow)'>single indivisible entity</span></b> where you do not need to reason about the parts inside it.

  >[!example] Atomic State Example
  > Given a map using the cartesian coordinate system, we can represent a state as `(x, y)`.
  > 
  > There is no additional information like, is this position blocked or weather it has a toll to pay to pass through.

2) **Factored**
A factored state is represented by a <b><span style='color:var(--mk-color-yellow)'>set of variables and their respective values</span></b>. Allowing you to reason about parts of the state separately.

The **set of all possible values** a variable can take is called the <b><span style='color:var(--mk-color-turquoise)'>domain</span></b>.

  >[!example] Factored State Example
  > Given a robot with coordinates and a battery capacity. The robot's state can be represented as `x : 1, y : 2, bettery : 80%`
  > 
  > Before transitioning to another state we need to determine if the robot has enough battery before proceeding.

3) **Structured**
A structured state is similar to a factored state but it now contains <b><span style='color:var(--mk-color-yellow)'>objects and relationships</span></b> between them.

  >[!example] Structured State Example
  > Lets represent a block stacking game. We can have 2 objects block `A` and `B`.
  > 
  > We can model relationships such as `On(A, B)`, meaning block `A` is on top of block `B`.

>[!failure] Factored & Structured states have exponential memory blowup when representing all possible states
>
>Given that 1 state can have $n$ variables and each variable can have $k$ possible values, we can have a total of $k^{n}$ possible states.

When a CSP finds a possible solution, this is known as a <b><span style='color:var(--mk-color-turquoise)'>goal state</span></b>. And in a goal state:
- It must be <b><span style='color:var(--mk-color-yellow)'>consistent or legal assignment</span></b> (*No constraints are violated*)
- And it must be a <b><span style='color:var(--mk-color-yellow)'>complete assignment</span></b> (*All variables are assigned a value*)
<div style="page-break-after: always;"></div>

>[!note] Partial Assignment
> In between the CSP execution <b><span style='color:var(--mk-color-red)'>not all variables are assigned a value</span></b>. However for a CSP <b><span style='color:var(--mk-color-green)'>every assignment is a consistent assignment</span></b>. 
## Components of a CSP

In each constraint satisfaction problem it will contain **3 components**:
1) **Variables**
We can define all variables as $X = \{ X_{1}, \dots, X_{n}\}$

>[!info] Auxiliary variables
>
> They are variables which represents a part of an expression, this is to make it <b><span style='color:var(--mk-color-green)'>simple, interpretable & reusable</span></b>.
> 
> For example, if we have $X + Y = Z$, then we can use an auxiliary variable $XYZ$ to represent a tuple combinations of all 3 variables with their given domains.

2) **Domains**
  We can define the set of <b><span style='color:var(--mk-color-yellow)'>all possible values a variable can take</span></b> as $D = \{D_{1}, \dots, D_{n}\}$
  
3) **Constraints**
 We can define the set of <b><span style='color:var(--mk-color-yellow)'>constraints over all variables and domains</span></b> as $C = \{C_{1}, \dots, C_{n}\}$

Each constraint ($C_{i}$) can be written as $<\text{scope}, \text{relation}>$
- A **scope** is a <b><span style='color:var(--mk-color-yellow)'>tuple of variables</span></b> for that constraint
- A **relation** defines what <b><span style='color:var(--mk-color-yellow)'>values these variables can take</span></b>, it can be a set of valid tuples or a function that checks its validity.
### Constraints

Constraints which **rules out potential solutions** is known as <b><span style='color:var(--mk-color-turquoise)'>absolute constraints</span></b>.
- Unary (*Against 1 variable and its possible values*)
- Binary (*Between 2 variables*)
- Higher order (*Between a fixed number of variables `fn(x, y, x)`*)
- Global (*The number of variables can vary `fn(x, y)` or `fn(x, y, z, a)`, you can think of `args` and `qargs` in python*)

>[!info] Converting a CSP to just binary constraints
>There are **2 steps**
>1) Eliminate the unary constraints
>2) Higher order constraints must be broken down into binary constraints (*using auxiliary variables*)
>   
>Given the same example above, after getting $XYZ$, our binary constraints will be:
>- $X$ must be equal to the first element in the trio
>- $Y$ must be equal to the second element
>- and so on....
> 
> To maintain the $X + Y = Z$ constraint we can <b><span style='color:var(--mk-color-yellow)'>just remove invalid triplets</span></b> in the domain, during constraint propagation.
<div style="page-break-after: always;"></div>

>[!note] Constraint Graphs
>
>If **every constraint relates to at most 2 variables** (*unary or binary*) then we can model each variable as a graph with its edges defining the constraint. This is also known as a <b><span style='color:var(--mk-color-turquoise)'>binary constraint graph</span></b>.
>
>What about **higher order or global constrains**, in this case we can model it using a **hypergraph** (*1 edge can connect to more than 2 nodes*).

Constraints which determines which **solutions are preferred** is known as <b><span style='color:var(--mk-color-turquoise)'>preference constraints</span></b>.
- These constraints are typically <b><span style='color:var(--mk-color-yellow)'>encoded as costs</span></b> on variable assignments or as another constraint
- Each solution will have a score based on the values

>[!abstract] Optimising Searches
>
>In most CSP solvers, they will have a optimised approach to find a solution or the most optimised solution.
>
>For instance in a partial assignment, it can rule out all other partial assignments which violates a constraint. Or for problems with preference constraints, it uses tactics like  branch & bound, heuristics or local search methods.
# Solving CSPs
---
A typical CSP solver will:
- Exploit structure of the states
- Identify states which violates constraints, removing them and reducing the search space
- Use general [[Problem Solving by Searching#Heuristic|heuristics]]
- Deduce actions & transitions models from problem descriptions

>[!info] Problem Specific Heuristics
>
> General solvers does not need problem specific heuristics, they have a general set of heuristics which often works well for CSPs.
## Constraint Propagation

It is a way to <b><span style='color:var(--mk-color-green)'>reduce the search space</span></b>. It does so by seeing it's <b><span style='color:var(--mk-color-yellow)'>constraints and reducing the domain</span></b> during preprocessing.

>[!example] Simple example of constraint propagation
>
>Assuming we have a constraint: $X \neq Y$ and our domain is $\{1, 2, 3\}$
>
>If a variable $A = 1$, then when assigning a variable $B$ its domain will only be $\{2, 3\}$. This reduces the search space from $3 \times 3$ to just $3 \times 2$ .
### Local Consistency

By removing invalid values from the domain it ensures <b><span style='color:var(--mk-color-turquoise)'>local consistency</span></b> which will <b><span style='color:var(--mk-color-green)'>ensure inconsistent values will be eliminated</span></b> throughout the search.

>[!info] Local consistency is ensuring that for a subset of variables it is consistent
<div style="page-break-after: always;"></div>

There are **4 types** of local consistency
1) **Node** consistency (*1-consistency*)
2) **Arc** or **edge** consistency (*2-consistency*)
3) **Path** consistency (*3-consistency*)
4) **K**-consistency
#### Node Consistency

One variable (*node in the CSP graph*) is node-consistent if <b><span style='color:var(--mk-color-yellow)'>all values in the domain satisfy its unary constraints</span></b>.

This is most likely done during **preprocessing**.

>[!note] If every variable is node-consistent then the graph itself it node-consistent

>[!example] Node consistency example
>
>If our domain is $\{0, \dots, 9\}$ and our unary constraint is that $X$ cannot be non-prime. Then $X$ can start with a domain of $\{2, 3, 5, 7\}$.
#### Arc Consistency

One variable (*node in the CSP graph*) is arc-consistent if <b><span style='color:var(--mk-color-yellow)'>all values in the domain satisfy its binary constraints</span></b>.

An <b><span style='color:var(--mk-color-turquoise)'>arc</span></b> is basically a <b><span style='color:var(--mk-color-yellow)'>pair of variables</span></b> (*$(A, B)$*) & on the graph it is represented by an edge.

How this works is that given 2 variables $A$ and $B$ for every value in $A$'s domain, **there is at least 1 value** in $B$'s domain which satisfies the binary constraint. Then do the same for $B$ but on the new domain of $A$.

>[!note] If every variable is arc-consistent then the graph itself it arc-consistent

>[!example] Arc consistency example
>
>If our domain is $\{1, 2, 3, 4, 5, 6\}$ and our binary constraint is that $2X = Y$. Then: 
>- $X$ can start with a domain of $\{1, 2, 3\}$ 
>- $Y$ can start with a domain of $\{2, 4, 6\}$.

There is an algorithm called the `AC-3` which checks if a CSP is consistent or not.

```cpp
bool AC_3(CSP) {
	queue q ; // Initialise this queue with all the arcs
	while (!q.isEmpty()) {
		arc = q.pop(); // arc -> (node1, node2). This is for all possible pairs
		if (revise(CSP. node1, node2)) {
			if (node1.domain.length() == 0) { // This means that there is no value in the domain which satisfies the constraints
				return false;
			}
			for (auto neighbour : node1) {
				if (neighbour != node2) {
					queue.push((neighbour, node1)); // We need to recheck due to pruning
				}
			}
		}
	}
	return true;
}

bool revise(CSP, node1, node2) {
	bool revised = false;
	for (auto value : domain) { // Domain of node 1
		if (no_value) { // If there is not 1 value in the domain of node 2 that satisfies the constraint
			domain.delete(value); // Remove the value from the domain of node 1
			revised = true;
		}
	} 
	return revised;
}
```

>[!info] You can treat partial assignments as a singleton domain with the assigned value
## Starting Our Search

After doing constraint propagation, if we have multiple possible values we need do start our search.
### Backtracking Search

Backtracking is essentially a variant of a [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Depth-First Search|depth-first search]] algorithm.

>[!info] It works over partial assignments

>[!success] It is a complete algorithm
>
>When we say complete it means it:
>- Correctly finds a solution or
>- Reports a failure (*No solution found*)

Here is a standard backtracking algorithm:
```cpp
// If you want to return a solution, have a vector or dictionary to store the correct assignment
vector<int> backtrack(CSP, assignment) {
	var = select_unassigned_var(CSP, assignment); // A function to determine which variable to go to next
	for (auto value : order_domain_values(csp, var, assignment)) { // In the domain of selected var
		if (value == consistent) { // Value is consistent with the constraints
			assignment.add(value, var); // Add the value for the variable
			// Check if assingment causes other unassigned vars to have a empty domain
			inference = inference(csp, var, assignment);
			if (inference != failure) { // Every other variable is still valid
				csp.update(inference); // Update the domains
				result = backtrack(CSP, assignment);
				if (result != faulure) {
					return result;
				}
				csp.remove(inferences); // The assigned value did not work thus rever to the original state
			}
			assignment.remove(var); // Revert to the original state
		}
	}
	return failure;
}
```
#### Improving Backtracking

To improve on our search in general we can use **domain-independent heuristics** taking advantage of the **factored representation** of CSPs (*the constraints, variables & domains*).
##### Ordering
With the pseudocode for the `backtracking` algorithm, we need to **pick one unassigned variable**, afterwards we need to **pick which value to assign** it.

To **pick a variable** (`select_unassigned_var`) we can use a heuristic called <b><span style='color:var(--mk-color-turquoise)'>minimum-remaining-values</span></b> (*MRV*).

>[!summary] Minimum-remaining-values
>
>It essentially <b><span style='color:var(--mk-color-yellow)'>picks the variable with the fewest legal values</span></b> (*smallest domain*).

>[!question] Why does MRV work?
>
>Also known as "most constraint variable" or "fail-first" heuristic. As the name suggests in the latter we want to <b><span style='color:var(--mk-color-yellow)'>pick the variable most likely to cause failure soon</span></b>.
>
>By doing so we can find a variable $X$ with an empty domain during forward propagation. Which will cause a backtrack, <b><span style='color:var(--mk-color-green)'>reducing the search space</span></b>.

If MRV does not help (*at the start of the search*), the <b><span style='color:var(--mk-color-turquoise)'>degree heuristic</span></b> can be used. This is to attempt to <b><span style='color:var(--mk-color-green)'>reduce the branching factor</span></b> on future choices affected by this variable.

>[!summary] Degree heuristic
>
>It essentially picks the variable <b><span style='color:var(--mk-color-yellow)'>involved in the most number of constraints on other unassigned variables</span></b>.
>
>In a graph you can just count the variable's neighbours.

To **pick a value** (`order_domain_value`) we can use the <b><span style='color:var(--mk-color-turquoise)'>least-constraining-value</span></b> (*LCV*) heuristic. This is to attempt to have the <b><span style='color:var(--mk-color-green)'>maximum flexibility for subsequent assignment</span></b>.

>[!summary] Least-constraining-value
>
>It will pick the value that <b><span style='color:var(--mk-color-yellow)'>rules out the fewest choices for its neighbouring variables</span></b>.
>
>Check the domain of its neighbours given an assignment.
##### Filtering
After assigning a variable to a value, we can do a **forward checking** to <b><span style='color:var(--mk-color-green)'>reduce the search space</span></b> & <b><span style='color:var(--mk-color-yellow)'>filter out unwanted values for unassigned variables</span></b> which are neighbours.

We can simply do this inside the `inference` function by **calling** the `AC-3` function but **on arcs** that are <b><span style='color:var(--mk-color-yellow)'>neighbours</span></b> of the assigned variable and they themselves are <b><span style='color:var(--mk-color-yellow)'>unassigned</span> </b>.

This algorithm is known as <b><span style='color:var(--mk-color-turquoise)'>maintaining arc consistency</span></b> (*MAC*) and its more powerful than forward checking (*since forward checking only check its neighbours*).

>[!info] We can do filtering before the search & it might give a solution even before starting it
##### Intelligent Backtracking

Instead of backtracking 1 decision back (*chronological backtracking*), how about <b><span style='color:var(--mk-color-yellow)'>going to a variable which can fix the problem</span></b>. This is known as <b><span style='color:var(--mk-color-turquoise)'>back jumping</span></b>.

>[!failure] Sometimes going back by 1 step does not resolve the problem

Each variable will have a conflict set (*a set of other variables*). When a value is assigned a value, <b><span style='color:var(--mk-color-yellow)'>add the assignment</span></b> to this set for all its neighbours.

When all values are exhausted, instead of going back by 1, <b><span style='color:var(--mk-color-yellow)'>backtrack to the variable in which was last added into the conflict set</span></b>.

>[!important] If we use forward checking or MAC, back jumping is redundant
### Local Search

Unlike backtracking where we build a solution progressively, for [[Local & Adversarial Search#Local Search|local search]] we will:
- Start with a complete assignment 
- If there is conflicts, change 1 variable to a value that minimises conflicts
- Repeat until a solution is found OR the max retries has been exceeded

>[!info] It works over complete assignments

>[!failure] It can be an incomplete algorithm
>
>When its incomplete, it means it <b><span style='color:var(--mk-color-red)'>does not guarantee a solution even though there is one</span></b>.

There are also heuristics to **pick the correct value to change**, one of these is the <b><span style='color:var(--mk-color-turquoise)'>minimum-conflict heuristic</span></b>.

This heuristic basically <b><span style='color:var(--mk-color-yellow)'>picks the value where it has the least constraint violations</span></b> against the other assigned variables.

>[!question] Why does the min-conflict heuristic work?
>
>Essentially by selecting the value with the least violated constraints, we are essentially **moving closer towards the solution**.