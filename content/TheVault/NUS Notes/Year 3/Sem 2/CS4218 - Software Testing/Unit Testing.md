---
Title: Unit Testing
Date Created: 15-January-2026
Last Updated: 12-March-2026
Tags:
  - CS4218
  - SWE/Testing/UnitTesting
---
# The 5W1H of Unit Testing
---
>[!abstract] Unit Test
>A unit test is an <b><span style='color: #FFD700'>automated test</span></b> that <b><span style='color: #FFD700'>verifies a small piece of code</span></b> (*often known as unit*). And it is <b><span style='color: #FFD700'>carry out in an isolated manner to ensure failure links directly to the component</span></b>.
>
>These test are <b><span style='color: #98FB98'>executed quickly for continuous feedback</span></b>.

So what is unit testing? It is the **responsibility of the software developers** who are writing the code to ensure quality.

The goal of unit testing is to <b><span style='color: #FFD700'>test components individually in isolation</span></b> (*components, functions, methods*), to ensure they <b><span style='color: #98FB98'>work as intended without external interference</span></b>.

Unit tests should be <b><span style='color: #FFD700'>performed early on</span></b> in the software development lifecycle. <b><span style='color: #FFD700'>Often after a piece of code is created</span></b>. These test cases can <b><span style='color: #98FB98'>act as a continuous feedback loop</span></b> to catch bugs the moment they are created.

Testing is <b><span style='color: #FFD700'>conducted on the developers local environment</span></b> using standard testing frameworks like JUnit.

>[!question] So why do we conduct unit testing?
> So that we can:
> - <b><span style='color: #98FB98'>Catch bugs early</span></b>
> - <b><span style='color: #98FB98'>Less costly to fix</span></b> (*Prevents rework in later stages*)
> - <b><span style='color: #98FB98'>Faster debugging</span></b> (*Faster identification*)
> - <b><span style='color: #98FB98'>Ensure code quality</span></b> (*Acts as documentation*)
> - <b><span style='color: #98FB98'>Make future code changes safer & easier</span></b> (*Safety net for refactoring or when adding new features*)
> - <b><span style='color: #98FB98'>Faster development</span></b>
> - <b><span style='color: #98FB98'>Better design</span></b> as it encourages modular, clean and well-structured code to ensure maintainability and extensibility

Typically a test case:
1) Takes a specific input
2) Runs the code
3) Uses an assertion to check if the output matches the expected output

>[!abstract] Method Under Test (MUT)
>It is a **individual method or function** within the software under testing (*SUT*) that the <b><span style='color: #FFD700'>test case is verifying its correctness, behavior or performance </span></b>.
## Why Should Unit Test Be Done Early?

This is due to the <b><span style='color: var(--mk-color-red)'>ripple effect</span></b>. As the more developers code the harder it will be to find and fix bugs.

>[!success] Catch bugs early which reduces cost
>Finding errors in the code during development is easier and cheaper than fixing them after integration or deployment.

>[!success] It ensures all the individual components work correctly before integration
> It prevents larger hard-to-trace problems when different parts of the system are combined.

>[!success] Supports faster & safer development
> Early unit tests acts as a safety net for refactoring or extending code without accidentally breaking existing functionality.
> 
> Improves innovation & productivity & prevents the software from being fragile & difficult to change over time.

<b><span style='color: #FFD700'>Quality unit tests are also important</span></b>, even though there is an <b><span style='color: var(--mk-color-red)'>up front investment in effort at the beginning</span></b>. However in the <b><span style='color: #98FB98'>later stages of development, it will require less effort</span></b> as we can develop without having a pile of bugs.
## Traditional Vs Unit Testing

In **traditional testing** we <b><span style='color: #FFD700'>test the system as a whole</span></b>, individual components rarely get tested which results in <b><span style='color: var(--mk-color-red)'>errors to go undetected</span></b>.

Since everything is already integrated, to <b><span style='color: var(--mk-color-red)'>isolate & find the error can be difficult</span></b> (*time consuming*).

>[!tldr] Traditional testing methods
>- Print statements
>- Using the debugger (*A reactive process*)
>- Debugger expressions
>- High level test scripts (*End to end tests*)

As for **unit testing**, components are tested individually, isolated & at least once. <b><span style='color: #98FB98'>Errors are pickeded up earlier</span></b> when they are the simplest & cheapest to fix because the <b><span style='color: #98FB98'>scope is smaller</span></b> (*we already know which component is causing the issue*).

>[!important] Unit tests must adhere to 4 core principles
>1) **Isolatable** (*Testing 1 thing only without external dependencies*), this <b><span style='color: #98FB98'>allows precise error location</span></b>
>2) **Repeatable**, yielding the exact same result
>3) **Automatable**, running constantly to <b><span style='color: #98FB98'>get immediate feedback on changes</span></b>
>4) **Easy to write**, to ensure that the practice is simple & sustainable
# Structing a Unit Test
---
While we can just write unit tests however we like, but it will be best if it had <b><span style='color: #FFD700'>structure to ensure readability</span></b>.

When writing unit tests we can structure it using the <b><span style='color: #87CEEB'>AAA pattern</span></b>:
1) **Arrange**
This is the setup phase where we <b><span style='color: #FFD700'>prepare everything for the test</span></b>, be it initialising objects, inputs, dependencies or to set up mocks.

2) **Act**
After the setup we can <b><span style='color: #FFD700'>execute the method under testing</span></b>, just call the function with the input and capture the output.

3) **Assert**
Lastly we <b><span style='color: #FFD700'>verify if the actual output matches the expected output</span></b>. Typically <b><span style='color: #DDA0DD'>assertions</span></b> are used to confirm the correct behavior.

>[!example] Example of writing a unit test using the AAA pattern
>```python
>def test_create_user_saves_user_to_database():
>	# Arrange 
>	mock_repo = Mock() 
>	user_service = UserService(user_repository=mock_repo) 
>	user_data = {"name": "Alice", "email": "alice@example.com"}
>
>	# Act
>	user_service.create_user(user_data)
>	
>	# Assert
>	mock_repo.save.assert_called_once_with(User(name="Alice", email="alice@example.com"))
>```

>[!important] Test cases are clean, readable & serves as documentation for the code behavior
>We prevent writing spaghetti code.

There are also **additional aspects in writing good test cases**. One is to <b><span style='color: #FFD700'>ensure that the test focuses on 1 behavior</span></b> (*Single responsibility principle*). This means that our <b><span style='color: #FFD700'>unit test has only one reason to fail</span></b>.

>[!success] Ensure separation of concerns & reduce coupling
>If we test 2 functionality then the later functionality will be dependent on the first one passing.

Another is to <b><span style='color: #FFD700'>name the tests to clearly describe what they check</span></b>. And lastly, use comments or spacing to <b><span style='color: #FFD700'>separate the AAA sections</span></b>.

>[!example] Example of a test case which focuses on 1 behavior
>For instance the `add` function, we should have a test case for adding positive numbers and another separate test case for adding negative numbers.
## 4 Pillars of a Good Unit Test

A unit test have to **balance 4 pillars**:
1) **Protection against regressions**
2) **Resistance to refactoring**
3) **Fast feedback**
4) **Maintainability**
### Protection Against Regressions

This is the <b><span style='color: #98FB98'>fundamental safety net</span></b> which unit tests provides by ensuring new changes does not affect existing ones. It acts as a <b><span style='color: #FFD700'>quick feedback if changes made cause existing code to fail</span></b>.

>[!question] What is regression?
> It is when a previously working code breaks after some changes are made.

To assess how well it protects against regressions consider:
- **How much code** is exercised by the test
- **Complexity** of the executed code
- The **importance** of that code to the business/domain

But in general the **more code the test executes** & **more critical or complex the code is** the <b><span style='color: #98FB98'>more valuable the test is in catching regressions</span></b>.

>[!success] It reduces risk of adding new features
>It ensures bugs are caught, improving code quality
### Resistance to Refactoring

Good tests verify behaviour and not internal implementation. It means that <b><span style='color: #FFD700'>test cases should remain green</span></b> (*pass*) even <b><span style='color: #FFD700'>when the underlying code is refactored</span></b>.

>[!question] Why is this the case?
>Refactoring is the act of changing the code but <b><span style='color: #FFD700'>not the behavior of it</span></b>. Thus the test case should still pass. 

If unit tests are **too coupled** with the implementation details of the code, it will <b><span style='color: var(--mk-color-red)'>produce a false positive</span></b> & making <b><span style='color: var(--mk-color-red)'>developers spend more time fixing tests</span></b> when they can be fixing bugs. So <b><span style='color: #FFD700'>focus on the observable behavior</span></b> to reduce false positives.

>[!abstract] Type 1 (false positive) & type 2  (false negative) errors in testing
> Lowering type 1 will increase the resistance to refactoring while for type 2 it improves the protection against regressions.
> 
> However there is a <b><span style='color: #FFD700'>trade off</span></b>. Making test cases sensitive to catch all bugs (*lower type 2*) makes it more prone to false alarms (*high type 1*).
### Fast Feedback

Our test suits must run quickly to <b><span style='color: #98FB98'>provide immediate feedback</span></b>, keeping the development process fluid. Developers can also run unit tests frequently throughout the development process.

>[!question] What if the tests are slow?
> It delays feedback which <b><span style='color: var(--mk-color-red)'>slows down identification & resolution</span></b> of bugs, <b><span style='color: var(--mk-color-red)'>increasing cost</span></b>.
> 
> Slow test cases causes a **reduction in running** them, <b><span style='color: var(--mk-color-red)'>wasting time in working on broken or incorrect code</span></b>.

>[!success] Fast test case shorten development cycles

>[!success] It gives more confidence in coding
### Maintainability

Tests are long term assets, it must be <b><span style='color: #FFD700'>clean, readable & maintainable</span></b> so that it is a benefit & not a liability over time.

Not only that but they must also be <b><span style='color: #FFD700'>easy & quick to run</span></b> without any additional set up.

>[!question] What if they are long, complex or poorly structured?
> It will be <b><span style='color: var(--mk-color-red)'>harder to debug</span></b> when they fail & <b><span style='color: var(--mk-color-red)'>harder to modify</span></b> when the underlying functionality changes.
> 
> This causes developers to <b><span style='color: var(--mk-color-red)'>not update the test cases</span></b> or <b><span style='color: var(--mk-color-red)'>worse remove them</span></b>.

>[!warning] Do not compress code unnaturally just to make tests shorter
### The Ideal Test Case

>[!important] It is hard to achieve all 4 at once
>Typically amongst the key 3 pillars (*first 3*), 2 will be focused and the other will be compromised.
>
>![[Ideal Test Case Tradeoff.png|center|400]]
>
>For example:
>- **End to end tests** draw back is that it is slow since it covers a lot of code & multiple components
>- **Trivial tests** does not protect & reveal against regressions because its simple that there is no room for errors
>- **Brittle tests** are not resistant to refactoring because it is sensitive to changes in the code (*tests are coupled with implementation details*)

So the best practice is to <b><span style='color: #FFD700'>maximise high maintainability and resilience to refactoring</span></b>. This <b><span style='color: #98FB98'>ensures long term stability</span></b> for the test cases.

As for protection against regression and fast feedback, strive to <b><span style='color: #FFD700'>have a balance with the remaining 2</span></b>. So have some end-to-end testing for protection against regression and some unit tests for fast feedback.
# Test Doubles
---
Typically the main issue with unit tests is to **ensure isolation**. For external dependencies we will require reliable stand-ins which are called <b><span style='color: #87CEEB'>test doubles</span></b>.

>[!info] Test doubles
>They <b><span style='color: #FFD700'>mimic real objects</span></b> but are <b><span style='color: #FFD700'>simplified</span></b> versions of it which is to be used for testing.

These test doubles, <b><span style='color: #98FB98'>reduces system complexity during testing</span></b> & is essential for automated testing. Allowing the unit's behaviour to be tested independently.
## Fakes

![[Fakes Example.png|center|500]]

<b><span style='color: #87CEEB'>Fakes</span></b> are essentially a <b><span style='color: #FFD700'>replica of an object but with simplified implementations</span></b>. They act like real components but are <b><span style='color: #FFD700'>not production grade code</span></b>.

Often they <b><span style='color: #98FB98'>take shortcuts to reduce complexity</span></b> like:
- Skipping real connections to the database or the network
- Use <b><span style='color: #FFD700'>pre-computed responses or data</span></b>.

These **shortcuts makes the fakes**, <b><span style='color: #98FB98'>fast & reliable</span></b>.

>[!important] Fakes follows the programming to an interface principle
> Code is written to <b><span style='color: #FFD700'>depend on the interface & not the specific implementation</span></b>. As long as the real and <b><span style='color: #FFD700'>fake objects use the same interface</span></b> they can be interchangeable.
> 
> This <b><span style='color: #98FB98'>allows for modular & highly testable software</span></b>.

>[!success] Enables faster integration tests

>[!success] Ideal for testing service logic without involving heavy external systems

>[!success] Allows developers to focus on 1 component at a time

>[!fail] Manual labour
>Every interface we <b><span style='color: var(--mk-color-red)'>write repetitive boilerplate code</span></b> which can be time consuming to maintain on large projects.

>[!fail] Inflexible
>This fake class is mostly hardcoded making it <b><span style='color: var(--mk-color-red)'>difficult to test failure scenarios</span></b> (*like a database exception*). To test this we need to change the fakes which increases complexity & requires maintainability.

>[!note] Fakes are not only for testing, but can be used for development
> It can use <b><span style='color: #FFD700'>used for prototyping & spikes</span></b> which <b><span style='color: #98FB98'>defers complex decisions & reduce initial complexity</span></b>.
> 
> Thus allowing developers to validate business logic and the UI.
## Mocks

![[Mock Example.png|center|500]]

For <b><span style='color: #87CEEB'>mocks</span></b> we instruct it to <b><span style='color: #FFD700'>behave deterministically under certain conditions</span></b> (*what to return*). Then we can <b><span style='color: #FFD700'>check if all expected actions are performed</span></b> (*verify behaviour*). 

>[!important] We use assertions on the mock itself to check the behavior is intended

But we <b><span style='color: var(--mk-color-red)'>cannot check if this function executed for real</span></b>, however this is not the focus as we mock external dependencies to isolate the system under test.

>[!question] So how does mock works?
>
>We can instruct the mock what to return when the function is called while also recording which functions were called with what arguments.

>[!success] We can mock a class or interface without implementing any code
>Mocks will return default values on function calls (*null for strings*) or a custom response.

>[!success] Verify if an interaction with the function is called or not
>It can be hard or impractical to verify if the function is actually executed.

>[!success] Isolate behaviour without relying on real implementations
>We can not to invoke production code during tests.
## Stubs

![[Stub Example.png|center|500]]

Unlike mocks, <b><span style='color: #87CEEB'>stubs</span></b> is <b><span style='color: #FFD700'>mainly about providing predefined data</span></b>. So it is mainly used when our code requires information to execute. So it is a more <b><span style='color: #FFD700'>lightweight version of a mock</span></b>.

>[!important] We use assertions on our own code that we want to test

>[!success] Helpful when real objects are unavailable or unsuitable

>[!success] Avoids side effects from using actual components

>[!success] Ensures consistent & controlled test scenarios
>Since it returns predefined data.

>[!fail] It is not a mock where it cannot record interactions

>[!fail] Cannot return mutiple values
# Types of Unit Tests
---
There are **3 types** of unit tests:
1) **Output** based
Here we are <b><span style='color: #FFD700'>interested in the output</span></b> (*correctness*) of the system under test, we are <b><span style='color: var(--mk-color-red)'>not interested in how it gets the output</span></b>.

They are **suitable** for pure functions that <b><span style='color: #FFD700'>do not modify global or internal state</span></b>.

>[!example] Example of output based testing
>We want to test the `add(int x, int y)` function. All we need to do is to `assertEquals(8, add(6, 2)`.

2) **State** based
Here we are <b><span style='color: #FFD700'>focusing on the state of the system after executing an operation</span></b>. Is useful when the function does not return a value but modifies the state.

State can refer to:
- Internal state of the **system under test**
- State of **collaborators** (*Other classes or services*)
- **External dependencies** like the database or the file system

>[!example] Example of state based testing
>We a delivery is completed the state for `isOutForDelivery` should be false and not true.

3) **Communication** based
Here we are <b><span style='color: #FFD700'>focusing on the integrations between collaborators</span></b> (*components*). Is useful when the unit under test interacts with other services especially when the result is not easily observable via return values.

We can verify a number of things:
- **Method calls**
- **Arguments used** in these calls
- **Call order** (*order in which functions are called*)

>[!warning] For this we require mocks or spies to capture interactions

>[!example] Example of communication based testing
>When a game is completed we need to check if the `cleanUp` function is called.



