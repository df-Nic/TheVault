---
Title: Test Metrics
Date Created: 29-March-2026
Last Updated: 30-March-2026
Tags:
  - CS4218
  - SWE/TestMetric
---
# The 5W1H Of Test Metrics
---
Almost <b><span style='color: #FFD700'>everyone will in some way use test metrics</span></b> (*testers, QA leads, developers, project managers, stakeholders*)

They are <b><span style='color: #FFD700'>quantitative measures used to assess</span></b> the quality, progress, and effectiveness of <b><span style='color: #FFD700'>testing activities</span></b> (*essentially data points which tells us something about the code*). It tells us:
- The **quality of software**
- The **progress** & whether we **meet expectation**
- And in general **improve the entire software development process**

They are not only used <b><span style='color: #FFD700'>throughout the software development lifecycle but also after deploying</span></b>, across <b><span style='color: #FFD700'>all environments</span></b>, including testing and production.

>[!question] Why are metrics important?
>Metrics answers a few fundamental questions:
>- How much **progress** have we done in our testing
>- Where are the areas to improve in
>-  What are the bottlenecks
>- Can we improve test efficiency
>- Can we deploy in time with the quality our user deserve
>
>So all this <b><span style='color: #98FB98'>supports decision making</span></b>, <b><span style='color: #98FB98'>ensure product quality</span></b>.

To get these metrics, we typically **use tools & techniques** that track data like test coverage, defect density (*how many bugs are there per module/code lines*), test case pass / fail rate, mean time to detect/fix bugs, etc.
# Types of Metrics
---
There are **2 types** of test metrics:
1) **White** box metrics (*gather from code & implementation specific*)
2) **Black** box metrics (*gather from tools and test engineers*)
## White Box Metrics
### Code Review Metrics

Also known as <b><span style='color: #87CEEB'>code level metrics</span></b>. Though code review is <b><span style='color: #FFD700'>mainly qualitative</span></b>, we can use metrics to <b><span style='color: #FFD700'>track progress & identify trends</span></b>.

**A typical code review workflow**:
![[Code Review Workflow Example.png|center]]
#### Defect Density

Also known as <b><span style='color: #87CEEB'>defect rate</span></b>. It tells us the <b><span style='color: #FFD700'>average occurrence of bugs per lines of code</span></b> (*LOC*). It can also be for defects per thousand LOC (*KLoC*).

$$
\text{Defect rate} = \frac{\text{Total number of defects}}{\text{Total LOC}}
$$

And if we want **KLOC** we just times 1000.

Here are some **aspects which affects defect density**:
- **Complexity**, more <b><span style='color: var(--mk-color-red)'>complex code increases the chance of defects</span></b> & <b><span style='color: var(--mk-color-red)'>hard to understand modules have a higher defect rate</span></b>
- **Skill level**, <b><span style='color: var(--mk-color-red)'>less experience developers may introduced more bugs</span></b> than those with strong coding & test skills
- **Defect type**, some types of <b><span style='color: var(--mk-color-red)'>defects are harder to detect</span></b> (*UI may be caught early and deeper bugs increase density over time*)

>[!success] Gives a high level view of the code quality

>[!success] Validate testing quality
>Helps assess how effective the testing process is at catching defects.

>[!success] Save testing resources
><b><span style='color: #FFD700'>Identifies high-defect areas early</span></b>, allowing focused testing and resource optimization.

>[!success] Compare developer efficiency
>Tracks defect trends <b><span style='color: #FFD700'>across modules or developers</span></b> to evaluate code quality and productivity

>[!fail] Treats all defects equally
> Minor bugs and major bugs are treated as the same.
> >[!example] For example, security issues are more serious that other bugs
> >So having 1 security bug, meaning low density does not mean that the system is very secure.

>[!fail] It is not a silver bullet for code review metrics
#### Lines of Code

It tells us the count of executable lines of code (*ignoring comments & spaces*). It <b><span style='color: #FFD700'>gives an estimate of the size of the code</span></b>.

>[!fail] It does not tell us the quality of our code
>Mainly using LOC to determine quality will <b><span style='color: var(--mk-color-red)'>lead to more quantity over quality and efficiency</span></b>.
#### Function Point Analysis

The <b><span style='color: #FFD700'>estimation of software size by measuring functionality</span></b> (*number of functions to do 1 task*). 

>[!success] Independent of programming language used or the development methodology

>[!success] Better way to compare complexity and size of different applications
#### Risk Density

This **address the issue of the original defect density** where all bugs are treated equally. Now bugs or <b><span style='color: #FFD700'>defects are rated by risk</span></b> (*typically high, medium low*).

So now we can **compute** things like:
- X risk per lines of code
- X risk per function point

>[!note] X is the risk category
>So X can be high so number of high risk bugs per function point for example.
>
>But typically this is based on the internal application development policies & standards

>[!success] It gives more insight into the quality and impact of the code being developed
#### Path Complexity

Or <b><span style='color: #87CEEB'>cyclomatic complexity</span></b>. It can help <b><span style='color: #FFD700'>establish risk and stability estimations</span></b> on an item of code, such as a class or method or even a complete system.

>[!success] Easy to calculate & apply making it useful

$$
\text{Cyclomatic complexity} = \text{Number of decisions} + 1
$$
Where:
- A decision is considered as any point where the code can branch (*if-else, while, switch case, catch within the function*)

>[!idea] As decision count increase so does the programs complexity
>So the more complex the code, the <b><span style='color: var(--mk-color-red)'>less stable, maintainable</span></b> the code is and it has a <b><span style='color: var(--mk-color-red)'>higher risk of defects</span></b>.

Typically a **threshold** is used to guide development:
- **0-10: stable code**, acceptable complexity
- **11-15: medium risk**, more complex
- **16-20: high risk code**, too many decisions for a unit of code
### Review Process Metrics

These are to <b><span style='color: #FFD700'>evaluate the efficiency & effectiveness of our code review process</span></b>.

>[!success] Get a comprehensive view on code quality

>[!success] Understand the efficiency & efficacy of the code review process 
#### Inspection Rate

it is the <b><span style='color: #FFD700'>rate of coverage a code reviewer can cover per unit of time</span></b>. This can give a <b><span style='color: #FFD700'>rough idea of the required duration to perform a code review</span></b>.

>[!important] Inspection rate should not be used as a measure of review quality
#### Defect Detection Rate

Measures the <b><span style='color: #FFD700'>defects found per unit time</span></b>. It can be used to <b><span style='color: #FFD700'>measure of performance of the code review team</span></b>.

>[!important] Defect detection rate should not be used as a measure of review quality

>[!note] Defect detection rate incases as inspection rate decreases
>Because testers slow down & will be less likely to miss defects.
#### Code Coverage

It is a **critical** metric, measured as a <b><span style='color: #FFD700'>percentage of lines of code or function points that have been reviewed for testing</span></b>.

>[!goal] Typically people aim for close to 100% coverage & for security code review it often aims higher

Typically there are **checks in place** where the <b><span style='color: #FFD700'>build will fail if the desired percentage is below</span></b>.
#### Defect Correction Rate

It is the <b><span style='color: #FFD700'>amount of time used to correct detected defects</span></b>.

>[!success] Can be used to optimise a project plan within the SDLC

Average values can be measured over time, <b><span style='color: #FFD700'>producing a measure of effort</span></b> which must be taken into account in the planning phase to fix bugs, future planning & resource allocation.
#### Reinspection Defect Rate

Rate at which upon <b><span style='color: #FFD700'>re-inspection of the code more defects exist, some defects still exist, or other defects manifest through</span></b> an attempt to address previously discovered defects.

>[!danger] High reinspection defect rate can indicate issues with quality of initial fixes, thoroughness of original review or complexity of code
## Black Box Metrics
### Products Metrics

It focuses on the <b><span style='color: #FFD700'>characteristics & quality of the software product itself</span></b> (*focus on the attributes of the final system like functionality, reliability, usability*).

Here is a <b><span style='color: #FFD700'>mix of white & black box</span></b>.

>[!success] Help assess user satisfaction and product performance

>[!example] Some examples of product metrics
>- Defect density (*defects per thousand LOC/KLoC*), this is a white box matric
>- Code coverage
>- Mean time between failures (MTBF)
>- Customer-reported issues

We can use **[[Year 3/Sem 2/CS4218 - Software Testing/Test Metrics.md#Defect Density|defect density]]** to measure the quality of the product and also mean time to failure.
#### Mean Time to Failure

Mean time to failure (*MTTF*), <b><span style='color: #FFD700'>measures average time the software runs before encountering a failure</span></b> (*software reliability over time*).

$$
MTTF = \frac{\text{Total time system ran}}{\text{Number of failures ocurred}}
$$

>[!goal] Have a high MTTF which indicates that the system is more stable
>Because higher MTTF, fewer failures meaning the system is more stable

>[!success] Accesses effectiveness of testing & fault tolerance
>Did we find and fix the bugs and how our system handles failures.

>[!note] This is very [[Year 3/Sem 2/CS4218 - Software Testing/Test Metrics.md#Defect Density|similar to defect density]] a white box metric which measures based on software size
### Process Metrics

It looks at the <b><span style='color: #FFD700'>efficiency & effectiveness of the software development & testing process</span></b> and project metrics.

>[!success] Help improve software development & testing workflows
> Basically seeing which metrics is below the defined threshold & see how to improve on it.

>[!success] Can identify process bottlenecks or weaknesses

>[!example] Some examples of process metrics 
>- Test case execution rate
>- Defect removal efficiency
>- Time taken for each development/testing phase
### Project Metrics

Measure the **management aspects** of a software project, essentially we are <b><span style='color: #FFD700'>tracking the progress, resources, & overall health of the software project</span></b> (*progress, resources, cost, and schedule*).

>[!success] Useful for project planning and control

>[!example] Some examples of project metrics
>- Actual vs. Estimated effort
>- Budget
>- Schedule adherence
>- Team productivity rate
# Test Metrics For Testing Effectiveness
---
Test metrics (*mix of white & black*) is a <b><span style='color: #FFD700'>quantitative measure used to assess the effectiveness, efficiency, & quality of the testing process</span></b>.

>[!success] Help monitor testing progress, improve quality, and guide decision-making
>Some questions it can help answer are:
>- How long will it take to test?
>- How much money will it take to test?
>- How bad are the bugs?
>- How many bugs found were fixed? Reopened? Closed? Deferred?
>- How many bugs did the test team did not find?
>- How much of the software was tested?
>- Will testing be done on time? Can the software be shipped on time?
>- How good were the tests? Are we using low-value test cases?
>- What is the cost of testing?
>- Was the test effort adequate? Could we have fit more testing in this release?

We can **categorise** these metrics into:
- **Base** metrics
- **Calculated** metrics
## Base Metrics

<b><span style='color: #FFD700'>Raw data collected directly during testing activities</span></b> which <b><span style='color: #FFD700'>serves as the foundation for calculated metrics</span></b>.

>[!example] Some examples of base metrics
>- Total number of test cases
>- Number of test cases passed / failed/ blocked (*blocked is test that did not run*)
>- Number of defects found / accepted / rejected / deferred
>- Number of critical defects
>- Number of planned test hours
>- Number of actual test hours
>- Number of bugs found after shipping
## Calculated Metrics

For the metrics to be effective, calculated metrics are <b><span style='color: #FFD700'>derived from base metrics</span></b>.

>[!success] Provides a deeper insight for analysis and decision making

The calculated metrics can be **categorized** under one of these **5 groups**:
1) Test **coverage** metrics
2) Test **effectiveness** metrics
3) Test **effort** metrics
4) Test **tracking & quality** metrics
5) Test **efficiency** metrices
### Test Coverage Metrics

>[!goal] They answer how much of testing have we covered?

Some of these metrics are:
$$
\text{Executed Test Coverage } (\%) = \frac{\text{Number of tests run}}{\text{Total number of tests to be run}} \times 100
$$
$$
\text{Requirements Coverage } (\%) = \frac{\text{Number of requirements covered}}{\text{Total number of requirements}} \times 100
$$
### Test Effectiveness Metrics

>[!goal] They answer how effective are our tests in catching bugs?
>Essentially how <b><span style='color: #98FB98'>good our testing is in catching bugs</span></b>.

Some of these metrics are:
$$
\text{Test effectiveness } (\%) = \frac{\text{Bugs found in tests}}{\text{Total number of bugs found (tests + after shipping)}} \times 100
$$
$$
\text{Defect Leakage } (\%) = \frac{\text{Number of defects reported by customers}}{\text{Total number of defects (test + after shipping)}} \times 100
$$
<b><span style='color: #87CEEB'>Defect leakage</span></b>, is just <b><span style='color: #FFD700'>defects that were missed during testing but found later by users</span></b>.
### Test Effort Metrics

>[!goal] They answer these questions how long did each test take? & how many bugs were found per test?
> This helps us <b><span style='color: #FFD700'>understand the intensity & focus of our testing</span></b>.

Some of these metrics are:
$$
\text{Number of tests run per time period} = \frac{\text{Number of tests run}}{\text{Total time}}
$$
$$
\text{Bug find rate} = \frac{\text{Total number of defects}}{\text{Total number of test hours}}
$$
$$
\text{Number of bugs per test} = \frac{\text{Total number of defects}}{\text{Total number of tests}}
$$
$$
\text{Average time to test a bug fix} = \frac{\text{Total itme between defect fix to retest for all defects}}{\text{Total number of defects}}
$$
### Test Tracking & Quality Metrics

>[!goal] They answer are the defects caught during testing fixed?
> This helps us <b><span style='color: #FFD700'>track progress and assess the overall quality of our releases</span></b>.

Some of these metrics are:
$$
\text{Passed test case percentage} = \frac{\text{Number of passed tests}}{\text{Total number of tests executed}} \times 100
$$
$$
\text{Failed test case percentage} = \frac{\text{Number of failed tests}}{\text{Total number of tests executed}} \times 100
$$
$$
\text{Critical defects percentage} = \frac{\text{Number critical defects}}{\text{Total defects reported}} \times 100
$$
$$
\text{Fixed defects percentage} = \frac{\text{Number defects fixed}}{\text{Total defects reported}} \times 100
$$
### Test Efficiency Metrics

>[!goal] They answer how fast can we fix our bugs?

Some of these metrics are:
$$
\text{Average time to repair defects} = \frac{\text{Total time taken for bug fixes}}{\text{Total number of bugs}} \times 100
$$
#### Defect Gap Analysis

Sometimes we want to know <b><span style='color: #FFD700'>how efficient are we in fixing bugs found</span></b>. This is where the <b><span style='color: #87CEEB'>defect gap analysis</span></b> comes in.

**Visual/Tool for defect gap analysis**:
![[Defect Gap Analysis Graph.png|center|600]]

Essentially the solid line are the bugs reported and the dotted & dashed line is the bugs fixed. The <b><span style='color: #FFD700'>gap is then our bugs that are not fixed at any given point of time</span></b>.

We can **compute the defect gap** as such:
$$
\text{Defect gap } (\%) = \frac{\text{Total number of defects fixed}}{\text{Total number of valid defects reproted}} \times 100
$$
Where:
- These defects are typically **valid defects**

>[!question] What are invalid defects
>These are <b><span style='color: #FFD700'>bugs which are reported by customers but they are not bugs</span></b> due to the design choices made.
>
>Or they can <b><span style='color: #FFD700'>duplicate bugs</span></b>.

>[!important] Defect gap percentage is different from defect gap
>$$
> \text{Defect gap} = \text{Total defects} - \text{Fixed defects}
>$$

>[!success] This helps team organise and prioritise what they should do
>Because now they got a better understanding of the current state of defect resolution (*bug fix*).
# Customer Problem Metric
---
Typically as developers we might have a different perspective but **what truly matters is customer experience**.

So <b><span style='color: #FFD700'>from a user’s perspective, all encountered problems reflect issues</span></b> in the software (*both valid and invalid defects*)

 These can include:
- Usability challenges
- Poor or unclear documentation
- Duplicates of existing defects

Typically this is expressed in terms of <b><span style='color: #87CEEB'>problems per user month</span></b> (*PUM*) which can be **calculated** as:
$$
PUM = \frac{\text{Total number of problems customer reported (valid or invalid)}}{\text{Total number of license months of the software}}
$$
Where:
- The denominator just means the total time in months the users has been using the application 

>[!info] Some ways to achieve low PUM
>- Improve development process to reduce defects
>- Reduce non-defect-oriented problems (*better user guide*)
>- Increase the sales
## Customer Satisfaction Metrics

These are <b><span style='color: #FFD700'>often accessed through customer surveys</span></b> and uses scales like the <b><span style='color: #87CEEB'>5 point Likert scale</span></b>.

>[!success] It allows us to quantify subjective feedback into measurable data

Some of these metrics are:
$$
\text{\% of completetly satisfied customers} = \frac{\text{Total numer of "very satisfied" responses}}{\text{Total number of responses}} \times 100
$$
$$
\text{\% of satisfied customers} = \frac{\text{Total numer of "very satisfied" \& "satisfied" responses"}}{\text{Total number of responses}} \times 100
$$
$$
\text{\% of dissatisfied customers} = \frac{\text{Total numer of "very dissatisfied" \& "dissatisfied" responses}}{\text{Total number of responses}} \times 100
$$
$$
\text{\% of very dissatisfied customers} = \frac{\text{Total numer of "very dissatisfied"}}{\text{Total number of responses}} \times 100
$$
>[!note] These depends on the number scale you are using

And neutral (*3rd point*) which is in the middle will not be considered.

We can also compute the <b><span style='color: #87CEEB'>net satisfaction index</span></b> (*NSI*) which <b><span style='color: #FFD700'>aggregates the customer ratings into a single score</span></b>.

So if we have a 7 point scale then the one that is the most positive will have a score of 7 while the least positive rating will have a score of 1.

So if you **know the ratings from the individual scale** then:
$$
NSI = \frac{\sum^{N} \text{Count of Customer who rated category n} \times \text{Raiting score for category n}}{\text{Total response} \times \text{Number of scales}}
$$
What if we **do not have the customer rating total from the individual scales**, then:
$$
NSI = \text{\% of satisfied customers} - \text{\% of disatisfied customers}
$$
# Test Metrics For Tester Efficiency
---
## Productivity Metrics

These metrics <b><span style='color: #87CEEB'>productivity metrics</span></b> show us the <b><span style='color: #FFD700'>efficiency of our efforts in uncovering issues</span></b>.
### Defects Per 100 Hours Of Testing

This metric <b><span style='color: #FFD700'>normalizes</span></b> the number of defects found in the product with respect to the effort spent.

$$
\text{Defects per 100 hours of testing} = \frac{\text{Total defects found for a period of time}}{\text{Total hours spent to get defects}} \times 100
$$

>[!goal] Helps us understand the rate at which our testing effort is uncovering defects.
### Test Cases Per 100 Hours Of Testing

$$
\text{Test cases executed per 100 hours of testing} = \frac{\text{Total test case executed for a period of time}}{\text{Total hours spent to get execute the test cases}} \times 100
$$
>[!goal] Helps us understand the throughput of our testing, how efficiently our testers are moving through their test suits
# Visualising Test Metrics
---
**Charts** are <b><span style='color: #FFD700'>essential for illustrating test metrics</span></b> in software testing, <b><span style='color: #FFD700'>transforming complex data into clear, visual representations</span></b>.

>[!important] We are not just showing numbers but actionable intelligence
>So we follow the <b><span style='color: #87CEEB'>3 core principle of charting</span></b>:
>1) Identify right and meaningful metrics to visualize (*show the key performance indicators that directly impact decision making or track critical goals*)
>2) Choose chart types appropriately (*the wrong chart can hide the truth in  the data*)
>3) Lastly review each chart and determine what insights can be gained

The choice of chart matters. As the chart type <b><span style='color: #FFD700'>depends on what you want to communicate</span></b>.

>[!success] Enables faster understanding

>[!success] More effective communication

>[!success] Better decision making for all stakeholders

For **comparisons across categories** (*pass/fail rates, severity counts*), <b><span style='color: #FFD700'>bar or column charts</span></b> are ideal because they make differences clear and easy to interpret.

To **show trends over time** (*defect rates, test execution progress*), <b><span style='color: #FFD700'>line charts or area charts</span></b> are recommended for visualizing changes and patterns.

To **display compositions** (*parts of a whole or a distribution*), <b><span style='color: #FFD700'>pie chart, donut, stack bar</span></b> charts useful

To **illustrating distributions** (*such as test duration or response times*), <b><span style='color: #FFD700'>histograms or box plots</span></b> help reveal how values are spread and where outliers exist.

For **showing relationships** (*like test execution time vs. number of test cases*), choose <b><span style='color: #FFD700'>scatter plots or bubble charts</span></b> to reveal correlations between variables.
## Sanky Chart

For <b><span style='color: #FFD700'>visualizing complex flow and relationships in the process</span></b> you can us the <b><span style='color: #87CEEB'>Sanky chart</span></b>.

>[!goal] Show relationship and flow specifically to how bugs originating from different features

![[Sanky Chart Example.png|center|500]]

Sankey Chart <b><span style='color: #FFD700'>show how a value moves from one set of categories to another</span></b>, and the width of the flow represents the volume.
## Heat Map Chart

It use color intensity to <b><span style='color: #FFD700'>convey the magnitude of a metric across two categorical or quantitative </b></span> axis.

>[!goal] Heat maps translate large multidimensional data tables into actionable visual intelligence

![[Heatmap Example.png|center|600]]

>[!success] Quickly spot high issues areas (*the darker clolour intensity*)
## Other Charts

To get **more actional insights**, we will need to **go beyond our traditional graphs**.
- Mind maps
![[Mind Map Example.png|center|400]]

To <b><span style='color: #FFD700'>visualise hierarchical  relationships</span></b>.

- Graphics
- Box plot
![[Box Plot Example.png|center|400]]

You can <b><span style='color: #FFD700'>compare the spread, median & outliers</span></b> in metrics.

>[!success] Good for A/B testing

- Bugs doughnut chart
![[Bugs Doughnut Chart Example.png|center|300]]

- Radar chart

![[Radar Chart Example.png|center|400]]

It is used to <b><span style='color: #FFD700'>compare performance across multiple attributes</span></b>.