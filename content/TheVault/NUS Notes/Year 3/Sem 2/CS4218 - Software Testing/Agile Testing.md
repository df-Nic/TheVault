---
Title: Agile Testing
Date Created: 20-April-2026
Last Updated: 21-April-2026
Tags:
  - CS4218
  - SWE/Testing/AgileTesting
---
# 5W1H Of Agile Testing
---
So typically for <b><span style='color: #87CEEB'>agile testing</span></b> <b><span style='color: #FFD700'>everyone on the team will be testers</span></b>. It <b><span style='color: #FFD700'>aligns testing practices with agile practices</span></b> (*collaboration, fast feedback & iterative deployment*).

Agile testing should be done <b><span style='color: #FFD700'>continuously and early throughout the whole development cycle on all environments</span></b> from planning to development.

>[!success] Frequent testing helps catch bugs early
>This then leads to <b><span style='color: #98FB98'>better customer satisfaction & supports rapid change</span></b>.

>[!question] So how do we do agile testing?
>Focus on small, testable increments with quick feedback loops for validation.

The foundation of agile is the [[Year 2/Sem 2/CS3213 - Foundations of Software Engineering/Software Engineering Processes.md#Agile Manifesto|"Manifesto of agile software development"]] and it establishes a set of **core values**:
- <b><span style='color: #FFD700'>Individuals and interactions</span></b> over processes and tools
- <b><span style='color: #FFD700'>Working software</span></b> over comprehensive documentation (*Does not mean no documentation*)
- <b><span style='color: #FFD700'>Customer collaboration</span></b> over contract negotiation
- <b><span style='color: #FFD700'>Responding to change</span></b> over following a plan
## Traditional Vs Agile Testing

When we talk about **traditional** we are talking about the **[[Year 2/Sem 2/CS3213 - Foundations of Software Engineering/Software Engineering Processes.md#Waterfall Model|waterfall approach]]** where things are done <b><span style='color: #FFD700'>sequentially</span></b>.

So typically <b><span style='color: #FFD700'>testing is done right after coding & right before release</span></b>.

>[!fail] This leads to a lack of time for testing
>Either the <b><span style='color: var(--mk-color-red)'>testing time gets reduced</span></b> or "squeezed". And some might take the time to do last-minute code & fix cycle before.

The **[[Year 2/Sem 2/CS3213 - Foundations of Software Engineering/Software Engineering Processes.md#Agile Software Engineering|agile]]** approach is <b><span style='color: #FFD700'>more iterative & incremental</span></b>. Here testing is not a separate phase but it is <b><span style='color: #FFD700'>done during each iteration</span></b>.

>[!success] This makes it possible to have a release after each cycle is completed

So we would want to have an agile mindset when testing, so here are some of the **principles for agile testers**:
1) Provide continuous feedback (*constant communication to build the right thing & test early*)
2) Deliver value to customer (*valuable and useful for the end-user, test on the important features*)
3) Enable face-to-face communication (*prioritise direct communication & it can solve issues faster*)
4) Have courage (*Voice out your concerns of issues to advocate what is best for the user*)
5) Keep it simple (*do the simplest testing approach to get the job done*)
6) Practice continuous improvement (*at each sprint retrospective ask how to be better*)
7) Respond to Change (*requirements change so our tests must adapt to it*)
8) Self-organize (*be proactive*)
9) Focus on People (*foster strong collaborative relationships with the team & the end users*)
10) Enjoy (*be curious, engaged & have a positive mindset*)
# Agile
---
## Agile Practices

|  Agile practice  |                                                                                                                  Meaning for the team                                                                                                                  |                                                                                                        Meaning for testing                                                                                                        |
| :--------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| Cross-functional | The team as a <b><span style='color: #FFD700'>whole should include all skills necessary</span></b>. Originally this was taken to imply that everyone could work with any task, but the need for specialized roles (*testers*) is now widely recognized | The <b><span style='color: #FFD700'>team must work together</span></b> on test strategy, test planning, test specification, test execution, test evaluation and test results reporting. The **tester might initiate** these tasks |
| Self-organising  |       The team <b><span style='color: #FFD700'>decides together who does what, when and how</span></b>. There is <b><span style='color: var(--mk-color-red)'>no external project manager</span></b> role that assigns tasks to the team members        |                               Ideally, the team should <b><span style='color: #FFD700'>include one</span></b> or more persons with a <b><span style='color: #FFD700'>testing background</span></b>                                |
|    Co-located    |                                                                                           The team, including the product owner, sit together in same space                                                                                            |                                                                             Testers, as part of the team, also sit together with the rest of the team                                                                             |
|  Collaborative   |                                               Team <b><span style='color: #FFD700'>members work together and with the business, customer or any stakeholder</span></b> to reach the goals of each sprint                                               |                                 <b><span style='color: #FFD700'>Testers collaborate continuously</span></b> with other team members, working together rather than alone on their dedicated tasks                                  |
|    Empowered     |                                                   The <b><span style='color: #FFD700'>team makes their own technical decisions</span></b>, together with the product owner and other teams if needed                                                   |                                 <b><span style='color: #FFD700'>Testing tasks and decisions are valued and done together as a whole team</span></b>, and not dictated by someone outside the team                                 |
|    Committed     |                                                                          The team commits to completing a selected number of backlog items with good quality within a sprint                                                                           |                                                         The tester (*and thus the whole team*) commits to test against the needs and expectations of users and customers                                                          |
|   Transparent    |                                                  All <b><span style='color: #FFD700'>progress is visible all of the time to any interested party</span></b>, by using an Agile task board for example                                                  |                                <b><span style='color: #FFD700'>Testing tasks are also visible</span></b> (*clear for everyone*) on the Agile task board or any other "information radiators" used                                 |
|     Credible     |                       The team must only <b><span style='color: #FFD700'>take on tasks that they have the credibility to accomplish</span></b> (*no overcommitting*). Otherwise, they risk micromanagement from all stakeholders                       |   The test strategy, its <b><span style='color: #FFD700'>implementation and its execution must be credible and communicated well</span></b>. Otherwise, stakeholders will not trust the test results and reported team progress   |
| Open to feedback |         Agile teams learn and evolve continuously by <b><span style='color: #FFD700'>learning from feedback and indeed asking continuously for feedback</span></b>. Retrospectives are natural events in Scrum that make it possible to learn          |                                          <b><span style='color: #FFD700'>Learning to be better in testing</span></b> must also be the mindset of all team members, especially the tester                                          |
|    Resilient     |                                                                        Agile projects must be able to <b><span style='color: #FFD700'>respond to change</span></b> at all times                                                                        |                                     Testing must also <b><span style='color: #FFD700'>adapt to changes and testing</span></b> must be defined so that changes are easily handled, not feared                                      |
## Sprint Zero

There is where the **Agile project actually begins**. It is a <b><span style='color: #FFD700'>preparatory sprint before the actual development begins</span></b>.

Typically during this sprint **the team** will:
- Lay out the foundation for the project before development begins
- Setting up the development environment, tools, and CI/CD pipelines
- Clarifying the product vision and high-level requirements
- Creating an initial product backlog with prioritized user stories

But **for the testers**:
- It helps <b><span style='color: #FFD700'>determine test emphasis</span></b> based on the project scope
- Creates an initial <b><span style='color: #FFD700'>test strategy & automation architecture</span></b>
- Perform quality <b><span style='color: #FFD700'>risk analysis</span></b>
- Specifying the <b><span style='color: #87CEEB'>"Definition of Done"</span></b> (*DoD*)

>[!tldr] Definition of Done
>It is to <b><span style='color: #FFD700'>specify what it means or something to be completed</span></b>.
>
>In a **testing view** it is the <b><span style='color: #FFD700'>level of testing required for a task to be completed</span></b>.

Here is a **summary of the tasks** in sprint 0 and what it means for the testers:

|                                 Task in sprint zero                                  |                                                                                                      Related testing                                                                                                       |                                                                                             Relevant testing perspective                                                                                              |
| :----------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|                          Identify the scope of the project                           |                                                                                         Identify test emphasis based on the scope                                                                                          |             Think about the whole product backlog to <b><span style='color: #FFD700'>understand the scope</span></b>. Bring testability into the discussion. Ask what would make sense to implement first             |
|           Create an initial system architecture and high-level prototypes            |                                                                                         Think about a test automation architecture                                                                                         |                       Talk about testability, and <b><span style='color: #FFD700'>make sure the architecture enables testability</span></b>; for example: easy access to test automation tools                        |
|                      Plan, acquire and install any needed tools                      |                                                                           Get tools for test management, defect management, and test automation                                                                            | Discuss the <b><span style='color: #FFD700'>integration of test cases</span></b> into task management and the integration of <b><span style='color: #FFD700'>test tools</span></b> into task management and reporting |
|                 Create an initial test strategy for all test levels                  | Based on the scope of the project, define what kind of testing is needed in the project and when. Consider (*among other topics*) test scope, technical risks, test types, test methods, test criteria and coverage goals. |                                 Discuss <b><span style='color: #FFD700'>what testing tasks will be part of other activities</span></b>; for example, tasks done with each coding task                                 |
|                       Perform an initial quality risk analysis                       |                                                                    Think of quality risks to bring up in the risk analysis session with the whole team                                                                     |                                           Determine the <b><span style='color: #FFD700'>risk for all backlog items</span></b>; for example, by using the risk poker method                                            |
|                                 Define test metrics                                  |                                                                            Measure the test process and the progress of testing in the project                                                                             |                                                                   Decide how to <b><span style='color: #FFD700'>measure product quality</span></b>                                                                    |
|                        Specify the definition of done (*DoD*)                        |                    Think of testing tasks you want to accomplish, and try to fit as many as you can into the team’s DoD. The remaining tasks might become the tester’s own tasks if there is still time                    |                                              <b><span style='color: #FFD700'>Decide what type of testing and to what extent</span></b> (*coverage*) must be part of DoD                                               |
|                                Create the task board                                 |                                                     In some cases, set up a separate testing task board; for example, for integration testing of several user stories                                                      |                                     Ensure <b><span style='color: #FFD700'>task boards include testing tasks and testing columns,</span></b> so that testing progress can be seen                                     |
| Define when to continue or stop testing before delivering the system to the customer |                                                                               Define test criteria that would help to decide when to release                                                                               |                                  <b><span style='color: #FFD700'>Determine such a set of release criteria</span></b> that utilizes test criteria and other information from testing                                   |
## Test Pairs

It is essentially **[[Year 2/Sem 2/CS3213 - Foundations of Software Engineering/Software Engineering Processes.md#Pair Programming|pair programming]]**.

There are **3 types of pairs**
1) **Developer-tester**, here the **developer** will <b><span style='color: #FFD700'>implement the code & tests while thinking aloud & get feedback</span></b> from the tester. The **tester** on the other hand will <b><span style='color: #FFD700'>analyse & discuss on the intention of the functionality</span></b> while also <b><span style='color: #FFD700'>write higher level test cases</span></b> & might help in <b><span style='color: #FFD700'>locating the defect</span></b>
2) **Tester-tester**, **one** of the testers will <b><span style='color: #FFD700'>do exploratory testing</span></b> (*navigating around the app to find bugs*) while the **other** will <b><span style='color: #FFD700'>observe & comment</span></b> on what to do next while also <b><span style='color: #FFD700'>logging what they are testing</span></b> (*these 2 can switch places at intervals*).
3) **Tester-product owner**, the **tester** will just <b><span style='color: #FFD700'>design and executes tests</span></b> while the **product owner** (*or any other business stakeholders*) brings in her business/domain knowledge, discusses with the tester what would be <b><span style='color: #FFD700'>beneficial to test to get more coverage and explains how users will expect different functions to work</span></b>.

>[!success] Promotes collaboration

>[!success] Improves test quality

>[!success] Ensures business value is delivered efficiency
# Agile Testing Quadrants
---
![[Agile Testing Quadrants.png|center]]

These quadrants help to <b><span style='color: #FFD700'>organise testing activities</span></b> along 2 axes:
- **Horizontal** axis is the <b><span style='color: #FFD700'>technology</span></b> facing tests (*left*) to <b><span style='color: #FFD700'>business</span></b> facing tests (*right*)
- **Vertical** axis is the tests that <b><span style='color: #FFD700'>guide development</span></b> (*bottom*) to the tests that <b><span style='color: #FFD700'>critique the product</span></b> (*top*)

To **summarise** the quadrants:
- Q1 is more of ensuring that the **functionality works as intended**
- Q2 is more on whether the **functionality meets what the user wants** (*software works from an end-user perspective*)
- Q3 is more on the **end to end** user experience
- Q4 is more on the **non-functional** requirements

<b><span style='color: #FFD700'>Different types of tests involve different stakeholders</span></b> like:
- Developers
- Testers
- Business analysts
- Customers (*not expected to write or run tests as they are still done by the developers*)

>[!info] The agile testing quadrants clarify responsibilities and testing focus areas

>[!question] Why do we seperate into quardrants?
>This separation helps <b><span style='color: #98FB98'>ensure that all aspects of quality are covered</span></b> (*functionality, performance, usability, etc.*).
>
>It also <b><span style='color: #98FB98'>encourages collaboration & shared understanding between technical & business roles</span></b>.
# Tools & Methods In Agile Testing
---
![[Overview of the Agile Process.png|center]]

So here you can see that in agile we do these activities in iteration so things are **fast paced** so having <b><span style='color: #FFD700'>structured methods & tools are important</span></b>.

>[!important] Tools & techniques must align with Agile's fast paced feedback cycles
>If it takes days to come up with tests then we won't be able to keep up with this fast pace. 
>
>So **methods** should <b><span style='color: #FFD700'>support rapid, continuous testing to match development speed</span></b>.
>
>**Tools and techniques** must help the team <b><span style='color: #FFD700'>meet project goals efficiently</span></b>.

This is not just the tools & methods but <b><span style='color: #FFD700'>selecting the right one is important also</span></b> as it makes the team more:
- <b><span style='color: #98FB98'>Agile</span></b>
- <b><span style='color: #98FB98'>Responsive</span></b>
- <b><span style='color: #98FB98'>Collaborative</span></b>
- <b><span style='color: #98FB98'>Responsive to changes</span></b>
## Agile Testing Practices

Here we will introduce some of the **test-first methodologies** and they are:
- Test driven development (*TDD*)
- Acceptance test driven development (*ATDD*)
- Behavior driven development (*BDD*)

Then we can **seamlessly** make this practices automated in our **daily workflow** through <b><span style='color: #FFD700'>continuous integration</span></b> (*CI*). 

>[!tldr] Continuous integration
> Where developers <b><span style='color: #FFD700'>upload changes into a central repository triggering a automated build and test</span></b>.

>[!success] Advantages of integrating these methodologies into CI
>- <b><span style='color: #98FB98'>Immediate feedback</span></b>, within minutes you will know if you broken anything
>- <b><span style='color: #98FB98'>Reduces cost, effort & time to fix bugs</span></b>
>- It creates a **quality gate** where the build succeeds if new code is integrated correctly & passes all test cases <b><span style='color: #98FB98'>preventing regressions</span></b>
>- Gives <b><span style='color: #98FB98'>confidence to move forward & deploy to customers</span></b>
>- Combines high level tests with low level tests (*ATDD/BDD & TDD/Unit tests*)

>[!failure] Downsides of integrating these methodologies into CI
>- <b><span style='color: var(--mk-color-red)'>Builds may become slow because all the tests runs every time</span></b>. So if you have a slow test suit the build will be slow (*try running a subset*)
>- Another issue is <b><span style='color: var(--mk-color-red)'>flakey test</span></b> (*test that sometimes fail or pass when there is no change*), this creates false positives
>- A **green build** does not mean your <b><span style='color: var(--mk-color-red)'>tests are of quality and have high coverage</span></b>
>- <b><span style='color: var(--mk-color-red)'>Increased test maintenance</span></b> as the project grows
### Test Driven Development

![[Test Driven Development Flow.png|center]]

Here is a **iterative flow** of a typical <b><span style='color: #87CEEB'>test driven development</span></b> (*TDD*). But essentially we will <b><span style='color: #FFD700'>write the test cases first before writing any code</span></b>.

Then we develop the <b><span style='color: #FFD700'>code in small increments just enough to pass the test</span></b> (*minimal amount of code*).

>[!question] Why do we refactor?
>This is just to keep <b><span style='color: #98FB98'>code clean, maintainable & understandable</span></b>.
>
>>[!important] After refactoring run all the tests again to ensure no functionality had been broken
>
>Some might do an upfront <b><span style='color: #FFD700'>architectural design to reduce refactoring</span></b>.

>[!success] Detect errors early and ensures code meets design expectations
>TDD catches bugs early in the development cycle, making them <b><span style='color: #98FB98'>easier and cheaper to fix</span></b>.

>[!success] Build a comprehensive safety net of tests driving a clean & robust software from the ground up

>[!success] Provides long-term confidence in code changes and refactoring
>This increases a developers confidence.

>[!success] Improved design
>Writing tests first forces you to <b><span style='color: #FFD700'>think about the function's interface and behavior</span></b> before implementation, leading to better design (*more user friendly, well-structured*)

>[!success] Creates living documentation
>Tests serve as living documentation of the code, clearly demonstrating how the code is supposed to be used (*clarity*). This is potentially better that static & out of date documentation.
### Acceptance Test Driven Development

ATDD takes a step back from the code & <b><span style='color: #FFD700'>focuses on the requirements</span></b> which is essentially <b><span style='color: #FFD700'>creating the acceptance tests before development begins</span></b> (*or in an agile case it will be iteratively*). Then we can incorporate TDD to pass the acceptance tests.

So now each <b><span style='color: #FFD700'>user story will include an acceptance criteria</span></b> (*involves a meeting with everyone like a workshop*) which can be used to draft acceptance tests.

>[!success] Bring developers, testers, & business stakeholders together to collaboratively define what the system should do from a user's perspective
>So there is this shared understanding on how the system should behave from the users perspective.

So what is the **difference between TDD & ATDD**:

|    Aspect    |                                                 TDD                                                  |                                                     ATDD                                                     |
| :----------: | :--------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------: |
|    Focus     |  Developer's perspective, focuses on <b><span style='color: #FFD700'>how the code works</span></b>   | Business / user perspective, focuses on what <b><span style='color: #FFD700'>the system should</span></b> do |
|  Test Type   |                                              Unit tests                                              |                              Acceptance tests (*high level behaviour focuses*)                               |
| Participants |                    Primary <b><span style='color: #FFD700'>developers</span></b>                     |    <b><span style='color: #FFD700'>Developers, testers & business stakeholders</span></b> collaboratively    |
|   Purpose    | Ensure correct code implementation at the <b><span style='color: #FFD700'>technical</span></b> level |      Ensure correct feature behaviour at the <b><span style='color: #FFD700'>business</span></b> level       |
| When written |                                         Before writing code                                          |                        Before implementation or as part of requirement clarification                         |
| Granularity  |                          Fine-grained, test individual functions or methods                          |                     Coarse-grained, tests system or feature behaviour from the user POV                      |
|   Outcome    |                              Clean, working code that passes unit tests                              |                              A system that behaves as expected by the customer                               |
In summary **TDD** helps us to <b><span style='color: #FFD700'>build the code right</span></b>, while **ATDD** helps us <b><span style='color: #FFD700'>build the right code</span></b>.
### Behavior Driven Development

![[BDD Life Cycle.png|center|350]]

BDD is an evolution of both TDD & ATDD which <b><span style='color: #FFD700'>emphasizes on communication</span></b> (*using common human readable language*) often in the <b><span style='color: #87CEEB'>"Given-When-Then" format</span></b> to <b><span style='color: #FFD700'>describe system behavior for all users to understand</span></b> (*unlike ATDD which uses an acceptance criteria*).

>[!abstract] Given-When-Then
>It is part of the **Gherkin syntax**, so:
>- **Given**: Is some initial context
>- **When**: An event occurs
>- **Then**: Verify the expected outcome
>
>The format should <b><span style='color: #FFD700'>include realistic data</span></b> that can be used for <b><span style='color: #FFD700'>test execution</span></b>.
>>[!example] Example for the Given-When-Then format
>>- **Given**: Given that the system is the main page or login page
>>- **When**: When the user IDs (John) & passwords (FunnyPassword!) are inputted to the user ID & password fields
>>- **Then**: The system will give the message "Login accepted" & move tot eh landing page
>>
>>This is a positive example you can also give negative examples as well like giving an incorrect password.

BDD also <b><span style='color: #FFD700'>promotes immediate test automation</span></b> more than ATDD.

Similar to ATDD these specifications are defined through a workshop (*or other means*), then these <b><span style='color: #FFD700'>behaviors are turned into executable tests</span></b> based on expected outcomes (*and they are run continuously*). 

>[!success] Ensures that everyone has a shard understanding on what needs to be built before writing code
>This works well for non-technical team members as we are <b><span style='color: #FFD700'>focusing on the system behaviors</span></b>.
>

>[!success] Ensures technical implementation is verifiably linked to the business level behaviour

>[!example] Examples of tools which support BDD methodology are Cucumber, JBehave & Robot Framework (adapted)

So essentially this differs from ATDD is that we are writing everything in plain text & then we can use these <b><span style='color: #FFD700'>tools which can understand human-readable language to translate to tests</span></b>.
# Test Debt
---
<b><span style='color: #87CEEB'>Test debt</span></b> is essentially the cost from <b><span style='color: #FFD700'>choosing an easy or incomplete testing solution now</span></b> instead of a better approach which can take longer (*skipping tests, writing bad tests just to meet deadlines*).

So each skipped test, untested edge case, poorly written test case id a debt which will be paid back later in the form of emergency bug fixes after a release.
## Test Debt In Manual Testing

1)  <b><span style='color: #FFD700'>Limited test execution</span></b>

We are <b><span style='color: #FFD700'>constrained by time & human resources</span></b> and thus is often impossible to run the entire test suite of manual tests. 

>[!fail] Resort to running a subset of tests which increases the risk of residual defects

>[!info] We are betting that untested areas are still working correctly

2) <b><span style='color: #FFD700'>Improper Test Deisgn</span></b>

Manual testing is <b><span style='color: var(--mk-color-red)'>time-consuming & repetitive</span></b>. This makes testers often <b><span style='color: #FFD700'>skip complex data combinations</span></b> and focus on happy paths. 

>[!fail] Leads to incomplete coverage & potential defects in the SUT

3) <b><span style='color: #FFD700'>Missing test reviews</span></b>

Test cases <b><span style='color: #98FB98'>benefit from peer review to ensure that they are of high quality</span></b>, but <b><span style='color: var(--mk-color-red)'>this step is often skipped</span></b>.

>[!fail] Increased cost of test maintenance
>As we need to redo the test cases or add more tests because we missed some cases.
## Test Debt In Automated Testing

>[!warning] Even though automated testing is very powerful it not done correctly it can also lead to test debt.

Typically this happens when we do not treat test code with the same care as our production code.

1)  <b><span style='color: #FFD700'>Inadequate infrastructure</span></b>

The environment used is critical, we <b><span style='color: #FFD700'>cannot use an environment that is different from the customers setup</span></b>. As passing a test will not guarantee success in production.

>[!fail] This leads to a reduce confidence in system's reliability
>This defeats the purpose of having a safety net.

2)  <b><span style='color: #FFD700'>Lack of coding standards</span></b>

Tests are still code, <b><span style='color: var(--mk-color-red)'>not having a consistent coding practices can make it hard to maintain</span></b>.

>[!fail] This increases the long-term maintenance cost
>Testers will need to spend more time to understand the test before updating it.

3)  <b><span style='color: #FFD700'>Unfixed or broken tests</span></b>

This is when we <b><span style='color: #FFD700'>ignore failing or broken tests</span></b> (*maybe cause the function was changed or removed*). This <b><span style='color: var(--mk-color-red)'>leads to false negatives & lowers trust</span></b>.

>[!fail] Reduces the overall test quality
>Because they will <b><span style='color: var(--mk-color-red)'>ignore the CI/CD pipeline</span></b> and the signal just becomes noise.
>
>So if a bug is actually introduced no one will notice or fix it.

>[!question] So how do we reduce test debt in automated testing
>It all lies with a <b><span style='color: #98FB98'>disciplined, ongoing commitment from the entire team</span></b>, so here are some key strategies:
>- <b><span style='color: #98FB98'>Treat test code like production code</span></b> (*coding standards, peer-reviewed, refactor & maintained*)
>- <b><span style='color: #98FB98'>Prioritize automation efforts</span></b>, do not automate everything, use the **[[Year 3/Sem 2/CS4218 - Software Testing/System Testing.md#System Testing|test pyramid]]** strategy
>- Adopt a <b><span style='color: #98FB98'>zero tolerance policy</span></b> for broken tests, stop and fix the code if the CI/CD pipeline fails & remove tests if not relevant
>- Make <b><span style='color: #98FB98'>quality a team responsibility</span></b>, the whole team (*testers, developers, product owners*) is responsible & with this shared ownership it prevents dept from accumulating
### Test Pyramid

We are used to the **2D test pyramid**:
![[2D Test Pyramid.png|center|400]]

Which tells us that we should focus on more unit & functional test and that the <b><span style='color: #FFD700'>quantity should decrease as we go up the pyramid</span></b> for automated tests.

>[!success] Guides towards a balanced and maintainable test strategy

>[!success] Encourages faster feedback loops and cost-effective testing
>Because we know where we should put our effort in when testing.

There is also a **3D test pyramid**:
![[3D Test Pyramid.png|center|400]]

On the **right** you can see the <b><span style='color: #FFD700'>type of testing to be done at different levels</span></b> (*the scope*). And on the **left** they are the <b><span style='color: #FFD700'>non-functional qualities to test</span></b> for known as <b><span style='color: #87CEEB'>ilities</span></b>.

>[!question] Why do we need a 3D test pyramid
>This is because testing is more than just functional automation

At the **peak there are your manual and exploratory testing** (*ET*), which shows that <b><span style='color: #FFD700'>human creativity & domain knowledge is irreplaceable with test automation</span></b> (*as automation cannot find all bugs*).

>[!success] Powerful strategic tool

>[!success] Encourages to build a strong, automated foundation

>[!success] Consider full spectrum of testing needed to deliver a high-quality product
### Simple Rules For Automated Testing

|                             Rule                             |                                                                                                                                        Reason                                                                                                                                        |
| :----------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|                        Single purpose                        |                                                                                             <b><span style='color: #98FB98'>Easier to debug & change</span></b> if business rules change                                                                                             |
|                DRY (*Don't Repeat Yourself*)                 |                                                                                    Ability to change tests in only one place for <b><span style='color: #98FB98'>easy maintainability</span></b>                                                                                     |
|            Use a DSL (*domain-specific language*)            |                                                                                                <b><span style='color: #98FB98'>Makes communication about the tests easier</span></b>                                                                                                 |
|                Abstract code out of the tests                |                                                                                                     Makes the tests business <b><span style='color: #98FB98'>readable</span></b>                                                                                                     |
|                   Setup and teardown tests                   |                                                                                                       Can run the tests <b><span style='color: #98FB98'>repeatedly</span></b>                                                                                                        |
|                         Independence                         |                                                                                Tests can run independently and <b><span style='color: #98FB98'>do not depend on order</span></b> to run consistently                                                                                 |
|            Avoid database access (*if possible*)             |                                                                  <b><span style='color: var(--mk-color-red)'>Database calls slow down the tests</span></b> (*note that somewhere you may need to test the access*)                                                                   |
|              Tests must run green—all the time               |                                                                                               <b><span style='color: #98FB98'>Confidence</span></b> in the tests; living documentation                                                                                               |
| Apply common test standards (*including naming conventions*) |                                                                                   Enables shared code/test <b><span style='color: #98FB98'>ownership and common understanding of tests</span></b>                                                                                    |
|    Separate the test (*what*) from test execution (*how*)    | Abstracting the what from the why can <b><span style='color: #98FB98'>allow the layers to evolve separately</span></b>; you can add more examples to the human-readable specification (*the test*), or you can change the underlying automation without affecting the business rules |
