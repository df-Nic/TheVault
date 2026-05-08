---
title: Code Quality
Date Created: 2024-09-01
Last Updated: 2025-09-28
tags:
  - CS2103
  - SWE
  - CodeQuality
---

## Code Analysis

There are <span style='color:var(--mk-color-orange)'>2 ways</span> to analyse code to ensure quality:
- **Static Analysis** - **Does not** require the code to be executed
- **Dynamic Analysis** - **Requires** the code to be executed

The goal of <span style='color:var(--mk-color-turquoise)'>static analysis</span> is to find unused bugs, unhandled exceptions, style errors etc. Basically <span style='color:var(--mk-color-yellow)'>anything to do with the code base</span>. Higher end tools can also check for bugs, memory leaks and inefficient code structures.

**Example:** Check style, PMD, FindBugs 

For <span style='color:var(--mk-color-turquoise)'>dynamic analysis</span>, it is more of <span style='color:var(--mk-color-yellow)'>analysing the performance</span> of the code and check for <span style='color:var(--mk-color-yellow)'>logic errors</span>.

**_Linters_ are a subset of static analyzers** that specifically aim to locate areas where the code can be made 'cleaner'.
## Code Reviews

It is a systematic **examination** of code with the intention of <span style='color:var(--mk-color-yellow)'>finding where the code can be improved</span>.

Some ways reviews can be done are through:
- **Pull request reviews** - Pull requests are public and other people can review it
- **Pair programming** - 2 People coding and reviewing each other
- **Formal inspections** - A team to inspect the project

> [!abstract] Advantages & Disadvantages of Code Review
> When compared with testing, the <span style='color:var(--mk-color-green)'>advantages</span> are:
> - It **can detect functionality defects** as well as other problems such as **coding standard violations**.
> - It can **verify non-code artifacts** and **incomplete code**.
> - It **does not require** test drivers or stubs.
> 
> The <span style='color:var(--mk-color-red)'>disadvantages</span> are:
> - It is a **manual process** and therefore, error prone.
## Testing

Here is an <span style='color:var(--mk-color-orange)'>outline of a testing cycle</span>:
1) Write test cases (*Description, inputs, expected output*)
2) Feed the inputs to the <span style='color:var(--mk-color-turquoise)'>SUT</span> (**Software under test**)
3) Observe and compare the actual output with the expected output

A <span style='color:var(--mk-color-red)'>test case failure</span> is a **mismatch between the expected and actual behavior**. A failure indicates a potential  defect (*or a bug or the test case itself*).

> [!tldr] Characteristics of Testing
> - **Dynamic**: Testing involves executing the software. It is not by examining the code statically.
> - **Finite**: In most non-trivial cases there are potentially infinite test scenarios but resource constraints dictate that we can test only a finite number of scenarios.
> - **Selected**: In most cases it is not possible to test all scenarios. That means we need to select what scenarios to test.
> - **Expected**: Testing requires some knowledge of how the software is expected to behave.
### Regression Testing

It is the act of **re-testing the software** to detect additional bugs after modification (*regressions*).

When a **bug is fixed**, <span style='color:var(--mk-color-red)'>unintended effects of the system may happen</span> and this is known as <span style='color:var(--mk-color-turquoise)'>regression</span>. Thus it is good to re-test the software will all of the test cases again.

This **can be done manually** but it can be <span style='color:var(--mk-color-green)'>more practical when automated</span>.
### Automated Testing

To **automate testing** is to programmatically run and compare results for a test case.

Advantages to automated testing is to <span style='color:var(--mk-color-green)'>improve efficiency and prevision of testing</span>, **minimising human errors** through manual means.

> [!example] Semi-automated testing using CLI
> The command line has a special function to re-direct input/output of a command line interface (*CLI*) applications to a text file using `<` and `>`.
> 
> First make 2 text files, one for input and one for the expected output.
> 
> Afterwards run the following command `java appName < input.txt > output.txt`. This basically means the app will take (`<`) data from input.txt and output (`>`) them into a file called output.txt.
> 
> Then to compare files run the following command `FC output.txt expected.txt`, and it will inform the tester if anything is mismatched.
## Test Case Design

Except for trivial SUTs, <span style='color:var(--mk-color-red)'>exhaustive testing is not practical</span>, we should only <span style='color:var(--mk-color-orange)'>focus on</span> testcases that are:
1) **Effective** - A test case than can find more bugs is preferred
2) **Efficient** - A small amount of test case that can find more bugs

This is to <span style='color:var(--mk-color-yellow)'>better make use of testing resources</span> as it can be <span style='color:var(--mk-color-red)'>costly</span> in real world.

A new test case should **target a potential fault** that is <span style='color:var(--mk-color-yellow)'>not covered by other test cases</span>.

> [!info] Positive & Negative Test Cases
> A <span style='color:var(--mk-color-green)'>positive</span> test is a test to **produce an expected behavior**.
> 
> A <span style='color:var(--mk-color-red)'>negative</span> test is a test to **produce an unexpected situation**.
> 
> Consider a function `lessThanOne(int i)`:
> - A positive test case will be `True == lessThanOne(0)`
> - A negative test will be `lessThanOne("ABCD")`

Some times, [[Models#Use Case Diagram|use cases]] can be used for both [[Developer Testing#System Testing|system]] and [[Developer Testing#Acceptance Testing|acceptance testing]]. The **main success scenario** can be a test case and **each variation can be another** test case. 

One issue is that use cases <span style='color:var(--mk-color-red)'>do not specify the exact data used</span>, thus the tester will chose which can result in **more test case**. To solve this <span style='color:var(--mk-color-yellow)'>high priority tests can be scripted</span> (*Predefined inputs*) while <span style='color:var(--mk-color-yellow)'>others can take a exploratory approach</span>.
### Types of Test Case Design

The type depends on <span style='color:var(--mk-color-yellow)'>how much SUT's internal details are considered</span> when designing test cases.

**Black-box** (*specification-based or responsibility-based approach*)
>Test cases are <span style='color:var(--mk-color-yellow)'>designed exclusively</span> based on the SUT’s specified external behavior.

**White-box** (*glass-box or structured or implementation-based approach*)
>Test cases are designed based on <span style='color:var(--mk-color-yellow)'>what is known about the SUT’s implementation</span>, i.e. the code.

**Gray-box approach**
>Test case design uses <span style='color:var(--mk-color-yellow)'>some important information</span> about the implementation (*Function*). For example, if a `sort` function uses 2 algorithms for different size inputs then we can do more meaningful tests.

## Equivalence Partitions

As mentioned previously it is **impractical to test all possible combinations**. Thus <span style='color:var(--mk-color-yellow)'>SUT's do not teach each unique input uniquely</span> (*the range is broken into smaller groups and this groups will be treated differently*).

Thus this is what <span style='color:var(--mk-color-turquoise)'>equivalence partitions </span>(*EP*) **also known as** <span style='color:var(--mk-color-turquoise)'>equivalence class</span>, uses the above observations to <span style='color:var(--mk-color-green)'>improve the E&E of testing</span>.

By <span style='color:var(--mk-color-orange)'>partitioning inputs</span> (*dividing*) we can:
- **Avoid testing too many inputs** - Evenly choosing from the partition <span style='color:var(--mk-color-green)'>increases efficiency</span> and <span style='color:var(--mk-color-green)'>reduces redundant tests</span>
- **Ensure all partitions are tested** - **Missing a partition** can <span style='color:var(--mk-color-red)'>result in bugs going unnoticed</span>, thus by partitioning inputs, we can <span style='color:var(--mk-color-green)'>find more bugs easily</span> and if we test all partitions we tested the entire range.

Sometimes the <span style='color:var(--mk-color-yellow)'>partitioning can be every possible value</span>, for example `showStatus(Enum x)`, then in this case every possible <span style='color:var(--mk-color-purple)'>enumerations</span> value has to be considered.

This is the same for <span style='color:var(--mk-color-purple)'>OOP methods</span> as well. We need to consider the <span style='color:var(--mk-color-yellow)'>different possible states the caller</span> can be in (`this`), the input parameters as well as <span style='color:var(--mk-color-yellow)'>other objects accessed</span> (*Global variables and other objects*).

> [!example] EP Example
> Consider this method in the `DataStack` class: `push(Object o): boolean`
> 
> - Adds `o` to the top of the stack if the stack is not full.
> - Returns `true` if the push operation was a success.
> - Throws
>     - `MutabilityException` if the global flag `FREEZE==true`.
>     - `InvalidValueException` if `o` is null.
> 
> EPs:
> 
> - `DataStack` object: [full] [not full]
> - `o`: [null] [not null]
> - `FREEZE`: [true][false]
### Boundary Value Analysis

It is a **test case design heuristic** that is based on the observation that **bugs often result** from <span style='color:var(--mk-color-red)'>incorrect handling of boundaries</span> of equivalence partitions. It is <b><mark style='background:var(--mk-color-yellow)'>not always the case where partitions have boundaries</mark></b>, thus this cannot be applied.

When **picking test inputs from an equivalence partition**, <span style='color:var(--mk-color-yellow)'>values near boundaries</span> (*i.e. boundary values or corner cases*) are **more likely to find bugs**.

Typically we will choose 3 values as such:
1) 1 from the boundary
2) 1 just below the boundary
3) 1 just above the boundary

**Example:** For strings choose, null string, string of maximum possible length and 1 + the maximum length
### Combining Test Inputs

As mentioned previously we will want to use inputs based on our **partitions and corner cases**. But **with multiple inputs** to a function it can be <span style='color:var(--mk-color-red)'>very expensive to test all combinations</span> but it is <span style='color:var(--mk-color-green)'>effective</span>.

Here are some strategies we can use (*It DOES NOT provide the same level of testing as testing everything*)
1) **At least once** strategy
It means to <span style='color:var(--mk-color-yellow)'>include each possible test input at least once</span>. This means we need to ensure that our all our test cases will have **at least one unique value for all inputs**.

If 1 variable has **exhausted all possible unique inputs** then for <span style='color:var(--mk-color-yellow)'>subsequent tests it can be of any value</span>.

2) **All pairs** strategy
This strategy came from the **observation** that **bugs rarely result** of <span style='color:var(--mk-color-yellow)'>more than 2 interacting factors</span>.

This involves <span style='color:var(--mk-color-yellow)'>taking all possible pairs of inputs</span> and between these inputs and their tested inputs we will <span style='color:var(--mk-color-yellow)'>get all combinations</span>. Then we will repeat for all pairs of inputs (*or focus on inputs that influence each other*).

> [!example] All Pairs Example
> Lets say $x_{1}$ has 3 values to test $x_{2}$ has 2 and $x_{3}$ has 2
> 
> - Look at pair $x_{1}$ and $x_{2}$ and get all combinations which is 6. Then for $x_{3}$ just pick any value for the test case
> - Same for $x_{2}$ and $x_{3}$ for 4
> - Same for $x_{1}$ and $x_{3}$ for 4 as well
> 
> With a total of 14 test cases.

3) **Random** strategy
This involves **using other strategies** and generating all the test cases. Afterwards <span style='color:var(--mk-color-yellow)'>take a random subset</span> of test cases.
### Heuristics for Combining Test Inputs

1) **Each valid input at least once in a positive test case**

This heuristic is mentioning that for all valid inputs $n$, we <span style='color:var(--mk-color-yellow)'>must have at least</span> $n$ test cases **for each of these valid inputs** and all of them must be a [[#Test Case Design|positive test case]]. This is to ensure that any bug for the unique input will be caught.

> [!example] Example of this Heuristic
> ![[Valid Input at Least Once in Positive Test Case Example.png|center|400]]
> 
> The underlined text are invalid inputs. This set of test case <span style='color:var(--mk-color-red)'>fails the heuristic</span> because of `Cherry` it **does not have its own positive test case**.

2) **Invalid inputs individually before combining them**

Lets look at the example above, for test case 4 <span style='color:var(--mk-color-yellow)'>there is 2 inputs that are invalid</span>, which <span style='color:var(--mk-color-red)'>does not follow this heuristic</span>. Thus we need to <span style='color:var(--mk-color-yellow)'>ensure that the invalid inputs are tested individually first </span>before combining them.

This is because if we combine them at the start, **how are we so sure that the error message is actually caused by one invalid input instead of the other**?

>Note that we can <b><mark style='background:var(--mk-color-yellow)'>mix</mark></b> **both the heuristics and the combination techniques** to get our test cases.
# Software Quality Assurance
---
QA, is the process of **ensuring that the software built** has the <span style='color:var(--mk-color-yellow)'>required levels of quality</span>.

While QA is mainly used, there are other techniques like, static analysis, code reviews and formal verification.

There is this equation, **Quality Assurance = Validation + Verification**. And <b><mark style='background:var(--mk-color-yellow)'>both must be done</mark></b>.

**Validation**
>Asking are the requirements <span style='color:var(--mk-color-yellow)'>correct</span>

**Verification**
>Are the requirements <span style='color:var(--mk-color-yellow)'>implemented correctly</span>
## Formal Verification

is just to **prove correctness** using <span style='color:var(--mk-color-yellow)'>mathematical techniques</span>. It can bs used to <span style='color:var(--mk-color-green)'>prove the absence of errors</span>. **Testing cannot prove their absence only presence**.

However, it only proves compliance <span style='color:var(--mk-color-red)'>not utility of the software</span> and it also <span style='color:var(--mk-color-red)'>requires great knowledge to apply</span>. Thus formal verification is **more commonly used in safety-critical software** like flight control systems.

# Readability
---
Apart from run time, security and robustness, **readability** (*understandability*) is also <span style='color:var(--mk-color-yellow)'>very important</span> since the code needs to be <span style='color:var(--mk-color-yellow)'>understood and modified by other developers</span> as well. 

Here are some ways to <span style='color:var(--mk-color-orange)'>improve readability</span>:
- Avoid **long methods** - Preferably keep methods with in <span style='color:var(--mk-color-yellow)'>30 lines of code</span>
- Avoid **deep nesting** - <span style='color:var(--mk-color-yellow)'>Any more than 3 levels of indentation</span> will make the reader lose track of the logic
- Avoid **complicated expressions** - <span style='color:var(--mk-color-yellow)'>Nested conditions are negations should be avoided</span> and they should be evaluated in steps
- Avoid **magic numbers** - Try and <span style='color:var(--mk-color-yellow)'>put all constants as named variables</span> to give them meaning
- Make code as explicit as possible - In <span style='color:var(--mk-color-purple)'>Java</span> use **explicit type conversion** or use **parentheses to show groupings**
## Structure Logical Code

The way you code should <span style='color:var(--mk-color-yellow)'>follow some sort of logical structure</span>. It should read just like a book, it should flow logically.

Thus structure your code in a way that lines that are meant to do a specific task to be <span style='color:var(--mk-color-yellow)'>grouped together</span> and separate them with a line break.


> [!fail] Don't do this
>```
>statement A1
>statement A2
>statement A3
>statement B1
>statement C1
>statement B2
>statement C2
>```
## Do Not Confuse the Reader

Try and <span style='color:var(--mk-color-red)'>not do the following things</span> which will confuse the reader:
- Unused parameters in the method signature
- Similar things that look different
- Different things that look similar
- Multiple statements in the same line
- Data flow anomalies such as, pre-assigning values to variables and modifying it without any use of the pre-assigned value
## KISSing

<span style='color:var(--mk-color-turquoise)'>KISS</span> is a abbreviation of, **keep it simple stupid**.

Try and keep your code <span style='color:var(--mk-color-yellow)'>as simple of an implementation as possible</span>. Discarding a brute force method for something more complicated can <span style='color:var(--mk-color-red)'>impact readability</span>.

Not only that but the potential <span style='color:var(--mk-color-red)'>bugs will be harder to debug</span>, with a more complicated code.

A more optimise solution can be used if the **additional cost can be justified**.
## Avoid Premature Optimizations

A popular saying goes as such, **make it work, make it right and make it fast**. This tells us that the most important thing is the <span style='color:var(--mk-color-yellow)'>correctness of our code</span>, then only we can optimise it.

If we <span style='color:var(--mk-color-orange)'>optimise too early</span>:
- We can be <span style='color:var(--mk-color-red)'>unsure</span> of which parts caused the performance bottlenecks
- It can <span style='color:var(--mk-color-red)'>complicate code</span> when trying to optimise **affecting correctness and readability**
- Hand-optimised code can be <span style='color:var(--mk-color-red)'>harder for the complier to optimise</span>. The simpler the code the easier the compiler can optimize.

Of course this **does not mean do not optimise**, <b><mark style='background:var(--mk-color-yellow)'>only optimise when it is necessary or required</mark></b>.

## SLAP

<span style='color:var(--mk-color-turquoise)'>SLAP</span> means, **single level of abstraction principle**.

**Avoid multiple levels of abstraction** and try and <span style='color:var(--mk-color-yellow)'>condense the logic into many small functions</span>.

It is **possible to have 2 levels of abstraction**, however this must be <span style='color:var(--mk-color-yellow)'>marked by comments and separated</span> using line spaces.

> [!example] Example of SLAP
> A <span style='color:var(--mk-color-red)'>bad</span> example:
> `readData();`
> `salary = basic * rise + 1000;`
> `tax = (taxable ? salary * 0.07 : 0);`
> `displayResult();`
> 
> A <span style='color:var(--mk-color-green)'>good</span> example:
> `readData();`
> `processData();`
> `displayResult();`

Try and make sure that a function is <span style='color:var(--mk-color-yellow)'>either low level</span> (*Code logic*) or <span style='color:var(--mk-color-yellow)'>high level</span> (*Function calls only*).
## Make the Happy Path Prominent

The <span style='color:var(--mk-color-turquoise)'>happy path</span> is the part of the **code** where it will <span style='color:var(--mk-color-yellow)'>execute if the input is correct</span>.

Thus we should <span style='color:var(--mk-color-yellow)'>first check for irregularities in our functionality</span> (*Guard clauses*) before executing the main part of the code. 

**Example:**
```java
if (isUnusualCase) { // Guard Clause
    handleUnusualCase();
    return;
}

if (isErrorCase) { // Guard Clause
    handleError();
    return;
}

start(); // Main part of the code
process();
cleanup();
exit();
```
# Error-Prone Practices
---
It is <span style='color:var(--mk-color-green)'>safer to use language constructs</span> in the way they are meant to be used, even if the **language allows shortcuts**. Such coding practices are <span style='color:var(--mk-color-red)'>common sources of bugs</span>.
## Use the Default Branch

In the `case` statements there is a branch called `default`, which handles all <span style='color:var(--mk-color-yellow)'>possible outcomes that are not considered</span>. The `default` branch even the `else` branch should <b><mark style='background:var(--mk-color-yellow)'>not be for the last option but rather all options that are not considered</mark></b>.

**Example:**
```Java
if (red) print "red";
else if (blue) print "blue";
else error("incorrect input");
```
## Do not Recycle Variable Names

**Use one variable for one purpose.** <span style='color:var(--mk-color-red)'>Do not reuse a variable</span> for a different purpose other than its intended one, just because the data type is the same.

**Do not _reuse_ formal parameters as local variables** inside the method.

**A Bad Example:**
```Java
double computeRectangleArea(double length, double width) {
    length = length * width;  // parameter reused as a variable
    return length;
}
```
## Avoid Empty Catch Blocks

For `try-catch` statements try and <span style='color:var(--mk-color-yellow)'>avoid having empty</span> `catch` blocks.

This is because an error has occurred and we should <span style='color:var(--mk-color-yellow)'>try and address the issue</span> or display something to the user.

It can be **left blank if it is unavoidable** but provide a comment as an explanation.
## Delete Dead Code

**Leaving unused code** just <span style='color:var(--mk-color-red)'>makes it more unreadable</span>. So just get rid of it. And if you need it back just use the version control tool.
## Minimise Scope of Variables

<span style='color:var(--mk-color-turquoise)'>Global variables</span> are good in a sense that they can be passed around into functions easily. They however <span style='color:var(--mk-color-red)'>create implicit links</span> between code segments and <span style='color:var(--mk-color-yellow)'>should be avoided</span> (*Minimise the usage of it*).

Also try and <span style='color:var(--mk-color-yellow)'>define variable in the least score as possible</span>. If the variable is only used in a `if` block, then it should be initialised in the `if` block.
## Minimise Code Duplication

<span style='color:var(--mk-color-turquoise)'>Code duplication</span>, especially when you <span style='color:var(--mk-color-yellow)'>copy-paste-modify code</span>, often <span style='color:var(--mk-color-red)'>indicates a poor quality implementation</span>. While it may not be possible to have zero duplication, always **think twice before duplicating code**; most often there is a better alternative.

This follows the DRY principle, **Don't Repeat Yourself**.
# Comments
---
When writing good code, it will be **self-explanatory** and thus comments are not needed. But for some cases to <span style='color:var(--mk-color-yellow)'>address the "WHY" in our code, a comment is needed</span>.

When commenting <span style='color:var(--mk-color-red)'>do not comment information that is obvious</span> from the code, something like `x++` or `getName()`, should not be commented.

When writing comments try and write it as if you are <span style='color:var(--mk-color-yellow)'>writing to other people</span>. Try and target other programmers reading the code.

As mentioned, try and <b><mark style='background:var(--mk-color-yellow)'>explain the WHAT and WHY</mark></b> aspects and not the <b><mark style='background:var(--mk-color-red)'>HOW aspect</mark></b>.

**What** - Comment on what the code is supposed to do
**Why** - The rational behind the current implementation
**How** - We do not need to explain how it works as it should be self-explanatory

