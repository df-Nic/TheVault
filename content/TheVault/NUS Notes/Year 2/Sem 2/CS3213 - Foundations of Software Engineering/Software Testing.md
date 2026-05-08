---
Title: Software Testing
Date Created: 28-November-2025
Last Updated: 24-January-2026
Tags:
  - CS3213
  - SWE/Testing
---
# What is Testing
---
We do testing to <span style='color:var(--mk-color-yellow)'>find bugs or defects</span>, or to ensure that the <span style='color:var(--mk-color-yellow)'>features corresponds to the requirements</span> of the systems.

We can also do <span style='color:var(--mk-color-yellow)'>formal proof</span> to <span style='color:var(--mk-color-yellow)'>show that a program is bug free</span>.

It is **important to do testing early** due to the shifting left concept, the later you do testing the <span style='color:var(--mk-color-red)'>more costly</span> it will be.

There are <span style='color:var(--mk-color-orange)'>2 measurements</span> to consider when testing, **verification** & **validation**.

> [!info] Verification
> Check if we build the product correctly, it should be<span style='color:var(--mk-color-yellow)'> bug free and works as intended</span>.

> [!info] Validation
> Check if we have built the right product, it <span style='color:var(--mk-color-yellow)'>should do what the user requires</span>.

To **do a test** we will need <span style='color:var(--mk-color-orange)'>2 components</span>:
1) **Test oracle**: It is a mechanism to determine if a test has passed or failed (*Can be functional or non functional*)
2) **Test input**: Resources required for the test (*Arguments, UI, environment, instructions / functions*)

> [!note] Pesticide Paradox
> There are many different kinds of testing, all with their **own advantages & disadvantages**.
> 
> Every method you use to prevent or find bugs leaves a residue of subtler bugs against which those methods are ineffectual.

> [!abstract] Manual vs automated testing
> By default , testing will involve some sort of automation (*JUnit*), however it is different than <span style='color:var(--mk-color-turquoise)'>automated testing</span>, where there is a tool that <span style='color:var(--mk-color-yellow)'>generates inputs and apply to the test oracle</span>.
> 
> <span style='color:var(--mk-color-turquoise)'>Manual</span> (*exploratory testing*) is instead of using test oracles, the <span style='color:var(--mk-color-yellow)'>tester acts as the oracle & manually enters inputs</span>.
# Testing Levels
---
There are <span style='color:var(--mk-color-orange)'>3 tiers</span> to testing:
1) **Unit tests**: Test individual components
2) **Integration tests**: Test with a combination of components
3) **System tests** (*end-to-end*): Evaluate the whole system
## Unit Tests

By component, we mean a <span style='color:var(--mk-color-yellow)'>single unit</span>, it can be a method or a set of related classes.

> [!info] Advantages & disadvantages of unit testing
> > [!success] Advantages
> > - **Fast**: Can <span style='color:var(--mk-color-green)'>test large portions of the system</span> with limited time since the components are small parts. 
> > - **Easy to control**: Typically check expected values with a certain input type
> > - **Easy to write**: There is <span style='color:var(--mk-color-green)'>no additional set up required</span> (*no need databases or web services*)
>
> > [!failure] Disadvantages
> > - **Lack reality**: Does <span style='color:var(--mk-color-red)'>not represent the real execution</span> of the system
> > - **Does not find all bugs**: Some bugs might get <span style='color:var(--mk-color-red)'>triggered after integration</span> with other components
> >  - **Require mocks**: Might have dependencies which requires [[Developer Testing#Stubs|stubs]]
## Integration Tests

We will test multiple components of a system together and <span style='color:var(--mk-color-yellow)'>focus mainly on the interactions between them</span>.

Typically we will focus on 2 parts, **"our" components** (*what we want to test*) & **external component**.
## System Tests

We will <span style='color:var(--mk-color-yellow)'>test the entire system</span> as a whole. 

> [!info] Advantages & disadvantages of system testing
> > [!success] Advantages
> > - **Realistic**: The testing will <span style='color:var(--mk-color-green)'>represent real life usage</span> of the application and bugs that user might face
>
> > [!failure] Disadvantages
> > - **Slow**: It requires many components
> > - **Harder to write**: Some components might <span style='color:var(--mk-color-red)'>require complex setup</span> (*database systems*).
> > - **Prone to flakiness**
### Flakiness

> [!info] Flaky test
> It is a test that might <span style='color:var(--mk-color-yellow)'>non-deterministically pass or fail</span>

If our test cases are flaky, it means that it is <span style='color:var(--mk-color-red)'>difficult to tell weather there is a bug or from the test</span>. In addition <span style='color:var(--mk-color-red)'>debugging will be difficult</span>, lowering developer productivity.

> [!question] Why does it happen?
> - **Concurrency**: Synchronization issues between threads
> - **Async wait**: Asynchronous calls without properly waiting for their result to come available (*waiting for a server to respond*)
> - **Test order dependency**: Tests do not clean up before starting another
> - **Time related issues**: Test case timeouts
> - **Resource leaks**
## Writing Tests

When **determining how much to write** for each type we can follow the <span style='color:var(--mk-color-turquoise)'>test pyramid</span>.

![[Images/CS3213 Images/Test Pyramid.png|center|400]]

Essentially try and write <span style='color:var(--mk-color-yellow)'>fewer high-level tests</span> and <span style='color:var(--mk-color-yellow)'>many small & fast unit tests</span>.

> [!fail] Pyramid antipatterns
> It is just a flip in the pyramid, <span style='color:var(--mk-color-yellow)'>less unit tests and more higher level tests</span>.
> 
> This is <span style='color:var(--mk-color-red)'>not recommended</span> as:
> - **Difficult to maintain**
> - Takes **very long to run**
> - Requires **more debugging effort**

# Testing & Processes
---
## User Acceptance Testing (UAT)

It focuses on validation of the system, ensuring that it <span style='color:var(--mk-color-yellow)'>meets the user requirements</span>. This process involves the customers and contrasts system testing (*all 3 testing levels*).

> [!info] UAT in waterfall models
> After the <span style='color:var(--mk-color-yellow)'>system has been implemented & tested</span>, it will be shown to the users for UAT.

> [!info] UAT in agile
> It will be carried out after the <span style='color:var(--mk-color-yellow)'>end of every sprint</span>.
## Test Driven Development (TDD)

In summary, TDD is to write the <span style='color:var(--mk-color-yellow)'>test cases first</span> and then <span style='color:var(--mk-color-yellow)'>code just enough to pass</span> the test cases that failed. This is <b><mark style='background:var(--mk-color-red)'>not a testing method</mark></b>, but more of a **development method**.

**Steps in TDD**:
1) Write tests (*focus on the happy path, then switch to testing mode later*)
2) Check if any of the tests failed
3) Write simplest code that passes the tests
4) All tests should pass
5) Refactor if needed

> [!success] Advantages
> - **Focuses on requirements**: Since we need to write the tests cases to relate to the requirements
> - **Quick feedback**
> - **Testable code**: As we start off with writing code
> - **Pace is up to us**: If we are confident with the problem we can create a more complicated tests

> [!question] When to use TDD?
> For projects with <span style='color:var(--mk-color-yellow)'>complex or unclear solutions</span>, TDD works better (*exploration & experimentation*). It will <span style='color:var(--mk-color-red)'>not be as good when the solution is clear</span>.

There are many ways to do TDD:
- One is the **inside-out** method where we write unit tests which will compose the overall feature
- The other is **outside-in** where we start from writing test from the outside and use mocking for dependencies.
# Black & White Box Testing Approaches
---
## Black-box Testing

For black-box testing, we <span style='color:var(--mk-color-yellow)'>do not require internal information</span>. This approach follows the <span style='color:var(--mk-color-turquoise)'>specification-based testing</span>.

> [!info] Specification-based testing
> Derives tests based on <span style='color:var(--mk-color-yellow)'>requirements or documentation</span> (*user stories or use cases*).
> 
> It can be used to <span style='color:var(--mk-color-yellow)'>test both functional & non-functional</span> requirements.
### Testing Workflow

1) **Understand the requirements**
> First <span style='color:var(--mk-color-yellow)'>understand</span> the requirements, inputs & outputs
2) **Explore the program**
> <span style='color:var(--mk-color-yellow)'>Know what the program does</span> to understand and build a mental model
3) **Identifying Partitions**
4) **Device test cases**
5) **Automated test cases** (*make the test cases*)
6) **Augment** (*requires creativity & experience to know what special cases will affect the software*)
#### Partitions

When testing a simple component, there are a **infeasibly many inputs**. We will need to <span style='color:var(--mk-color-yellow)'>identify equivalent classes</span> (*[[Code Quality#Equivalence Partitions|partitions]]*) of inputs and outputs.

Essentially we need to <span style='color:var(--mk-color-yellow)'>classify certain values to be in certain partitions</span> (*both outputs & inputs*). Thus we will not need to test every value.

> [!important] Boundary values
> **Inputs at boundaries** are <span style='color:var(--mk-color-yellow)'>more likely to trigger bugs</span>, because the behavior changes from 1 boundary to another.
> 
> Thus <span style='color:var(--mk-color-yellow)'>use 1 value from each side of the boundary</span> when testing. This is known as <span style='color:var(--mk-color-turquoise)'>off-point tests</span> (*on-point tests are values within the boundary*).
## White-box Testing

For white-box testing, we do <span style='color:var(--mk-color-yellow)'>use internal information</span>. This approach follows the <span style='color:var(--mk-color-turquoise)'>structural-based testing</span> and it is <span style='color:var(--mk-color-green)'>good if we are focusing on code coverage</span>.

This **additional information** can be the:
- Source code
- Any documentation

**Applying structural testing**
1) Apply specification-based testing
2) Run a code coverage tool like <span style='color:var(--mk-color-blue)'>Jacoco</span> (*identify missing tests*)
3) For each uncovered code, know why it is not tested and weather or not to implement a test to cover it

> [!question] Why do white-box testing?
> - Forgot about partitions when analysing requirements
> - Know more about the product to do better testing
### Mutation Testing

The <span style='color:var(--mk-color-orange)'>goal of mutation testing</span> is to:
- **Evaluate quality** of existing tests
- **Derive new tests**

It is a **type of white-box testing**, however the idea is to <span style='color:var(--mk-color-yellow)'>purposely inject bugs into the program</span> and if our <span style='color:var(--mk-color-green)'>test cases are strong, it will fail</span>, which means the mutant has been killed. <span style='color:var(--mk-color-green)'>More killed results in better test suite</span>.

However if the **program passes all test cases** then that means we did not kill the mutant and thus a <span style='color:var(--mk-color-red)'>test case has not been covered</span>.

Mutation testing is <span style='color:var(--mk-color-yellow)'>not applicable to all possible scenarios</span> depending on the application and its implementation.

**Carrying out mutation testing**:
1) Select statement in the source code
2) Apply a mutation to it (i.e., create a mutant)
3) Execute the test suite
4) Proceed depending on the outcome
	1) <span style='color:var(--mk-color-green)'>Test case fails: mutant is killed</span>
	2) <span style='color:var(--mk-color-red)'>Test case succeeds: mutant survives</span>
5) Undo the change and continue with 1. until a <span style='color:var(--mk-color-yellow)'>budget is reached or exhaust all possible mutants</span>
6) Return the mutation score
$$
\text{Mutation score} = \frac{\text{number of mutants killed}}{\text{number of mutants}} \times 100
$$

> [!info] Advantages & disadvantages of mutation testing
> > [!success] Advantages
> > - <span style='color:var(--mk-color-green)'>Effective</span> way of **discovering undertested parts**
>
> > [!failure] Disadvantages
> > - **Computationally expensive**: We need to <span style='color:var(--mk-color-red)'>build the software</span> for every mutant and <span style='color:var(--mk-color-red)'>execute the entire test suite</span>
> > - **Equivalent mutants**: Mutants does <span style='color:var(--mk-color-red)'>not guarantee that the program behavior changes</span>
### Coverage Criteria

![[Coverage Criterias .png|center|400]]

For the following coverage criteria, having <span style='color:var(--mk-color-red)'>100% does not mean everything is tested</span>. This coverage criteria should be a <span style='color:var(--mk-color-yellow)'>tool that helps to identify uncovered code</span>.
#### Line Coverage

It is the simplest one which is basically <span style='color:var(--mk-color-yellow)'>how many lines of code was executed after running the test cases</span>.

$$
\text{Line coverage} = \frac{\text{lines covered}}{\text{total lines of code}} \times 100\%
$$
#### Branch Coverage

This is mainly for conditionals (`if`, `for`, `while`) we just need to<span style='color:var(--mk-color-yellow)'> test for the true and false paths</span> are covered
$$
\text{Branch coverage} = \frac{\text{branch covered}}{\text{total branches}} \times 100\%
$$
#### Condition + Branch Coverage

It is an **addon to branch coverage** where we also <span style='color:var(--mk-color-yellow)'>check for each condition and weather it is true or false</span> (*the individual conditions*).

However <b><mark style='background:var(--mk-color-yellow)'>conditional coverage does not imply branch coverage</mark></b>. It is possible that the combinations of conditions does not trigger one of the branches.

$$
\text{Condition and Branch Coverage} = \frac{\text{branch covered} + \text{conditions covered}} {\text{total branches} + \text{total conditions}} \times 100\%
$$

#### Path Coverage

It's the **strongest criterion** as every path of the program is covered. However it is <span style='color:var(--mk-color-red)'>very difficult to achieve 100%</span>.

> [!question] Why is it difficult to achieve 100%?
> If we have 10 conditions then we will have $2^{10}$ paths which is a lot, and if we have an unbounded loop we will have infinite paths.

$$
\text{Path coverage} = \frac{\text{paths covered}} {\text{total paths}} \times 100\%
$$
#### MC / DC Coverage

It is **more practical than path coverage**, <span style='color:var(--mk-color-green)'>less expensive but better than condition + branch coverage</span>. And it is mainly used for safety-critical applications.

It typically requires at least $n + 1$ test cases where $n$ is the number of conditions.

> [!info] Condition
> In a decision a condition is essentially just `a > 10` or `a == true`

When ensuring MC / DC coverage:
- Each **condition** in a decision <span style='color:var(--mk-color-yellow)'>takes every possible outcome</span>
- Each **condition** in a decision <span style='color:var(--mk-color-yellow)'>independently affect the outcome of the decision</span> (*the rest stays the same*).

> [!example] Approach to MC/DC coverage
> ![[MC-DC Coverage Example.png|center]]
> 
> Here are some potential tests:
> - For `isLetter`: {T1, T5}, {T2, T6} , {T3, T7}
> - For `== 's'`: {T2, T4}
> - For `== 'r'`: {T3, T4}
>   
> Notice how **each pair**,<span style='color:var(--mk-color-yellow)'> only the condition changes the rest stays the same</span>.
> 
> Now look at the `decision`, we need at least 1 from `{T1, T2, T3}` and 1 from `{T4, T5, T6, T7, T8}`.
> 
> Now **getting the minimum set** from the 2 conditions, we can either have, `{T2, T3, T4, T6}` or `{T2, T3, T4, T7}`.

