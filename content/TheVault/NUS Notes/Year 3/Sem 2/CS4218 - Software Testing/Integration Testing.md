---
Title: Integration Testing
Date Created: 23-January-2026
Last Updated: 24-January-2026
Tags:
  - CS4218
  - SWE/Testing/IntegrationTesting
---
# Integration Testing
---
>[!abstract] Integration Testing
>It is an <b><span style='color: #FFD700'>automated test</span></b> which accomplishes the following:
>- <b><span style='color: #FFD700'>Verifies the integration</span></b> between multiple modules/components. Ensuring they work correctly when combined
>- Ensures <b><span style='color: #FFD700'>data is passed & process correctly</span></b> across interfaces
>- <b><span style='color: #FFD700'>Detects issues in how units work together</span></b>

Integration testing is **done by** QA engineers (*expand coverage & does more broader integration testing*), automation testers & developers (*initial integration testing*).

It is done **when** <b><span style='color: #FFD700'>unit tests are completed & before system testing</span></b>. And is **carried out in** <b><span style='color: #FFD700'>test environments</span></b> or in a <b><span style='color: #FFD700'>automated CI/CD pipeline</span></b>.

>[!success] Ensure consistency & early detection in the software development lifecycle

>[!question] Why do we do integration testing?
>It <b><span style='color: #FFD700'>catches interface & communication bugs early</span></b>. Which <b><span style='color: #98FB98'>ensures smooth & uninterrupted data flow</span></b> between 2 components.

Here are the steps to conduct integration testing:
- Prepare (*environment, scope, modules*)
- Decide integration testing approach
- Design test cases (*data flow, API interactions, control logic*)
- Integrate and Deploy Modules
- Execute Tests and Track Results
- Log and Track Defects
- Repeat with More Modules / Scenarios
## Types of Integration Testing

>[!question] How do we choose the correct integration test strategy?
> There is no 1 fixed solution it depends on:
> - Architecture, infrastructure & the code
> - Number of test harness ([[Year 3/Sem 2/CS4218 - Software Testing/Unit Testing.md#Stubs|stubs]])
> - Location of critical parts
> - Power of hardware machine
> - Deadlines
### Incremental Approach

Here we test components piece by piece. Meaning <b><span style='color: #FFD700'>modules are integrated & tested one at a time</span></b>. 

When a **new module is added**, the <b><span style='color: #FFD700'>entire system is tested</span></b> again to ensure smooth integration. For the other **components which have not been added** we can <b><span style='color: #FFD700'>use stubs or drivers</span></b> to simulate them.

>[!success] Easier to isolate bugs
>This is because changes are introduced gradually (*module by module*).

>[!success] Allows early detection of defects during integration phase
>It is easier to pin point if we add modules on by one.
#### Top Down Approach

This approach <b><span style='color: #FFD700'>starts from the top-most module & then adding lower modules step by step</span></b>. This provides us a structural way of testing our system.

For **modules which are not yet integrated**, <b><span style='color: #FFD700'>stubs are used</span></b> to simulate their behavior during testing.

**Example of a top down approach**:
![[Integration Testing Top Down Approach.png|center]]

>[!success] Early detection of high level issues
><b><span style='color: #87CEEB'>High level</span></b> means bugs related to the <b><span style='color: #FFD700'>overall system architecture & flow</span></b>.
>
>This is because the highest level component is tested first.

>[!success] Test focused on user experience
> High level components are usually user facing modules. Thus we are <b><span style='color: #FFD700'>prioritising end-to-end user functionality</span></b>.

>[!success] Efficient for hierarchical systems
>Top level modules significantly impact the behaviour of lower level ones.

>[!success] Modular & structured
>It is a <b><span style='color: #87CEEB'>gradual testing</span></b> since we integrate each module progressively.

>[!fail] Incomplete testing without lower-level modules
> Early on, lower modules are simulated using stubs & not the actual components.

>[!fail] Stub complexity
>Larger systems results in <b><span style='color: var(--mk-color-red)'>stubs being more complex & difficult to maintain</span></b> (*especially those with intricate dependencies*).

>[!fail] Late testing of lower-level modules
> They are usually tested last thus a delay in discovering these issues.

>[!fail] Increased dependency on stubs
>We use stubs often which are inaccurate representations of the real module behavior
#### Bottom Up Approach

Is the opposite of top down, we <b><span style='color: #FFD700'>start from he lower-level modules first and progressively go up</span></b>.

**Example of a bottom up approach**:
![[Integration Testing Bottom Up Approach.png|center]]

>[!success] Through testing of lower level first
>We <b><span style='color: #98FB98'>ensure the foundational components are stable</span></b> before integrating with higher level logic.

>[!success] No need for stubs
> Real modules are tested as they are integrated. Thus there is no need to simulate behavior.

>[!success] Easier to isolate & fix bugs in low level logic

>[!fail] Delayed availability of higher level features
>User facing features are tested late which will <b><span style='color: var(--mk-color-red)'>cause delays in feedback on overall functionality</span></b>.

>[!fail] Drivers are needed for higher modules
>Temporary divers are needed to simulate higher-level modules which <b><span style='color: var(--mk-color-red)'>adds development overhead</span></b>.

>[!fail] Top-level design issues found late
>Since we test the upper levels later.

>[!fail] Lack of real world use cases early
>Testing starts at a granular level & <b><span style='color: var(--mk-color-red)'>may not reflect actual issues</span></b> until higher layers are added.
#### Sandwich Approach

We consider both top down & bottom up approaches by <b><span style='color: #FFD700'>diving the system into 3 logical layers</span></b>:
- Top layer
- Bottom layer
- Target layer (*middle level modules*)

Testing will be done simultaneously from <b><span style='color: #FFD700'>top & bottom layers, then converging at the target layer</span></b>.
 
**Example of a sandwich approach**:
![[Integration Testing Sandwich Approach.png|center]]

>[!success] Combines the strengths of both top-down & bottom up approaches
>Typically chosen for more large complex systems as it <b><span style='color: #98FB98'>provides good coverage & early detection</span></b>.

>[!success] Enables early testing for critical high-level & low-level modules

>[!success] Reduces overall integration time through parallel testing

>[!success] Provides balanced coverage of both control logic & utility functions

>[!fail] Test planning & coordination can be complex

>[!fail] Integration of middle layer (target) is delayed

>[!fail] Still requires development of stubs

>[!fail] Less effective in systems that do not follow a clear layered architecture
### Big Bang Approach

Here <b><span style='color: #FFD700'>all modules are integrated simultaneously after unit testing</span></b>. So the entire system is tested as a whole.

>[!success] All real components are present there is no need for stubs

>[!fail] Difficult to isolate & fix bugs when failures occur

>[!fail] Critical defects may be discovered late in the development cycle

It may look bad to do but we can **use it when**:
- For <b><span style='color: #FFD700'>small scale systems</span></b> with limited modules
- <b><span style='color: #FFD700'>Module dependencies are simple</span></b> & well understood
- <b><span style='color: #FFD700'>Low-risk projects</span></b> where late defect discovery is acceptable
- <b><span style='color: #FFD700'>Tight deadlines</span></b> & minimal time for incremental integration