---
Title: Code Coverage Metrics
Date Created: 24-January-2026
Last Updated: 02-February-2026
Tags:
  - CS4218
  - SWE/TestMetric/CodeCoverage
---
# Code Coverage Metrics
--- 
We want to <b><span style='color: #FFD700'>quantitatively assess</span></b> the extent of our testing, **code coverage** does gives us an indicator that we have <b><span style='color: #FFD700'>tested enough</span></b>.

Code coverage helps us <b><span style='color: #FFD700'>know the % of code that was covered</span></b> (*the higher it is the more code are tested*). Not only that but it <b><span style='color: #98FB98'>access the thoroughness of the test suite</span></b>.

>[!fail] Code coverage does not guarantee quality tests
>```java
>Public static bool WasLastStringLong {get; private set;}
>public static bool IsStringLong(string input){
>	bool result = input.Length > 5;
>	WasLastStringLong = result;
>	return result;
>}
>public void Test(){
>	bool result = IsStringLong("abc");
>	Assert.Equal(false, result);
>}
>```
>Here you can see we achieve 100% code coverage but we did not verify that the `WasLastStringLong` is set to the correct value even though it is obvious. So this is not a good quality test.

>[!failure] Does not consider codes from external dependencies
>If we were to use **external dependencies**, typically code coverages <b><span style='color: var(--mk-color-red)'>does not take those into account</span></b>. Only code that you have written will be considered.

## Function Coverage

It simply measures <b><span style='color: #FFD700'>how many functions or methods</span></b> in the codebase are <b><span style='color: #FFD700'>executed at least once during testing</span></b>.

>[!info] Broad & highest level in code coverage

It follows the following **equation** to compute function coverage:
$$
\text{Function Coverage} = \frac{\text{Number of functions called}}{\text{Total number of functions}} \times 100
$$

>[!success] Quickly identify untested functions
>Which may contains hidden bugs

>[!success] Ensures ensure all major logic blocks are exercised

>[!fail] Does not reveal if the function was fully exercised internally
>A function might be called but it <b><span style='color: var(--mk-color-red)'>does not mean every line of code within the function was executed</span></b>.
## Statement Coverage

Also known as <b><span style='color: #87CEEB'>code or line coverage</span></b> as well. It measures <b><span style='color: #FFD700'>how many individual lines of code</span></b> have been executed during testing.

>[!info] The most common metric used & is often used in unit testing

It follows the following **equation** to compute statement coverage:
$$
\text{Statement Coverage} = \frac{\text{Number of statement executed}}{\text{Total number of statements}} \times 100
$$

>[!success] Identify untested parts of the codebase

>[!success] Encourages writing tests that exercise all code paths

>[!fail] Does not guarantee that all logical branches or conditions have been tested
>For example an `if` statement has 2 possible outcomes. Our test case can be for when the `if` statement is true which counts as that line being covered. But we did not test when the `if` condition is false.
## Branch Coverage

Also known as <b><span style='color: #87CEEB'>decision coverage</span></b> as well. It measures weather <b><span style='color: #FFD700'>each possible branch from a decision point has been executed</span></b>. Basically it tests all possible outcomes of conditional logic (*if, else, switch case statements*).

>[!info] It is more rigorous than statement coverage

>[!important] It is essential for validation system's core logic

It follows the following **equation** to compute branch coverage:
$$
\text{Branch Coverage} = \frac{\text{Number of branches executed}}{\text{Total number of branches}} \times 100
$$

>[!example] Example of branch coverage
>```cpp
>bool isOdd(int n) {
>	if (n % 2 == 0) {
>		return false; 	
>	} else {
>		return true;	
>	}
>}
>```
>For this simple function to get 100% branch coverage we need 2 test cases, `isOdd(1)` and `isOdd(2)`.

>[!success] It ensures both true & false paths of the conditions are tested

>[!fail] May miss testing all Boolean expressions in complex conditions
## Condition Coverage

It measures if each <b><span style='color: #FFD700'>Boolean sub-expression in a compound condition has been evaluated to both true and false</span></b>. Ensuring every path is fully tested.

In simpler terms, it means it means that <b><span style='color: #FFD700'>each individual argument in the condition must be tested to be true & false</span></b>.

>[!question] Why do we do condition coverage?
> This is required as <b><span style='color: #FFD700'>some combination of sub-expression can cause errors</span></b>.

>[!info] Most rigorous and garnular out of all the coverages & is important for mission critical logic

>[!example] Example of condition coverage
>```cpp
>bool test(int a, bool b, bool c) {
>	if (a == 1 && (b || C)) {
>		return false; 	
>	} else {
>		return true;	
>	}
>}
>```
>For this function to get 100% condition coverage we need a few test cases where:
>- `a = 1` (*the others can be any value same for the following*)
>- `a != 1`
>- `b = True`
>- `b = False`
>- `c = True`
>- `c = False`
 >
> You can see each sub expression (*a, b, c*) has seen to be both true and false.

It follows the following **equation** to compute condition coverage:
$$
\text{Condition Coverage} = \frac{\text{Number of conditions evaluated to both True and False}}{\text{Total number of condition outcomes}} \times 100
$$

>[!important] 100% condition coverage does not guarantee 100% branch coverage
>And vice versa as well.

>[!success] Helps identify potential logic errors in testing complex logical expression

>[!success] Tests deeper than branch coverage
>As it <b><span style='color: #FFD700'>tests individual conditions</span></b> not just the outcome.
## Branch Condition Coverage

It is a **combination of branch & condition** where:
- We need to ensure each condition is evaluated to true & false
- And also each possible decision point is evaluated to true & false
## Path Coverage

It's the **strongest criterion** as every path of the program is covered. However it is <span style='color:var(--mk-color-red)'>very difficult to achieve 100%</span> due to its [[Year 3/Sem 2/CS4218 - Software Testing/Control Flow Testing.md#Core Concepts for Control Flow|infinite possibilities]].

> [!question] Why is it difficult to achieve 100%?
> If we have 10 conditions then we will have $2^{10}$ paths which is a lot, and if we have an unbounded loop we will have infinite paths.

$$
\text{Path coverage} = \frac{\text{paths covered}} {\text{total paths}} \times 100\%
$$
While an integer input it has a upper limit based on type. Things like strings have an infinite length.
## Multiple Condition Coverage

Here <b><span style='color: #FFD700'>all combinations of truth values in each decision must occur at least once</span></b> to reach full coverage.

>[!example] Example of multiple conditions coverage
>```cpp
>bool test(int a, bool b, bool c) {
>	if (a == 1 && (b || C)) {
>		return false; 	
>	} else {
>		return true;	
>	}
>}
>```
>For this function to get 100% multiple condition coverage we need a few test cases where:
>
>| a == 1 |   b   |   c   |
| :----: | :---: | :---: |
| False  |       |       |
|  True  | True  |       |
|  True  | False | True  |
|  True  | False | False |
>
> Technically we need $2^{3} = 8$ tests but <b><span style='color: #FFD700'>some languages like C++ performs short-circuit evaluation</span></b>. So we do not really need all 8 test cases.
> 
> >[!important] For this course we do not consider short circuit-evaluation, it will evaluate all sub-conditions 

>[!info] Most granular of the code coverage metric

>[!fail] We need more exhaustive test cases to test all logic paths