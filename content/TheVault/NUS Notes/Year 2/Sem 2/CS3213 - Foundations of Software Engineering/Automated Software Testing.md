---
title: Automated Software Testing
Date Created: 2025-04-07
Last Updated: 2025-09-28
tags:
  - CS3213
  - SWE/Testing/AutomatedTesting
---
# Static Analysis
---
They are <b><span style='color:var(--mk-color-yellow)'>tools that reason about code without executing it</span></b>. These various static analysis tools that exist <b><span style='color:var(--mk-color-green)'>typically aim to find style violations or potential bugs in programs</span></b>.

**Some examples are:**
- Type checkers ([[Static Analysis & Type Systems#Type Systems|type systems]])
- Linters & style checkers, check the formatting and practices in the code without a deeper analysis
- Data-flow analysis, it reason about the potential set of values at different points in the execution
- Control-flow analysis, it reasons about the potential orders of executions

For static analysis it is very <b><span style='color:var(--mk-color-red)'>difficult to achieve full</span></b> [[Static Analysis & Type Systems#Soundness|soundness]] & [[Static Analysis & Type Systems#Completeness|completeness]].

> [!failure] Issues with static analysis
> - Can be **slow** (*complex static analysis*)
> - Can result in **false positives** (*i.e., false alarms*)
> - Can result in **false negatives** (*i.e., missed bugs*)
> - **Warnings might not be sufficiently actionable** (*i.e., developers do not know how to address them*)
> - Can be **difficult to integrate into the developer’s workflow**
> - Might be **inapplicable for complex features** (*e.g., when they are not modeled by the tool*)

> [!success] Successful static analysis characteristics
> - Focus on developer happiness (*Google*)
> - Must be **understandable** (*for the users*)
> - Must be **actionable and easy to fix** (*guide user or automatically fix it*)
> - **Low false positive rates** (*less than 10%*)
> - The bugs should have **potential for significant impact on code quality**
> - **Integrate with developers workflow**
> - **Timely report**

We know <b><span style='color:var(--mk-color-red)'>static analysis can be slow</span></b> if we focus on the whole code base. So why not, <b><span style='color:var(--mk-color-yellow)'>just focus on code that was changed</span></b>, this is known as <b><span style='color:var(--mk-color-turquoise)'>diff time</span></b>.

So only issues for the changes code will be reported which can be integrated during code review with bots.

> [!important] Timeliness of reports is important
> Those who change the code are prepared to look and discuss changes. Instead of manually deciding who fix what.

> [!example] Example of static analysis tools
> For **Facebook** they use Infer, which initially ran the whole code but but subsequently changed to diff time.
> 
> For **Google** they use FindBugs which also ran over the entire codebase. The bug dashboard used was outside the developer's usual workflow. Which they change to **Tricorder** which deliver valuable results.
> > [!failure] Problems these big companies faced
> > <b><span style='color:var(--mk-color-red)'>Context switching is costly for developers</span></b>, the bugs might <b><span style='color:var(--mk-color-red)'>not be relevant</span></b> to their current work or project.
> >
> > In addition it can be <b><span style='color:var(--mk-color-red)'>difficult to assign the bugs to the right person</span></b> (*person might have left*).

Though **static analysis** can be <b><span style='color:var(--mk-color-green)'>useful</span></b>, it can be <b><span style='color:var(--mk-color-red)'>challenging to integrate it to bring value</span></b>.
# Automated Testing
---
When we manually write tests, the <b><span style='color:var(--mk-color-red)'>test might be incomprehensive</span></b> or we can <b><span style='color:var(--mk-color-red)'>miss tests</span></b>. So we want someone to **automatically generate tests inputs**.

Automated testing techniques are useful especially <b><span style='color:var(--mk-color-green)'>for complex systems and components to find bugs</span></b>.

Automated testing approaches have found many bugs in important software systems (*OSs, compilers, database systems*)

> [!failure] Drawback for automated testing
> For some of these techniques (*property based testing, metamorphic testing*) <b><span style='color:var(--mk-color-red)'>more creativity is required in realizing</span></b> them as compared to example based tests

> [!abstract] Grey-box testing
> It is the combination of [[Software Testing#Black-box Testing|black-box]] and [[Software Testing#White-box Testing|white-box]], where we <b><span style='color:var(--mk-color-yellow)'>use some internal information</span></b> (*e.g., coverage*).

There are <span style='color:var(--mk-color-orange)'>many appraoches</span> to automated testing:
- Property based Testing
- Differential Testing
- Metamorphic Testing
- Fuzzing
- Symbolic Execution
## Property-Based Testing

Here we specify properties for the component we can test and <b><span style='color:var(--mk-color-yellow)'>let the test framework try to find a counterexample</span></b> that causes the property to break (*i.e., falsify it*). Unlike [[Software Testing#Black-box Testing|specification based]] where **we select** the values from a partition.

This <b><span style='color:var(--mk-color-yellow)'>follows the black-box approach</span></b>.

Pioneered in <b><span style='color:var(--mk-color-blue)'>QuickCheck</span></b> for <b><span style='color:var(--mk-color-purple)'>Haskell</span></b> (*about 300 lines of code*).

> [!example] jqwik
> One of the many property-based testing frameworks for <b><span style='color:var(--mk-color-purple)'>java</span></b>.
> 
> 

For property based testing, we <b><span style='color:var(--mk-color-yellow)'>constraint the input domain</span></b>, the frameworks will <b><span style='color:var(--mk-color-yellow)'>provide ways to adapt existing generators or create new generators</span></b> (*input value generation*). We can also override this generator.

> [!info] The generator will not enumerate all values but do some sort of sampling

They also provide <b><span style='color:var(--mk-color-turquoise)'>shrinkers</span></b> which are <b><span style='color:var(--mk-color-yellow)'>test-input reduction tools</span></b>.

> [!example] Example using jqwik
> ```Java
> @Property
> void positiveAbs (@ForAll @IntRange (min = Integer. MIN_VALUE + 1, max = Integer. MAX_VALUE ) int val ) {
> 	assertTrue(Math. abs val ) >= 0 )
> }
> ```

For specification based testing the inputs are more simpler, but for <b><span style='color:var(--mk-color-yellow)'>more creative and complex inputs</span></b> we should **use property based testing**.

> [!success] Advantages of using property-based testing
> - Can **test complex systems** (*high leverage scenarios*)
> - **Tests provides greater confidence**
> - Used to **communicate the specification**
## Differential Testing

Software can have **alternative implementations, versions, or configurations** that exists whose <b><span style='color:var(--mk-color-yellow)'>output we can compare to check for discrepancies</span></b> (*functional or non-functional*).

This <b><span style='color:var(--mk-color-yellow)'>follows the black-box approach</span></b>.

Differential testing is also known as <b><span style='color:var(--mk-color-turquoise)'>A/B testing</span></b> or <b><span style='color:var(--mk-color-turquoise)'>N-version testing</span></b>.

> [!hint] The idea is to send a common input to multiple systems to see if the result is the same

When **one of the output differs**, then at **least one of the systems** might be <b><span style='color:var(--mk-color-red)'>affected by a bug</span></b>.

![[Differential Testing Visualisation.png|center|500]]


> [!success] Advantages of differential testing
> In general it is a <b><span style='color:var(--mk-color-green)'>simple</span></b> and <b><span style='color:var(--mk-color-green)'>effective</span></b> technique.

> [!failure] Challenges of differential testing 
> - **False alarms** from small overlaps in functionality and intended differences
> - **Overlook bugs** when multiple system produce the same incorrect result
> - **Non-deterministic output** (*concurrency*)
> - **Input generation can be challenging** (*undefined behavior free programs for C/C++ compilers*)
### What to Compare

#### Comparing Versions

There should be a <b><span style='color:var(--mk-color-yellow)'>known working version</span></b> this is known as the <b><span style='color:var(--mk-color-turquoise)'>golden version</span></b> (*form of regression testing*). Thus we check between the updated version and the golden version.

> [!failure] Sometimes the change in semantics might have been intended but will be flagged
#### Comparing Configurations

Here multiple software system provide <b><span style='color:var(--mk-color-yellow)'>different configurations</span></b> which can be compared.

> [!example] For instance compilers you can test between using `-O0` optimisation level against `-O3`

Here a <b><span style='color:var(--mk-color-yellow)'>known working configuration</span></b> is known as a <b><span style='color:var(--mk-color-turquoise)'>reference engine</span></b>.

For **complex systems this reference engine** might be some <b><span style='color:var(--mk-color-yellow)'>naive, unorganised or does not have the full functionality</span></b> of the system (*example google spanner database system*).
#### Comparing Implementations

For important software systems where there are <b><span style='color:var(--mk-color-yellow)'>multiple implementations</span></b> (*competition*).

If the <b><span style='color:var(--mk-color-yellow)'>2 implementations are sufficiently similar</span></b> they can be used for **differential testing**. So if 2 software's have common major functionalities you may compare with one another.

> [!example] Like different OSs, windows macOS, linux
## Metamorphic Testing

Sometimes for differential testing, there is no reference system or it is untestable where there is no clear single solution exists (*machine translation software*).

It uses a source test case (*and its result, which has some metamorphic relation*) to <b><span style='color:var(--mk-color-yellow)'>generate a follow up test case</span></b> for which the <b><span style='color:var(--mk-color-yellow)'>result can be inferred</span></b>.

![[Metamorphic Testing Visualisation.png|center]]

The 2 inputs and outputs are related in some way and it can be seen as a <b><span style='color:var(--mk-color-yellow)'>special case of property based testing</span></b>.

This <b><span style='color:var(--mk-color-yellow)'>follows the black-box approach</span></b>.

> [!example] Example using the sin function
> We know that $sin(\pi - x) = sin(x)$. Thus we can morph $x$ into $\pi - x$ which are related and we should expect the 2 outputs to be the same.
### Equivalence Modulo Inputs

It is one of the <b><span style='color:var(--mk-color-green)'>most successful metamorphic testing approaches</span></b> and has found hundreds of bugs in GCC and LLVM.

**Generating diverse equivalent programs** for compiler testing is <b><span style='color:var(--mk-color-red)'>challenging</span></b>.

The idea is rather than creating equivalent programs, <b><span style='color:var(--mk-color-yellow)'>create programs that are equivalent only for a given input</span></b>, which is <b><span style='color:var(--mk-color-green)'>easier</span></b>.

> [!question] How to generate equivalent programs?
> For a given program with an input $I$, where till be <b><span style='color:var(--mk-color-yellow)'>certain parts which will not be executed</span></b>.
> 
> We can just <b><span style='color:var(--mk-color-yellow)'>mutate the unexecuted part</span></b> and verifying the output is still the same.

By **mutating the unexecuted portions**, it might <b><span style='color:var(--mk-color-yellow)'>change how the compiler generates or optimise code</span></b>, which can reveal bugs.

> [!success] Advantages of metamorphic testing
> - It **requires only a single system**. It avoids some of the weaknesses in differential testing such as requiring multiple systems that produce the same result for a given input
> - **Simple and effective technique** (*assuming that metamorphic relation is simple*)

> [!failure] Disadvantages of metamorphic testing
> **Finding** a bug-revealing metamorphic relation can be <b><span style='color:var(--mk-color-red)'>difficult</span></b>.
## Fuzzing

The idea of <b><span style='color:var(--mk-color-turquoise)'>fuzzing</span></b> is to <b><span style='color:var(--mk-color-yellow)'>send a random input</span></b> to a program and hope it crashes.

> [!abstract] Fuzzing test oracles
> 1) **Crashes**: For instance <b><span style='color:var(--mk-color-purple)'>C/C++</span></b> programs might crash with <b><span style='color:var(--mk-color-red)'>segmentation fault</span></b>
> 2) **Hangs**: Requires a pre-set thresholds
> 3) **Dynamic analysis tools**: Instrument the program to detect issues (*race conditions*). For example, LLVM sanitisers Valgrind or Miri for Rust

### Black-Box Fuzzing

> [!success] Advantages of black-box fuzzing
> It is a <b><span style='color:var(--mk-color-green)'>simple & efficient</span></b> test-case generation 

> [!failure] Disadvantages of black-box fuzzing
> <b><span style='color:var(--mk-color-red)'>Unlikely to uncover deep bugs</span></b>, especially when the input format is complex.
> 
> Also there is <b><span style='color:var(--mk-color-red)'>no feedback</span></b> from the program.
> 
> <b><span style='color:var(--mk-color-yellow)'>Partly addressed by grammar based fuzzing</span></b>, which uses a description of the input language to generate test inputs.
#### Mutation-Based Fuzzing

Rather than passing random input to the program, <b><span style='color:var(--mk-color-yellow)'>mutate existing inputs</span></b> (*adding, removing, exchanging*).

> [!success] Advantages of mutation-based fuzzing
> <b><span style='color:var(--mk-color-green)'>Higher quality inputs</span></b> assuming a diverse input seed corpus.

> [!failure] Disadvantages of mutation-based fuzzing
> <b><span style='color:var(--mk-color-red)'>Requires seed inputs</span></b> to mutate.
### White-Box Fuzzing

Here it will <b><span style='color:var(--mk-color-yellow)'>leverage detailed knowledge of the program</span></b> for fuzzing. Applies program analysis, typically some form of symbolic execution.

> [!example] Example of a white-box fuzzer is SAGE
> It execute with a concrete input. As it execute it will gather path constraints.
> 
> With the information it will systematically negate and solve them with a constraint solver.

White box Fuzzing Techniques are often powered by <b><span style='color:var(--mk-color-turquoise)'>constraint solvers</span></b> and <b><span style='color:var(--mk-color-turquoise)'>symbolic execution</span></b>.

> [!success] Advantages of white-box fuzzing
> It can generate <b><span style='color:var(--mk-color-green)'>diverse</span></b> test inputs.

> [!failure] Disadvantages of white-box fuzzing
> <b><span style='color:var(--mk-color-red)'>Heavyweight and costly</span></b> in terms of run-time performance.
#### Constraint Solvers

We give a set of inputs and its <b><span style='color:var(--mk-color-yellow)'>restrictions</span></b> and see if the <b><span style='color:var(--mk-color-yellow)'>condition is satisfiable</span></b> (*unsatisfiable, UNSAT*) and **return a possible set of inputs**.

> [!example] An example of a solver is z3 for python

There are <span style='color:var(--mk-color-orange)'>2 types of solvers</span> (*which are both [[NP-Completeness|NP hard problems]]*):
1) SAT solvers
2) SMT solvers
##### Boolean Satisfiability (SAT Solvers)

[[NP-Completeness#CNF-SAT & 3-SAT|SAT]]solvers **takes in** a <b><span style='color:var(--mk-color-yellow)'>propositional formula as a input</span></b> (*Boolean expressions and variables*).

It will **output** weather the <b><span style='color:var(--mk-color-yellow)'>model satisfies the formula or not</span></b> (*model means solutuon*).
##### Satisfiability Modulo Theories (SMT Solvers)

<b><span style='color:var(--mk-color-red)'>Not all problems is a Boolean formula</span></b>. These solvers solve a formula by <b><span style='color:var(--mk-color-yellow)'>using theories</span></b> (*theory of linear integer arithmetic*).
#### Symbolic Execution

Instead of using concrete inputs we <b><span style='color:var(--mk-color-yellow)'>use a symbolic input</span></b>.

> [!info] A symbolic input can represent any concrete value

The idea is to <b><span style='color:var(--mk-color-yellow)'>keep track of the constraints</span></b> on the symbol values (*path constraints*) and use a theorem solver (*constraint solver*) to <b><span style='color:var(--mk-color-yellow)'>check if they are reachable</span></b>.

> [!success] We can use this to derive test cases for different paths from the constraint solver

> [!example] A widely used and widely known symbolic execution tool is KLEE

First **generate a execution tree**.

![[Execution Tree.png|center]]

For each path (*path condition*), we will **encode all the branch decision on the symbolic variables** (*can encoded as a test oracle*).

If the constraint solver cannot find a solution, then this <b><span style='color:var(--mk-color-red)'>path cannot be reached</span></b> which means:
- The <b><span style='color:var(--mk-color-yellow)'>code is redundant</span></b> because it cannot be reached
- This code will <b><span style='color:var(--mk-color-yellow)'>never be executed thus a bug is found</span></b>

> [!success] Advantages of symbolic execution
> It can <b><span style='color:var(--mk-color-green)'>systematically generate inputs</span></b>.

> [!failure] Disadvantages of symbolic execution
> - Path explosion problem, there can be **exponentially many paths**
> - **Modeling the environment** (*system or library calls*)
> - With **loops** there can be an **infinite execution trees**
> - **Heap modeling**, modeling as a bit array can be **expensive**
> - The **performance of the solvers** as well as the **complex path conditions**
### Grey-Box Fuzzing

For <b><span style='color:var(--mk-color-turquoise)'>grey-box fuzzing</span></b>, it <b><span style='color:var(--mk-color-yellow)'>balances the benefits</span></b> of black box fuzzing (*efficient test case generation*) and white box fuzzing (*high quality inputs*).

The idea is that, for **each mutated input**, check whether it <b><span style='color:var(--mk-color-yellow)'>resulted in a gain of code coverage</span></b> (*or code coverage pattern*). **If so, keep the input and mutate it further**.

> [!example] AFL, American Fuzzy Lop or AFL++ is a widely known grey-box fuzzer

![[AFL style Greybox Fuzzers Simplified Scheme.png|center]]

Here is <span style='color:var(--mk-color-orange)'>how it works</span>:
- Instrument a program to collect code coverage
- Given a seed corpus select an input for mutation
- Execute the instrumented program
- If new code is covered then the input is added to the seed corpus and subsequently further mutated
