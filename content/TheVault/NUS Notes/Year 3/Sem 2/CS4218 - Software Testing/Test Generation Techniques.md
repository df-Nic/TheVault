---
Title: Test Generation Techniques
Date Created: 06-February-2026
Last Updated: 01-May-2026
Tags:
  - CS4218
  - SWE/Testing/TestCaseFormulation
---
# Is Control Flow Testing Not Enough?
---
In [[Year 3/Sem 2/CS4218 - Software Testing/Control Flow Testing.md|control flow testing]], it allows us to **analyse the control flow of a program** (*the various paths*) which can help us identify meaningful test inputs.

However this itself can be **inadequate**:
- There are a <b><span style='color: var(--mk-color-red)'>large number of potential inputs</span></b>. Control flow testing only shows is the potential paths but we still need to decide which input values to use. Thus we need some way to <b><span style='color: #FFD700'>scope it down</span></b>
- It might <b><span style='color: var(--mk-color-red)'>not always catch edge cases</span></b> (*subtle bugs*)

>[!warning] Lets take the most rigorous coverage [[Code Coverage Metrics.md#Path Coverage|path coverage]], we might still miss out some edge cases
> So this shows that <b><span style='color: var(--mk-color-red)'>control flow testing might not be enough on its own</span></b>.

So **test generation techniques asks which test inputs are the best to choose**.
# Test Generation Terminologies
---
Before continuing we need to understand some terminologies. To start we need to know what is a **test case & a test suite / set**.

|       Term       |                                                              Definition                                                              |
| :--------------: | :----------------------------------------------------------------------------------------------------------------------------------: |
|    Test case     | A test case consisting of a combination of <b><span style='color: #FFD700'>input data & the corresponding expected output</span></b> |
| Test suite / set |                   A <b><span style='color: #FFD700'>collection of test cases</span></b> becomes a test suite / set                   |
## Test Requirements & Specifications

Test requirements and test specifications are different, in that <b><span style='color: #FFD700'>test requirements is used to derive test specification</span></b>.

|        Term        |                                                                                                Definition                                                                                                 |
| :----------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|  Test Requirement  | It <b><span style='color: #FFD700'>indicates how to test a program</span></b>, based on how the program should behave & it <b><span style='color: #FFD700'>describes the objective of the test</span></b> |
| Test Specification |             An <b><span style='color: #FFD700'>exact specification of values</span></b> (*input, global variables, expected values (output) & environment variables*) to be used for testing              |

>[!info] "Expect" part of test specification
> Apart from what was stated, <b><span style='color: #FFD700'>all observable effects must be specified here</span></b>.
> 
> Essentially anything that changes the system state of an external environment.

>[!example] Example of how both are different
>So given a function `isIntegerPositive` one possible **test requirement** is, "program returns true for integers more than 0" (*sounds like its describing functionality*).
>
>Then for the **test specification** it will be input value = 5 & expected output is true.
>
>We can do the same for negative numbers / inputs.

There is <b><span style='color: #FFD700'>not always a 1-1 correspondence between test requirement & specification</span></b>. Sometimes, 1 test specification can satisfy multiple test requirements.

>[!success] The fewer the test the better
>But <b><span style='color: #98FB98'>only if the test are of good quality</span></b>. We want to be efficient without sacrificing thoroughness.

>[!fail] Combining test requirements for 1 test case / specification might not be good when considering error conditions
>Typically when testing error conditions, it will be in its own test case for isolation & verification.
>
>>[!example] Example of why it is not a good idea to combine test requirements for 1 test specification when checking for error conditions
>>```java
>>if (speed_dial < 0 || speed_dial > 120) {
>>	error_exit(“Invalid input values!”);
>>if (zone < 6 || zone > 10) { // Zone < 6 is the error here
>>	error_exit(“Invalid input values!”);
>>}
>>```
>>Assuming the following code & out input is `speed_dial = - 1` & `zones = 3`. Our test requirement is that an error is thrown when `speed_dial < 0` & `zones < 5`. However, with this input we will only hit the first error before exiting the function & never hitting the 2nd error.

But **between test specifications**, try and <b><span style='color: #FFD700'>avoid reusing the same values of a variable</span></b>.
# Test Generation Techniques
---
![[List of Test Generation Techniques.png|center]]
## Equivalence Partitioning (EP)

The <b><span style='color: var(--mk-color-red)'>input domain is usually too large</span></b> for exhaustive testing. Thus, we want to <b><span style='color: #FFD700'>find meaningful regions of input data</span></b> to generate test cases.

The idea is to <b><span style='color: #FFD700'>partition the input domain into a finite number of sub-domains</span></b> to select test inputs. These sub-domains are also <b><span style='color: #FFD700'>called equivalence class</span></b>.

Partition based on the <b><span style='color: #87CEEB'>equivalence relations</span></b> which are <b><span style='color: #FFD700'>essentially the functionality of the code</span></b>.

These partitions can be:
- **Non-overlapping** partitions
The partitions do not overlap (*disjoint between one another*)

>[!important] Each equivalence class serves as a source of at least 1 test input
>We cannot have a partition and not use it as a test input. Because our goal is to test all equivalence partitions.

- **Overlapping** partitions 
Now the partitions <b><span style='color: #FFD700'>can overlap one another</span></b>. 

![[Selecting Regions for Overlapping partitions.png|center|450]]

You can visualise the <b><span style='color: #FFD700'>circle as the input space with all possible combinations of all the inputs</span></b>. Thus when you partition by a particular input variable, there will be mixed values for the rest of the inputs.

>[!warning] Not every 2 input or more function will guarantee to have overlapping partitions
>For example if there are impossible input combinations take for instance, payment type and credit card number. If we partition by payment type you can tell that those under cash will not have a card number and thus the partitions are not overlapping.

So instead of looking at each partition for 1 input, we now look at <b><span style='color: #FFD700'>every region formed by the intersections should be covered by at least 1 test case</span></b>.

>[!question] How do we partition?
>We need to <b><span style='color: #FFD700'>consider the program behavior</span></b>.
>>[!example] Example of how to partition the input domain
>>Lets say we have this function:
>>```java
>>public static void performTask(int x) {
>>	if (x < 0) {
>>		performTaskOne();
>>	} else {
>>		performTaskTwo();
>>	}
>>}
>>```
>>
>>We can tell that for all values `x < 0` behaves the same while `x >= 0` will behaves the same.
>>So our 2 partitions or equivalence classes will be:
>>- `x < 0`
>>- `x >= 0`

These partitions are also called <b><span style='color: #87CEEB'>equivalence classes</span></b> is because we assume that **all inputs are equivalent** (*can consist of more than 1 input variable*), meaning if <b><span style='color: #FFD700'>one test input reveals an error so will the rest within this partition</span></b>.

**Guidelines** for partitioning:

|           Case            |                                     Guideline                                      |                                Example                                |
| :-----------------------: | :--------------------------------------------------------------------------------: | :-------------------------------------------------------------------: |
| A single sided conditions |                    Identify 1 region within & the other outside                    |            Condition:`X < a`<br>1) `X < a`<br>2) `x >= a`             |
|    A bounded condition    |              Identify 1 region within & the 2 above & below the range              | Condition:`b < X < a`<br>1) `b < X < a`<br>2) `x >= a`<br>3) `x <= b` |
|     A specific value      |          Identify 1 region as the value and the other as all other values          |           Condition: `X == 2`<br>1) `X == 2`<br>2) `X != 2`           |
|     A member of a set     | Identify 1 region within the set and the other as all other values outside the set |     Condition: `X` is even<br>1) `X % 2 == 0`<br>2) `X % 2 != 0`      |

>[!note] We can also do equivalence partitioning on output variables as well
>For output values also <b><span style='color: #FFD700'>consider invalid outputs as well</span></b>.
>
>But for this course by default if it is not stated it will be input based.
## Boundary Value Analysis (BVA)

It is closely similar to [[Year 3/Sem 2/CS4218 - Software Testing/Test Generation Techniques.md#Equivalence Partitioning (EP)|equivalence partitions]] where we need to identify the partitions. Then we focus on <b><span style='color: #FFD700'>boundary values within a partition</span></b>.

>[!question] Why look at the boundary?
>Even with control flow & equivalence testing we might <b><span style='color: #FFD700'>miss finding bugs that happen at the edges</span></b>.
>
>But more importantly, <b><span style='color: #FFD700'>because errors are more likely to occur at the boundary</span></b>.

>[!note] BVA can also be applied to output variables
>So our output domain can have a set of equivalence classes & we can <b><span style='color: #FFD700'>find test input that covers each output equivalence classes</span></b>.
>
>But output is different as outputs <b><span style='color: #FFD700'>can also include those that the function cannot output</span></b>, but they are excluded when writing testcases.

There are **2 types** of BVA:
1) **1 dimensional** BVA

First <b><span style='color: #FFD700'>identify the boundary values</span></b> then **consider test cases** for:
- <b><span style='color: #FFD700'>Below</span></b> the boundary
- <b><span style='color: #FFD700'>On</span></b> the boundary
- <b><span style='color: #FFD700'>Above</span></b> the boundary

>[!important] Boundary values is not the same as the test cases from boundary value analysis
>Boundary values are the values on the boundary.

>[!example] Example of a 1 dimensional BVA
>Assume that a code does the following check `10 <= X <= 20`. Then our boundary is `X = 10` & `X = 20` & `X = 9` & `X = 21`.
>
>So our 6 test cases are:
>- `X = 8` (*below*)
>- `X = 9` (*on*)
>- `X = 10` (*on*)
>- `X = 11` (*above*)
>- `X = 19` (*below*)
>- `X = 20` (*on*)
>- `X = 21` (*on*)
>- `X = 22` (*above*)

2) **2 dimensional** BVA

Here our values lie on a 2 dimensional plane & it is more complicated to figure out all test case inputs.

>[!example] Example of a 2 dimensional BVA
>![[2D BVA Example.png|center|450]]
>
>To figure out our test cases we follow a few heuristics:
>
>|                              Heuristics                               |      Case      |
| :-------------------------------------------------------------------: | :------------: |
|                    Select one test at each corner                     |   1, 2, 3, 4   |
|  Select one test just outside each of the four sides of the boundary  |   5, 6, 7, 8   |
| Select one test just inside of each of the four sides of the boundary | 10, 11, 12, 13 |
|             Select one test inside of the bounded region              |       9        |
|             Select one test outside of the bounded region             |       14       |
>
>For a **total of 14 test cases**. But do take note that for string length we cannot go below 0 so we can exclude test case 7.
## Finite State Machines (FSM)

This technique is useful to test generation <b><span style='color: #FFD700'>for state-based programs</span></b> (*we need to ensure the programs internal state as well*).

While [[Year 3/Sem 2/CS4218 - Software Testing/Test Generation Techniques.md#Equivalence Partitioning (EP)|equivalence partitioning]] & [[Year 3/Sem 2/CS4218 - Software Testing/Test Generation Techniques.md#Boundary Value Analysis (BVA)|boundary value analysis]] are useful it <b><span style='color: var(--mk-color-red)'>cannot be easily applied to all programs</span></b>. Which is just the case for state-based programs.

>[!info] State based programs
>It is where the <b><span style='color: #FFD700'>logic depends on the current internal state</span></b> of the program.
>
>>[!example] You can think of it as a traffic light, the next colour depends on the current colour it is on.
>>And there are no EP or BV.

A state machine is a abstract representation of actions or functions that the program can do, we can **represent it as**:

| Part |                                                                                                      Explanation                                                                                                      |
| :--: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|  A   | It is a <b><span style='color: #87CEEB'>finite input alphabet</span></b> where its elements are called letters which are the <b><span style='color: #FFD700'>possible set of inputs</span></b> into the state machine |
|  Q   |                                                        A <b><span style='color: #FFD700'>finite set of states</span></b> that the machine can transition into                                                         |
|  q0  |                                                            The <b><span style='color: #FFD700'>initial state</span></b> of the state machine ($q0 \in Q$)                                                             |
|  T   |                                    It is the <b><span style='color: #FFD700'>state transition function</span></b>, which is the mapping of $T(q, a) \rightarrow q$ where $q \in Q$                                    |
|  F   |                                     It is a <b><span style='color: #FFD700'>finite final states</span></b>, which indicates which state the machine can end in ($F \subseteq Q$)                                      |
**An example of a state diagram**:
![[Images/State Diagram Example.png|center|550]]

>[!note] `reset` is $\in A$

A state machine recognises a <b><span style='color: #87CEEB'>language</span></b>, you can think of this as a <b><span style='color: #FFD700'>series of inputs which goes through valid transitions & ends up in the final state</span></b>. We can define the set of all possible inputs series as $S$.

There are **3 special states**:
1) **Unreachable** states, they are <b><span style='color: #FFD700'>states which cannot be reached from q0</span></b> using any sequence of transitions
2) **Dead** states, they are <b><span style='color: #FFD700'>states which cannot be left once it is reached</span></b> (*end state is also one*)
3) **Error** states, which indicates the system is facing an error

>[!example] Example of the 2 special states
>![[Unreachable & Dead States Example.png|center|400]]

So after **translating** the code or problem description to a state diagram, we can derive test cases to achieve **2 types of coverage**:

|      Coverage       |                                                                                                                   Definition                                                                                                                   |
| :-----------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|   State coverage    |                                                              To achieve 100% state coverage, every <b><span style='color: #FFD700'>state must be reached at least once</span></b>                                                              |
| Transition coverage | To achieve 100% transition coverage, <b><span style='color: #FFD700'>every transition must be exercised at least once</span></b>. We can never have duplicate transitions if we use the given definition of state machines, because T is a set |

>[!important] These test cases must end at an end state
## Decision Tables

This method is useful for generating test cases <b><span style='color: #FFD700'>for programs with complex decision logic</span></b> by providing a <b><span style='color: #98FB98'>simple & systematic</span></b> way to handle combinations of different input conditions.

>[!info] Cause-effect tables
> Decision tables are also known as cause-effect tables as it <b><span style='color: #FFD700'>illustrates under what conditions will an action will be performed</span></b>.

Here are **key elements** in a decision table:

|     Element     |                                                                                               Description                                                                                                |
| :-------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|   Conditions    |                                                       The <b><span style='color: #FFD700'>inputs</span></b> or factors that influence the outcome                                                        |
|     Actions     |                                                           The possible results or <b><span style='color: #FFD700'>system behaviours</span></b>                                                           |
|      Rules      |                                   Combinations of <b><span style='color: #FFD700'>conditions which trigger specific actions</span></b> ($C1 \land C2 \rightarrow A1$)                                    |
| Table Structure | Conditions are on the left, actions on the right. <b><span style='color: #FFD700'>Each column represents a specific rule</span></b> which is a combination of conditions leading to a particular outcome |

Here are some **terminologies** which are used within decision tables:

|    Terminology     |                              Explanation                              |
| :----------------: | :-------------------------------------------------------------------: |
|         C          |                          Denotes a condition                          |
|         A          |                           Denotes an action                           |
|         Y          |                            Denotes `true`                             |
|         N          |                            Denotes `false`                            |
|         X          |                      Denotes action to be taken                       |
| Blank in condition | Denotes that the conditions does not affect the rule or the condition |
|  Blank in action   |                 Denotes that no action will be taken                  |
So to **create a decision table**:
1) Identify the conditions
2) Identify the actions
3) Determine the rules (*condition + action*)
4) Fill up the table

<b><span style='color: #FFD700'>Each action usually indicates 1 rule</span></b>. And with the table <b><span style='color: #FFD700'>each rule corresponds to 1 test requirement</span></b>.

>[!example] Example of generating a decision table & using it to form a test case
>Assuming we have the following **conditions & actions**:
>
>
| S/N |              Condition               |
| :-: | :----------------------------------: |
| C1  |    The account number is correct     |
| C2  |        The signature matches         |
| C3  | There is enough money in the account |
>
>| S/N |                       Action                       |
| :-: | :------------------------------------------------: |
| A1  | Give statement indicating incorrect account number |
| A2  |          Give money           |
| A3  |    Give statement indicating insufficient funds    |
| A4  |         Call the police to check for fraud         |
>
>Then we can form the **following rules** based on how the application should perform:
>
>| S/N |                                     Rule (Logic)                                     |
| :-: | :----------------------------------------------------------------------------------: |
| R1  |    A1 is to be performed when C1 is false, regardless of the values of C2 and C3     |
| R2  | A4 is to be performed when C1 is true and C2 is false, regardless of the value of C3 |
| R3  |            A3 is to be performed when C1 and C2 are true, and C3 is false            |
| R4  |                  A2 is to be performed when C1, C2 and C3 are true                   |
>
>Then we can finally form the decision table:
>
>| S/N | R1  | R2  | R3  | R4  |
| :-: | :-: | :-: | :-: | :-: |
| C1  |  N  |  Y  |  Y  |  Y  |
| C2  |     |  N  |  Y  |  Y  |
| C3  |     |     |  N  |  Y  |
| A1  |  X  |     |     |     |
| A2  |     |     |     |  X  |
| A3  |     |     |  X  |     |
| A4  |     |  X  |     |     |
> 
> Lets look at rule 3 so if we look at the table, if C1 is true (*Y*) & C2 is true (*Y*) but C3 is false (*N*) then A3 is performed (*X at where A3 is*).
> 
> So for rule 2, we can either have the following test inputs as our test case resulting in A4 being performed:
> - C1 is true, C2 is false & C3 is true
> - C1 is true, C2 is false & C3 is false 
