---
title: Debugging & Fault Localization
Date Created: 2025-03-10
Last Updated: 2025-09-28
tags:
  - CS3213
  - SWE
  - Debugging
---
# Debugging
----
During development developers spend <b><span style='color:var(--mk-color-red)'>35-50% of their time validating and debugging</span></b> software. And the **cost** of debugging, testing and verification is estimated to be <b><span style='color:var(--mk-color-red)'>50-75% of the total budget</span></b>.

Thus is is better to **identify systematic & effective approaches** to debugging to <b><span style='color:var(--mk-color-green)'>improve productivity</span></b>.

> [!question] When to do debugging?
> - **Throughout development**
> - **After software has been deployed** (*Product evolution or bugs found*) 

> [!fail] How not to approach debugging
> We can **change the code and try various conditions** until it works.
> 
> This will not work as if we do not understand the underlying cause, just <b><span style='color:var(--mk-color-red)'>changing the code might fix one bug but not others</span></b>.

> [!note] Debugging terminlogies
> - **Mistake**: A <b><span style='color:var(--mk-color-yellow)'>human act or decision</span></b> resulting in an error
> - **Defect** (*bug*): An error in the program code  that <b><span style='color:var(--mk-color-yellow)'>cause the initial fault</span></b>
> - **Fault**: <b><span style='color:var(--mk-color-yellow)'>Location</span></b> in which the programming error is triggered and we enter an unwanted stare
> - **Failure**: Where the fault becomes <b><span style='color:var(--mk-color-yellow)'>externally visible</span></b>
> 
> ![[Debugging Terminology and Mental Model.png|center]]

## Debugging Approaches
### `Printf` Debugging

The function `printf` comes from <span style='color:var(--mk-color-purple)'>C</span>. But essentially we will be **printing out certain variables onto the console at certain parts of the code**.

With this we can see what are the <b><span style='color:var(--mk-color-yellow)'>various states</span></b> at certain points and the <b><span style='color:var(--mk-color-yellow)'>branches took</span></b> for conditionals.

> [!success] Advantages of `printf`
> - **Simple & intuitive**
> - **Language & tool agnostic**

> [!failure] Disadvantages of `printf`
> - Can be **confusing & unclear**
> - **Forget print statements** in the program code
> - **Require recompilation** of the code
### Logging

It is a <b><span style='color:var(--mk-color-yellow)'>more systematic alternative</span></b> to **adding print statements**. For logging there are multiple debugging levels:

| Message Type |                           Description                           |
| :----------: | :-------------------------------------------------------------: |
|   DEBUG 🐞   |                     General debugging event                     |
|   INFO ℹ️    |                Event for informational purposes                 |
|   WARN ⚠️    |                Even that might lead to an error                 |
|   ERROR ❌    |      An error in the application & is possibly recoverable      |
|   FATAL ☠️   | A fatal event that will prevent the application from continuing |
### Debugger

We can use the <b><span style='color:var(--mk-color-yellow)'>tools offered by the IDE</span></b> to debug. 

Typically we can use the debugger as such:
1) Add **breakpoints**, to pause at certain locations in the code
2) **Stepping** in / over / out of methods (*execute code step by step*)
3) **Inspect program state**. Check on variable stack trace etc

> [!success] Advantages of debugger
> - **More systematic** than `printf` debugging
> - Can **display additional information**
> - Set breakpoints **specific to values**

> [!failure] Disadvantages of debugger
> - **Requires a debugging strategy**, even though it is a useful tool
## Debugging Strategies

We <span style='color:var(--mk-color-orange)'>need</span> some sort of **debugging strategy** because:
- <b><span style='color:var(--mk-color-yellow)'>Program states are typically large</span></b>, making it challenging or infeasible to search everything manually
- It is <b><span style='color:var(--mk-color-yellow)'>not always clear </span></b> whether (*intermediate*) <b><span style='color:var(--mk-color-yellow)'>states are correct or not</span></b>
- <b><span style='color:var(--mk-color-yellow)'>Executions</span></b> might consist of <b><span style='color:var(--mk-color-yellow)'>million of steps</span></b> (*a long time*)
### Scientific Method

Scientific method <span style='color:var(--mk-color-orange)'>process</span>:
1) Formulate a question
2) Come up with an **hypothesis** based on the <b><span style='color:var(--mk-color-yellow)'>knowledge</span></b> obtained while formulating the question that may <b><span style='color:var(--mk-color-yellow)'>explain the observed behavior</span></b>
3) Determining the logical consequences of the hypothesis, **formulate a prediction that can support or refute the hypothesis** . Ideally, the prediction would <b><span style='color:var(--mk-color-yellow)'>distinguish the hypothesis from likely alternatives</span></b>.
4) **Test the prediction** (and thus the hypothesis) in an experiment. If the **prediction holds**, confidence in the hypothesis <b><span style='color:var(--mk-color-green)'>increases</span></b>, otherwise, it <b><span style='color:var(--mk-color-red)'>decreases</span></b>.
5) **Repeat Steps 2-4** until there are <b><span style='color:var(--mk-color-yellow)'>no discrepancies between hypothesis and predictions</span></b> and/or observations (*can try to generalise the hypothesis*).

If our hypothesis did not hold (*use assert statements*), then we will need to **refine our hypothesis**.

> [!info] Refining Hypothesis
> It is essentially <b><span style='color:var(--mk-color-yellow)'>making adjustments to our hypothesis</span></b> based on the observations from testing.

Once we exit step 5 our <b><span style='color:var(--mk-color-yellow)'>hypothesis will becomes a diagnosis</span></b> and we can fix the bug.

> [!info] Diagnosis
> A diagnosis <b><span style='color:var(--mk-color-yellow)'>explains both causality & incorrectness</span></b>. Since it is consistent with observations and it predicts future observations.
### Rubberducking

It is the <b><span style='color:var(--mk-color-yellow)'>process of explaining the problem to someone else</span></b> to revisit observations and come up with hypothesis.

To explain the problem to someone else, you will need to <b><span style='color:var(--mk-color-yellow)'>explain it to yourself</span></b>. And by doing so you will get a <b><span style='color:var(--mk-color-green)'>better understanding</span></b> of the problem and may <b><span style='color:var(--mk-color-green)'>naturally find the solution</span></b>. 
# Program Slicing
---
When debugging we **want to know which part of the code** or variables influenced the current erroneous state.

it can also extend from just debugging, a developer can:
- **Better understand** the code
- Carry out **maintenance**
- Perform **security analysis**

> [!info] Slicing
> Extracts a subset of the <b><span style='color:var(--mk-color-yellow)'>program that potentially affects variables</span></b> at a certain program location.

> [!success] Advantages of slices
> - **Rule out parts of the programs that have no effect on the failure**, thus we <b><span style='color:var(--mk-color-yellow)'>focus only on the important parts</span></b>.
> - **Bring possible origins that may be scattered across the code**, classes, functions are all in different locations & slicing bring them all together

There is no need for the whole code as we just need the parts that cause the issue. It can help as a <b><span style='color:var(--mk-color-green)'>mental model</span></b> or implemented as a <b><span style='color:var(--mk-color-green)'>tool</span></b> (*some IDEs*).

There are <span style='color:var(--mk-color-orange)'>2 types of slicing</span>:
1) **Static** slicing: Given a variable that is incorrect, what is the relevant subset (*manually trace the execution path*)
2) **Dynamic** slicing: Same thing but we are now <b><span style='color:var(--mk-color-yellow)'>given a concrete execution</span></b>. (*just need to follow the executed path*), this is <b><span style='color:var(--mk-color-green)'>better for debugging</span></b>.

There are also <span style='color:var(--mk-color-orange)'>2 approaches to slicing</span>:
1) **Backwards** slicing: To find what influenced a value, <b><span style='color:var(--mk-color-green)'>better suited for debugging</span></b>
2) **Forwards** slicing: What statements influenced by the value
## Tracking Origins

This is another **debugging strategy**. Start from a invalid state and <b><span style='color:var(--mk-color-yellow)'>recursively go back to its previous states</span></b> to <b><span style='color:var(--mk-color-yellow)'>find the origin</span></b> of the issue.

> [!question] How can we determine where to go back to?
> Starting from the observed failure we can determine the fault by <b><span style='color:var(--mk-color-yellow)'>inspecting individual variables</span></b> that are part of the state.

Typically for a **state to transition to another state** there are <span style='color:var(--mk-color-orange)'>2 program dependencies</span>:
1) **Data** dependency, is essentially our arguments, variables & return value
2) **Control** dependency are our conditional statements or iterative loops
### Dependency Graph

We can <b><span style='color:var(--mk-color-yellow)'>visualise the dependencies</span></b> in something called a <b><span style='color:var(--mk-color-turquoise)'>dependency graph</span></b>.

![[Images/CS3213 Images/Dependency Graph Example.png|center]]


> [!important] Dependency graph representation
> For **control dependencies**, the arrow is <b><mark style='background:var(--mk-color-yellow)'>dashed</mark></b>.
> 
> For **data dependencies**, the arrow is <b><mark style='background:var(--mk-color-yellow)'>a solid line</mark></b>.
# Statistical Fault Localization
---
It is to utilize <b><span style='color:var(--mk-color-yellow)'>multiple executions for localizing faults</span></b>. It is a part of **statistical debugging** where we use <b><span style='color:var(--mk-color-yellow)'>statistical reasoning for debugging</span></b>.

> [!info] Fault localization
> Is a set of code which is the <b><span style='color:var(--mk-color-yellow)'>source of the problem</span></b> or error.

Weather a program fails or passes all depends on the events that precede it. However correlation does not imply causation, but it can help locate faults.

The intuition of this is to, run a test case and **see which lines were executed**. If the test case fails then the <b><span style='color:var(--mk-color-yellow)'>fault lies in one of the executed lines</span></b>, and we can just focus on those with other inputs (*automatic program repair*).

> [!abstract] Some hypothesis on statistical debugging tools adoption
> Hypothesis 1 Programmers who debug with the assistance of automated debugging tools **will locate bugs faster** than programmers who debug code completely by hand.
> > Conclusion: helps experts on easy debugging task
> 
> Hypothesis 2 The **effectiveness** of an automated tool **increases with the level of difficulty** of the debugging task.
> > No support
>
> Hypothesis 3 The **effectiveness** of debugging when using a ranking based automated tool is affected by the **rank of the faulty statement**
> > No Support
## Tarantula

It is a <b><span style='color:var(--mk-color-yellow)'>statistical debugging technique</span></b>, and it is an instance of a spectrum-based fault localization technique

> [!important] Intuition behind tarantula
> Program <b><span style='color:var(--mk-color-yellow)'>elements that are executed by a failing test are more likely to be faulty</span> </b> (*i.e., suspicious*) than those primarily executed by passing test cases.

**Formula for suspiciousness**
$$
\text{Suspiciousness}(\text{line}) = 
\frac{\frac{\text{failed}(\text{line})}{\text{total failed}}}
{\frac{\text{failed}(\text{line})}{\text{total failed}} + \frac{\text{passed}(\text{line})}{\text{total passed}}} 
= \frac{\%\text{failed}(\text{line})}{\%\text{failed}(\text{line}) + \%\text{passed}(\text{line})}
$$
Where:
- $\%failed(line)$ is the **number of failing test cases** where the line was executed
- $\%passed(line)$ is the **number of passing test cases** where the line was executed

We can **visualise the scores** by using some <span style='color:var(--mk-color-orange)'>color</span> (*hue*):
- <b><span style='color:var(--mk-color-red)'>Red</span></b> means suspicious (*0*)
- <b><span style='color:var(--mk-color-yellow)'>Yellow</span></b> is somewhere in-between (*0.5*)
- <b><span style='color:var(--mk-color-green)'>Green</span></b> means its safe (*1*)

$$
\text{color hue}(\text{line}) = \text{low color (red)} + 
\frac{\%\text{passed}(\text{line})}{\%\text{passed}(\text{line}) + \%\text{passed}(\text{line})} 
\times \text{color range}
$$
> [!warning] High suspicion does not mean the root of the problem
> While a line with a high suspicion is related to the defect, it does not mean it is the cause of it.
> 
> Thus it does <b><span style='color:var(--mk-color-red)'>not give further information to help localize the fault</span></b>.
# Test Case Reduction
---
We do not need complex inputs to find the majority of bugs, as mentioned in the <b><span style='color:var(--mk-color-turquoise)'>small scope hypothesis</span></b>.

> [!info] Small scope hypothesis
> A high proportion of errors can be found by **testing** a program for <b><span style='color:var(--mk-color-yellow)'>all test input within some small scope</span></b> (*use small and simple outputs*).

Essentially we are <b><span style='color:var(--mk-color-yellow)'>taking a test input and reducing it to a simpler test input</span></b> which will return the same result when passed into the test oracle.
## Binary Search

A naive approach will be to use [[Searching#Binary Search|binary search]]. For a failing test case:
- If we **use the right half** and the test case still fails then we remove the left half
- Else **use the left half** if the bug triggers remove the right half

However it will not work, what if **both halves pass the test case**, that means we <b><span style='color:var(--mk-color-red)'>need to use the full length</span></b>.
## Delta Debugging

Systematically removes elements from the bug inducing input. Behaves like binary search but <b><span style='color:var(--mk-color-yellow)'>tries different combinations of smaller blocks</span></b> where binary search fails.

**Algorithm for delta debugging**:
![[Delta Debugging Algorithm.png|center]]

> [!example] An easy to understand example of the delta debugging algorithm
> 1) Lets say we have N = n (*the algorithm starts with 2*), and partition the input into n partitions
> 2) We will have n partitions as well as n complements (*portion excluded from the partition*)
> 3) Run the test case on each of the n partitions, all partitions passes, then do the same for the complements
> 4) After step 3 there will be 4 possible outcomes
> 	- If everything passes and n is the same as the augmented input then **that is our reduced input**
> 	- If everything passes, increase n by `max(lenth(augmented input), 2n)`
> 	- If one partition fails, then the next iteration, focus on this partition only and set n to be 2
> 	- If one complement fails, the next iteration, focus on this complement and set n to be `min(n - 1, 2)`
> 	

However, delta debugging is <b><span style='color:var(--mk-color-red)'>not optimal</span></b>. It will **give a local minima** (*1-minimality*) of the reduced input. Finding the global minimum is very expensive ($2^{size}$).

> [!success] Advantages of reducing the bug
> - **Easier to debug and analyze the reason of bug**
> - **Help in identifying duplicate bug-inducing test cases**
> - **Easier to communicate the bug**

> [!failure] Challenges of reducing the bug
> - Interestingness test can be **complex**
> - Delta Debugging might be inefficient for highly structured languages (*additional reduction approaches such as hierarchical delta debugging have been proposed*)
# Isolating Failure-Inducing Changes
---
Sometimes a project might have a <b><span style='color:var(--mk-color-turquoise)'>regression bug</span></b> where <b><span style='color:var(--mk-color-yellow)'>over a few iterations of changes something does not work</span></b>.

We can technically use automated testing to detect newly-introduced bugs but it might not always work. 

A **naive approach** will be to just <b><span style='color:var(--mk-color-yellow)'>go through all past versions</span></b> (*we can use git*) and check if the issue is triggered. However it is <b><span style='color:var(--mk-color-red)'>not effective</span></b> and it might have <b><span style='color:var(--mk-color-red)'>many changes</span></b> (*we can optimise using binary search*).
## Git Bisection

A better way will be to automate this process and git has a functionality called **bisection** which automatically does this for you.

> [!tldr] How to use bisect
> 1) Find 2 versions to test one
> 2) Indicate which is good and which is bad
> 3) Run our test case
> 4) GitHub will then show what are the changes which can potentially cause the issue 

We can also do all this in a <span style='color:var(--mk-color-orange)'>test script</span>:
- It (re)builds the program under test for the given version
- It tests whether the failure is present.
- Its exit code indicates the test outcome:
	- 0 means "good" (the failure did not occur)
	- 1 means "bad" (the failure did occur)
	- 125 means "undetermined" (we cannot decide if the failure is present or not)

