---
Title: Testing AI Systems
Date Created: 19-April-2026
Last Updated: 03-May-2026
Tags:
  - CS4218
  - SWE/Testing/AI
---
# 5W1H Of Testing AI Systems
---
Here we will see how different software engineering **testing** methods can be adapted for modern <b><span style='color: #FFD700'>ML & DL libraries or systems</span></b>.

>[!danger] The main issue with AI systems is that they do not behave deterministically
>As compared to traditional deterministic software, which can be due to:
>- Shuffling of data for each iteration during training
>- Dropout layers adds randomness
>- Weight initialization differs

>[!goal] Demonstrate how creative application of SE principles can uncover bugs and validate AI systems effectively

So typically <b><span style='color: #FFD700'>anyone who deals with AI will be testing</span></b> them, it is a distributed responsibility  (*ML Ops engineers, data scientist, ML researchers, software engineers*). This is to <b><span style='color: #FFD700'>ensure that the AI system performs as expected</span></b> (*in terms of accuracy, robustness, fairness, reliability, data quality*).

>[!important] AI systems require multi-faceted holistic evaluation
>This means <b><span style='color: #FFD700'>evaluating from different angles</span></b> or prespectives.

Typically <b><span style='color: #FFD700'>testing is done throughout the ML pipeline</span></b> (*data preprocessing, training & post training*).

During **data preprocessing** you are testing if the data is:
- Clean
- Representative of the population
- Free from biases

During **training** we monitor for:
- Convergence
- Overfitting
- Track performance

Then **after training** we evaluate on:
- Evaluate on held-out test data
- Stress test edge cases
- Assess production readiness

All these **testing is done** depending on the AI but typically is done <b><span style='color: #FFD700'>anywhere</span></b>:
- For **small** scale it is done on local machines to iterate quickly
- For **medium** scale it happens on company's GPU servers with controlled environments & reproducibility
- For **large** scale, it happens on the cloud GPU infrastructure

>[!important] Each environment has different constraints, failure modes, and implications
>A bug in development might be bad in production.

Typically to **test** an Ai there are **3 things to consider**:
1) Select appropriate testing methods
2) Establish meaningful metrics
3) Employ specialized tools & infrastructure

>[!question] So why do we even want to test AI systems?
>1) **Reliability** to ensure AI <b><span style='color: #FFD700'>behaves consistently & predictably</span></b>
>2) **Fairness** to ensure <b><span style='color: #FFD700'>equitable treatment</span></b> for all users
>3) **Security** to ensure <b><span style='color: #FFD700'>robustness against adversarial inputs & manipulation</span></b>
>4) **Effectiveness** to ensure that the <b><span style='color: #FFD700'>system solves the problem it was designed for</span></b>
# Differential Testing
---
The idea is that we take <b><span style='color: #FFD700'>2 or more different implementations but they achieve the same outcome</span></b> & test them on the same input (*different solutions or different versions etc*).

>[!important] This means that we do not need a ground truth label or know how the function does its task

If the **outputs are different**, <b><span style='color: #FFD700'>at least one of the implementations has some discrepancies</span></b> in their behaviour.

>[!info] But when testing AI systems we do not need to check if the 2 outputs are identical, we need to ensure that they are similar enough to what we expect
>Typically there is some threshold which we set or we can use something like <b><span style='color: #87CEEB'>stratified bootstrap confidence intervals</span></b> (*SBCI*).
>
>>[!tldr] Stratified bootstrap confidence intervals
>>Essentially we will first ask the model to do some tasks. Then we will <b><span style='color: #FFD700'>sample with replacement within the strata</span></b> (*meaning if task a has 10 outputs & task b has 5 outputs we sample 10 from task a and 5 from task b*).
>>
>>Then we <b><span style='color: #FFD700'>compute some matrix</span></b> like accuracy & aggregate it. Then we <b><span style='color: #FFD700'>repeat the whole process a number of times</span></b>.
>>
>>In the end we can be 95% confident (*or any other confidence interval*) that our model's accuracy will be within some range.

>[!warning] If the inputs are the same it does not guarantee that both implementations are correct
>It might be that <b><span style='color: var(--mk-color-red)'>both have the same bug</span></b> or that this output is the same but for <b><span style='color: var(--mk-color-red)'>other outputs it might be different</span></b>.
>
>So if they have the same output, they can be said that they are <b><span style='color: #FFD700'>equivalent for that input/output</span></b>.

>[!fail] If there is no other version or implementation then differential testing cannot be done

>[!failure] It does not localize the issue
>It <b><span style='color: var(--mk-color-red)'>does not tell you where or why</span></b> there is a mismatch in the output.

>[!fail] It can be misleading
>Sometimes it can be:
>- Both the implementations have a bug
>- Your implementation is correct but the reference is wrong
>
>So it is <b><span style='color: #FFD700'>important to find a gold standard reference</span></b>.
# Metamorphic Testing
---
Here we are answering the <b><span style='color: #87CEEB'>test oracle problem</span></b>, which is <b><span style='color: #FFD700'>how do we know whether our function outputs are correct</span></b>?

>[!example] Example of a well-defined test oracle
>So given any sorting function, the output will be that for any given array the elements will be sorted.

So <b><span style='color: #87CEEB'>metamorphic testing</span></b> is a software testing technique where differences are revealed by <b><span style='color: #FFD700'>checking the relations among the inputs and outputs of the software under test</span></b>.

>[!success] We do not need to know exactly the correct output, but know whether a change in the input changes the output
>This **relationship between outputs & the change in the input** is called a <b><span style='color: #87CEEB'>metamorphic relationship</span></b>.
>>[!example] Example of a metamorphic relation
>>We do not know if the probability of default for any given person.
>>
>>But we should observe that if the person is employed vs not employed the probability should be greater.

There are **3 types of metamorphic relations**:
1) **Invariance**, which states that certain <b><span style='color: #FFD700'>transformations of the input does not change the output</span></b> ($O = O'$)
2) **Increasing**, which states that the <b><span style='color: #FFD700'>transformation should increase the output</span></b> ($O' \gt O$)
3) **Decreasing**, which states that the <b><span style='color: #FFD700'>transformation should decrease the output</span></b> ($O' \lt O$)

>[!failure] Defining good metamorphic relations can be difficult
>It needs good domain expertise & creativity to find more complex relations and find more bugs.

>[!fail] Not all bugs violate the relations
>Metamorphic testing will <b><span style='color: var(--mk-color-red)'>not be able to prove that there is an absence of bugs</span></b>.
# Mutation Testing
---
This type of testing is to asks if the <b><span style='color: #FFD700'>test cases are good enough to detect faults</span></b>? So we do this by intentionally <b><span style='color: #FFD700'>introduce faults & see if our test suits can detect it</span></b>.

>[!info] A thorough test means that they can catch most injected faults
>And it is <b><span style='color: var(--mk-color-red)'>inadequate if it miss most injected faults</span></b>.

So to **do mutation testing**:
1) First run your test on the original program
2) Augment your original program (*remove statements, replace operands, etc*) to create a <b><span style='color: #87CEEB'>mutant</span></b>
3) Run the test cases which <b><span style='color: #FFD700'>passed originally in step 1</span></b> with the mutated program
4) Check to see if any test cases fail

If we <b><span style='color: #FFD700'>inject 1 change</span></b> it is known as <b><span style='color: #87CEEB'>first order mutants</span></b>. Then in **general** and <b><span style='color: #87CEEB'>x order mutants</span></b> means that we made <b><span style='color: #FFD700'>x number of changes</span></b>.

If we have <b><span style='color: #FFD700'>at least 1 test case fails</span></b> after mutation it means that the <b><span style='color: #FFD700'>test kills the mutant</span></b> (*or our tests are thorough*).

$$
\text{Mutation Score } = \frac{\text{Number of Killed Mutants}}{\text{Total Mutants}}
$$
Where:
- If they as for the mutation score in % then just times 100

>[!warning] Having a 100% mutation score does not mean your tests are very good
>It can mean you are <b><span style='color: var(--mk-color-red)'>over-specification</span></b> (*testing too many irrelevant details*).
>
>The <b><span style='color: #FFD700'>target is between 70 to 90%</span></b>. But in general the <b><span style='color: #98FB98'>higher the score the more likely the tests are to capture real defects in the program</span></b>.

>[!success] Mutation testing can be used to assess the quality of your test suite

>[!example] Using mutation testing in AI
>It is more on the quality of the test set. We create some mutant models and test it on the test set. If the test set is of high quality the mutant models should perform poorly. If it is of low quality then the models should perform the same as properly trained models.
>

>[!failure] Some mutants are impossible to kill
>For example <b><span style='color: var(--mk-color-red)'>mutants in unreachable codes resulting in false positives</span></b>.

>[!fail] Mutants can be artificial creating unrealistic scenarios
> Mutation testing <b><span style='color: #FFD700'>works at a syntax level</span></b>. So it has no semantic understanding which might <b><span style='color: var(--mk-color-red)'>make mutants which will never occur in practice</span></b>.
> 
> So your test cases will not catch it making the score looks worse than it actually is.

>[!fail] Cannot catch all defects
>It can <b><span style='color: #FFD700'>only detect faults that mutations can represent</span></b>.
>
>So <b><span style='color: var(--mk-color-red)'>some bugs needs creative scenarios</span></b> which mutation operators do not generate.

>[!fail] Mutation can be computationally expensive
> We need significant computation depending on size of the test suites and also the size of the code base.
# Fuzz Testing
---
The previous 3 methods were more methodical where we compare outputs or test results. <b><span style='color: #87CEEB'>Fuzz testing</span></b> (*or fuzzing*) is the opposite it is more **brute force**, just <b><span style='color: #FFD700'>generate a large amount of test inputs & see what breaks</span></b> (*hangs, memory leak, crashes, etc*).

>[!fail] Difficult to find logic bugs with fuzzing
>A fuzzer <b><span style='color: #FFD700'>detects bugs when the program crashes</span></b>, so we will <b><span style='color: var(--mk-color-red)'>need an oracle which sometimes might not exist </span></b>

>[!fail] Bugs found tend to be of the same type
>Certain crashes are easier to trigger & we might <b><span style='color: var(--mk-color-red)'>miss some rare conditions</span></b>.

>[!fail] Processing crashes & logs can be time confusing
>This is the <b><span style='color: #87CEEB'>triage burden</span></b>. Someone has to go through, analyse, group them, determine severity & remove duplicates for all these logs. So it is <b><span style='color: var(--mk-color-red)'>very time consuming</span></b> & <b><span style='color: var(--mk-color-red)'>requires expertise</span></b>.
>
>In addition, <b><span style='color: var(--mk-color-red)'>not every crash represents a real bug</span></b>, some can be due to the environment or are non-reproducible.

We can **generate tests** through:
- Some pre-defined specification
- Random inputs
- Mutated valid inputs

>[!goal] Is with enough random inputs we might hit edge cases which developers did not consider

There are **2 types of fuzzing**:
1) **Coverage-guided**

Or **grey-box fuzzing**. It uses a **program instrumentation** will <b><span style='color: #FFD700'>keep track of paths taken by each input</span></b> & then the **fuzz engine** uses this information to <b><span style='color: #FFD700'>mutate the input to reach deeper portions</span></b> of the program (*unexplored paths*).

>[!success] More efficient as it finds bugs faster

2) **Black-box fuzzing**

It is even simpler, it <b><span style='color: #FFD700'>just generate inputs</span></b> without knowing the knowledge of the internal behavior or implementation.

>[!success] Simpler as there is no need for a program instrumentation

>[!failure] Less efficient
>We do not know if we are exploring interesting parts of the code or just hitting the same lines.

>[!example] An example of fuzzing tool is ClusterFuzz
>Which supports both types of fuzzing techniques.

