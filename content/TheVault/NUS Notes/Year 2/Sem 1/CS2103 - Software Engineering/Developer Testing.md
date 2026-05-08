---
title: Developer Testing
Date Created: 2024-08-24
Last Updated: 2025-09-28
tags:
  - CS2103
  - SWE/Testing/DeveloperTesting
---
# Why Developer Testing
---
Firstly <span style='color:var(--mk-color-turquoise)'>developer testing</span> is **testing done by the developers** as supposed to other parties.

<span style='color:var(--mk-color-orange)'>Testing is necessary especially early</span> on is because:
1) It is <span style='color:var(--mk-color-green)'>easier to find</span> the cause of the issue at the start rather at the end (*Large code base*)
2) **1 bug** can result in <span style='color:var(--mk-color-red)'>major rework</span> if left at the end
3) A bug can <span style='color:var(--mk-color-red)'>hide other bugs</span>
4) <span style='color:var(--mk-color-red)'>Can cause delays in delivery</span> if there is too many bugs

> [!question] What are the Pros & Cons for developers to Test
> <span style='color:var(--mk-color-green)'>Pros</span>
> - Can be done early
> - Can be done at lover levels (*Class levels / backend*)
> - More tesing can be done as developers know the expected behavior
> - Take respeonsibility for their work
> 
> <span style='color:var(--mk-color-red)'>Cons</span>
> - Subconsciously only test situations that he knows to work
> - Did not consider certain cases
> - Misunderstand what SUT is supposed to do
> - Lack testing experience
# Types of Testing
---
## Unit Testing

The idea of unit testing is to <span style='color:var(--mk-color-yellow)'>test individual components in the code</span>, more specifically individual functions.

To automate test cases, a <span style='color:var(--mk-color-turquoise)'>test driver</span> (*In java it will be a class*) will be created with many test cases whose purpose is to <span style='color:var(--mk-color-yellow)'>run the SUT with sample inputs</span> and check if the actual output matches the expected output.

For java the tool to carry out automated testing is <span style='color:var(--mk-color-purple)'>JUnit</span>.

**Sample code for JUnit**
```Java
import org.junit.jupiter.api.Test; 
import static org.junit.jupiter.api.Assertions.assertEquals; 
import static org.junit.jupiter.api.Assertions.fail;

public class TestClass {
	@Test
	public void testTotalSalary() {
		Payroll p = new Payroll();
	
		// test case 1
		p.setEmployees(new String[]{"E001", "E002"});
		assertEquals(6400, p.totalSalary());

		// test case 2
		p.setEmployees(new String[]{"E001"});
		assertEquals(2300, p.totalSalary());
	}
}
```

The test cases written should be <span style='color:var(--mk-color-yellow)'>inputs that can potentially trigger buggy behaviour</span> in the code. Another way write test cases is to <span style='color:var(--mk-color-yellow)'>future proof it</span>, by catching bugs caused from future developments.
### Stubs

In <span style='color:var(--mk-color-orange)'>unit testing</span> it is important that the <b><mark style='background:var(--mk-color-yellow)'>unit to be tested is isolated</mark></b>. For example if a class depends on another class, then it can <span style='color:var(--mk-color-red)'>influence the test since bugs can arise from that class</span>.

A workaround is using <span style='color:var(--mk-color-turquoise)'>stubs</span>, Which is just **recreating a class component with simple implementation** of the code that it will not likely have bugs.

These <span style='color:var(--mk-color-turquoise)'>stubs</span> only know how to respond to a predefined set of inputs and nothing else (*Basically set your own inputs*).

This is also known as <span style='color:var(--mk-color-turquoise)'>dependency injection</span>, which is a process of injecting objects (*Usually stubs*) to <span style='color:var(--mk-color-yellow)'>replace current dependencies with a different object</span>, to isolate testing from its dependencies.

To initialise a stub we can use **polymorphism**, here is an example of a stub:
```Java
class SalaryManagerStub extends SalaryManager {
    /** Returns hard coded values used for testing */
    double getSalaryForEmployee(String empID) {
        if (empID.equals("E001")) {
            return 1000.0;
        } else if (empID.equals("E002")) {
            return 1500.0;
        } else {
            throw new Error("unknown id");
        }
    }
}
```

### Addition JUnit Features

- **Annotations:** In addition to the `@Test` annotation you've seen already, there are many other annotations in JUnit which can be found [here](https://junit.org/junit5/docs/current/user-guide/#writing-tests-annotations).
  
- **Pre/post-test tasks:**  It is possible to supply code that should be run before/after every test method/class by using test instance lifecycle annotations such as `@BeforeEach` `@AfterAll`.
  
- **Conditional test execution:** It is possible to configure tests to run only under [certain conditions](https://junit.org/junit5/docs/current/user-guide/#writing-tests-conditional-execution).
  
- **Assumptions:** It is possible to specify assumptions that must hold for a test to be executed (i.e., the test will be skipped if the assumption does not hold)
  
- **Tagging tests:** It is possible to tag tests (e.g., `@Tag("slow")` so that tests can be selected based on tags. 
  
- **Test execution order:**  It is possible to specify a specific testing order. But the default order is to ensure standardisation of future tests.
  
- **Test hierarchies**: Normally, we organize tests into separate test classes. If a more hierarchical structure is needed, the `@Nested` [annotation](https://junit.org/junit5/docs/current/user-guide/#writing-tests-nested) can be used to express the relationship among groups of tests.

- **Repeated tests:** JUnit provides the ability to repeat a test a specified number of times by annotating a method with `@RepeatedTest` and specifying the total number of repetitions desired.
  
- **Parameterized tests** make it possible to run a test multiple times with different arguments. The parameter values can be supplied using a variety of ways.
  
- **Dynamic tests**: The `@TestFactory` annotation can be used to specify factory methods that generate tests dynamically.
  
- **Timeouts:** The `@Timeout` annotation allows one to declare that a test should fail if its execution time exceeds a given duration.
  
- **Parallel execution:** By default, JUnit tests are run sequentially in a single thread. Running tests in parallel — for example, to speed up execution — is available as an opt-in feature.
    
- **Extensions:** JUnit supports third-party extensions. The built-in `TempDirectory` extension is used to create and clean up a temporary directory for an individual test or all tests in a test class.
## Integration Testing

The idea of <span style='color:var(--mk-color-turquoise)'>integration testing</span> is to <span style='color:var(--mk-color-yellow)'>test weather different parts can work together</span> as expected.

Unlike unit testing, we <span style='color:var(--mk-color-red)'>do not use stubs</span> when testing with other classes.

Sometimes developers use hybrid testing, which is the combination of **unit and integration** to <span style='color:var(--mk-color-green)'>minimize the need for stubs</span>.

> [!info] Carrying out Integration Testing
> Lets say you have 3 classes, `Car`, `Engine`, `Wheel`.
> 1) Unit test `Engine` and  `Wheel`
> 2) Unit test `Car` (*If doing hybrid this will be included in the next step*)
> 3) Integration test `Car` with `Engine` and `Wheel` to ensure it works as intended
## System Testing

Take the **whole system** and <span style='color:var(--mk-color-yellow)'>test it against the specifications</span> of it. These test are based on **specified external behavior** of the system.

Sometimes, these tests <span style='color:var(--mk-color-yellow)'>go beyond the bounds</span> defined in the specification To ensure there is some <span style='color:var(--mk-color-green)'>leeway when pushed beyond limits</span>.

> [!note] Examples of System Testing
> Below are some <span style='color:var(--mk-color-orange)'>non-function requirements</span> than can be tested:
> - **Performancing Testing** - Respons quickly
> - **Load testing** - Can work under heavy load
> - **Security testing** - Test security
> - **Compatibility testing** - Can work with other systems
> - **Interoperability testing** - Can work with other systems
> - **Usability testing** - Ease of use
> - **Portability testing** - Can work on different platforms
## GUI Testing

**Testing of GUI** is <span style='color:var(--mk-color-red)'>harder</span> than testing other parts of the system.
- Hard to automate
- Its behaviour can be unexpected at times
- Might be different across platforms
- Order of operations GUI performs can vary

One way to make this easier is to <span style='color:var(--mk-color-yellow)'>move as much of the logic out of the GUI</span>, so that we can use automated API testing to test the logic, <span style='color:var(--mk-color-green)'>reducing the test cases</span>.

Some **tools** that can <span style='color:var(--mk-color-orange)'>automate GUI testing</span>:
- TestFX
- Visual Studio Code
- Selenium
## Acceptance Testing

Also known as <span style='color:var(--mk-color-turquoise)'>user acceptance testing</span> (*UAT*), is a test that ensures it meets user requirements. It give an assurance to the customer that the **product is working as intended**.

<span style='color:var(--mk-color-turquoise)'>Acceptance testing</span> comes <span style='color:var(--mk-color-yellow)'>after system testing</span>

**Difference between system and acceptance testing**
![[System vs Acceptance Testing.png|center]]

**Positive tests**
>Tests where the SUT is <span style='color:var(--mk-color-green)'>expected to work normally</span>

**Negative tests**
> Tests where the SUT is <span style='color:var(--mk-color-red)'>not expected to work normally</span>

**Requirement vs system specification**
![[Requirement vs System Specification.png|center]]

Usually the requirements are **both combined into 1 documents**. And if the <span style='color:var(--mk-color-green)'>system test pass</span> it <span style='color:var(--mk-color-red)'>does not mean it passes acceptance testing</span>.

For instance, it might be in line with the specification but it might not work as interned outside of the test environment or it simply does not meet the user demands.
## Alpha-Beta Testing

<span style='color:var(--mk-color-turquoise)'>Alpha testing</span> is **performed by the users**, under <span style='color:var(--mk-color-yellow)'>controlled conditions</span> set by the software development team.

<span style='color:var(--mk-color-turquoise)'>Beta testing</span> is **performed by a selected subset** of target users of the system in their <span style='color:var(--mk-color-yellow)'>natural work setting</span>.

An <span style='color:var(--mk-color-turquoise)'>open beta release</span> is the <span style='color:var(--mk-color-yellow)'>release of not-yet-production-quality-but-almost-there software</span> to the general population. For example, Google’s Gmail was in 'beta' for many years before the label was finally removed.
## Exploratory & Scripted Testing

There are a few ways to <span style='color:var(--mk-color-orange)'>approach testing a software</span>.

**Scripted testing**
> Write test cases based on the <span style='color:var(--mk-color-yellow)'>expected behaviour</span> of the SUT

**Exploratory testing**
> **Devise test cases on the fly**, based on the <span style='color:var(--mk-color-yellow)'>results from past test cases</span>

In other words, exploratory testing is the **simultaneous, learning, test design and execution**. It is also known as reactive testing, error guessing technique, attack-based testing or bug hunting.

So which is better? Well there is no definitive answer but a <span style='color:var(--mk-color-green)'>mix is beneficial and more prefered</span>.

**Scripted testing** is <span style='color:var(--mk-color-green)'>more systematic</span>, and hence, likely to <span style='color:var(--mk-color-yellow)'>discover more bugs given sufficient time</span>, while **exploratory testing** would <span style='color:var(--mk-color-green)'>aid in quick error discovery</span>, especially if the tester has a lot of experience in testing similar systems.

However the **success of exploratory testing** depends on the <span style='color:var(--mk-color-red)'>tester’s prior experience and intuition</span>.
# Test Coverage
---
First we need to define, <span style='color:var(--mk-color-turquoise)'>testability</span>, which is an indication of how easy it is to test an SUT. It is <span style='color:var(--mk-color-green)'>good to have high testability</span> as it will be easier to **achieve better quality software**.

It mainly depends on the design and implementation of the system.

Now <span style='color:var(--mk-color-turquoise)'>test coverage</span> is a **metric used to measure** the extend to which <span style='color:var(--mk-color-yellow)'>testing exercise the code</span>.

> [!info] Coverage Citeria
> 1) **Function/method coverage** - How much functions are executed during testing
> 2) **Statement coverage** - How many LOC are executed during testing
> 3) **Decision/branch coverage** - How many decisions are executed (*Tests cover all possible decisions*)
> 4) **Condition coverage** - Based on the boolean sib-expressions, each evaluated to both true and false with different test cases
> 
> For 100% **branch or decision coverage**, two test cases are required:
> 
> - `(x > 2 && x < 44) == true` : [e.g. `x == 4`]
> - `(x > 2 && x < 44) == false` : [e.g. `x == 100`]
> 
> For 100% **condition coverage**, three test cases are required:
> 
> - `(x > 2) == true` , `(x < 44) == true` : [e.g. `x == 4`]
> - `(x < 44) == false` : [e.g. `x == 100`]
> - `(x > 2) == false` : [e.g. `x == 0`]
> 
> 5) **Path coverage** - All possible execution paths from start to finish
> 6) **Entry/exit coverage** - All places where the method is called and also consider what happens after a return or a exception.

**Measuring coverage** is often done using <span style='color:var(--mk-color-yellow)'>coverage analysis tools</span>. Most IDEs have inbuilt support for measuring test coverage, or at least have plugins that can measure test coverage.

Coverage analysis can be **useful** in <span style='color:var(--mk-color-green)'>improving the quality of testing</span> e.g., if a set of test cases does not achieve 100% branch coverage, more test cases can be added to cover missed branches.
# Test Driven Development
---
It advocates <span style='color:var(--mk-color-yellow)'>writing the tests before writing the SUT</span>, while evolving functionality and tests in small increments.

Essentially, <span style='color:var(--mk-color-yellow)'>come up with the test cases first for some small feature</span>, then build a SUT that will pass these test cases or improve on a existing SUT to meet these test cases.

Some <span style='color:var(--mk-color-orange)'>rules to follow</span> when carrying out TDD:
- You are not allowed to write any production code unless it is to make a failing unit test pass.
- You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.
- You are not allowed to write any more production code than is sufficient to pass the one failing unit test.

> [!question] How to Carry Out TDD
> **Here are the steps to carry out TDD**
> 1) Decide what behavior to implement.
> 2) Write/modify a test case to test that behavior.
> 3) Run the test cases and watch them fail.
> 4) Implement the behavior.
> 5) Run the test cases.
> 6) Keep modifying the code and rerunning test cases until they all pass.
> 7) Refactor code to improve quality.
> 8) Repeat the cycle for each small unit of behavior that needs to be implemented.
