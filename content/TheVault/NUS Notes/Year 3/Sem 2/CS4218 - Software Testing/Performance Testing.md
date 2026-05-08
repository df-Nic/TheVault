---
Title: Performance Testing
Date Created: 08-March-2026
Last Updated: 13-March-2026
Tags:
  - CS4218
  - SWE/Testing/PerformanceTesting
---
# The 5W1H Of Performance Testing
---
<b><span style='color: #87CEEB'>Performance testing</span></b> is a type of <b><span style='color: #FFD700'>non-functional testing</span></b> where we measure the following attributes like:
- Speed
- Scalability
- Stability
- Responsiveness

Typically performance testing is **conducted** by <b><span style='color: #FFD700'>QA engineers, developers or DevOps</span></b>, <b><span style='color: #FFD700'>before being deployed</span></b> to production.

Performance testing is usually <b><span style='color: #FFD700'>done in a controlled test environment, mimicking production environment</span></b>.

>[!question] Why conduct performance testing?
>We need to ensure that the application <b><span style='color: #FFD700'>can handle expected user load efficiently and perform well under stress</span></b>.
>
>Helps us <b><span style='color: #98FB98'>identify bottlenecks, performance & leakage issues</span></b>.

There are **various tools** to conduct performance testing (*simulate high user loads*):
- JMeter
- k6

Typically in performance test we **configure a parameter** known as <b><span style='color: #87CEEB'>concurrent users</span></b> (*VUsers*). We denote the number of active users interacting with our application at the same time, which <b><span style='color: #FFD700'>define the load level</span></b> (*simulating what it will be like when traffic is high*).
# Performance Test Metrics
---
Here are some **examples of performance test metrics**:
![[Examples of Performance Test Metrics.png|center]]

Analyzing different performance metrics, we can <b><span style='color: #FFD700'>understand the app performance, identify bottlenecks & ensure high quality experience for users</span></b>.
## Throughput

It measures <b><span style='color: #FFD700'>how much work the system completes in a given time</span></b> (*rate of success request handling*).

>[!success] Higher throughput = more efficient & capable system
>If the system **does not meet the expected throughput** it means that it might be <b><span style='color: var(--mk-color-red)'>lacking in raw processing power</span></b>.

We can **compute throughput** as such:
$$
\text{Throughput} = \frac{\text{Total Successful Requests}}{\text{Total Time in Seconds}}
$$
## Error Rate

It is a direct <b><span style='color: #FFD700'>measure of application’s health & stability</span></b>.

We can **compute error rate** as such:
$$
\text{Error Rate} (\%) = \left(\frac{\text{Total Failed Requests}}{\text{Total Requests}}\right) \times 100
$$
>[!tldr] Failures
>They are essentially <b><span style='color: #FFD700'>unexpected things which leads to your program being in an invalid state</span></b> during a programs execution such as:
>- Internal server errors
>- Database connection issues
>- Unhandled exceptions

>[!warning] Typically anything above 1 - 2 % flags a serious underlying stability issue

## CPU Utilisation

This tells us <b><span style='color: #FFD700'>how busy server’s processor is executing tasks</span></b>. This helps us <b><span style='color: #FFD700'>understand if server resources are sufficient</span></b> for the load it’s handling.

There are **monitoring tools** which does provide this value directly.

We can **compute CPU utilisation** as such:
$$
\text{CPU Utilisation } (\%) = \left(\frac{\text{Time CUP was Busy}}{\text{Total Time Measured}}\right) \times 100
$$
Where:
- Ensure that the time is in the same units

>[!fail] Hard to isolate
>If you are running on a local machine there will be other processes which will be using your CPU.

>[!important] Here we want something in between, not too high not too low
>Too **high** (*about 80 - 90 % under expected load*), it means that our <b><span style='color: var(--mk-color-red)'>server is under provisioned & does not have enough processing power</span></b>.
>
>Too **low** (*on expected load*), it means that we are <b><span style='color: var(--mk-color-red)'>underutilizing</span></b>, thus we are <b><span style='color: var(--mk-color-red)'>spending too much on resources which we do not need</span></b>.
## Response Time

>[!note] One of the most important metric in the users perspective

It is the <b><span style='color: #FFD700'>total time needed for a user to get a complete response after sending a request</span></b>.

>[!success] We always want to aim for a low response time
>High response time means it takes very long to respond.

We can **compute response time** as such:
$$
\text{Response Time} = \text{Time}_{\text{ Last Byte Received}} - \text{Time}_{\text{ First Byte Sent}}
$$
>[!example] Example of computing response time
>If the user clicks login at 11:50:02.100 AM and the page is loaded at 11:50:02.905 AM
>
>Then the response time is 0.850 seconds or 850 miliseconds.
### 90th Percentile Response Time

Or <b><span style='color: #87CEEB'>P90</span></b> (*Or P-something*) is the <b><span style='color: #FFD700'>value in which 90% of your response time fall into</span></b> (*and 10% is slower*). So this means if the value is 1 second, it means that 90% of the user will experience a response time of 1 second or faster.

>[!question] What is wrong with our original response time
>Typically you will take the **average response times** since it can vary. But the average can be <b><span style='color: var(--mk-color-red)'>misleading since it is very sensitive to outliers</span></b>.

This is often used in <b><span style='color: #87CEEB'>service level agreements</span></b> (*SLAs*) & <b><span style='color: #87CEEB'>service level objectives</span></b> (*SLOs*) to define acceptable performance for a significant portion of users.

>[!success] It excludes the slowest 10% (*outliers*) but still account for slower interactions

>[!success] It sets a more realistic performance targets
>Because if the average is good but our 90% is bad it still means that majority of the users are having poor experience.

To **compute 90th response time**:
1) So given a **list of response times**, <b><span style='color: #FFD700'>first sort in ascending order</span></b>.
2) Compute the 90th percentile (*change depending on what you want*) index using the following formula:
$$
\text{Position} = \left(\frac{\text{Percentile}}{\text{100}}\right) \times \text{Number of data points}
$$

>[!example] How to compute 90th percentile response time
> So give the response Times (ms): 50, 60, 70, 80, 90, 100, 110, 120, 150, 500.
> 
> After sorting, 50, 60, 70, 80, 90, 100, 110, 120, 150, 500.
> 
> Compute the position for the **90th percentile**, $90/100 \times 10 = 9$. Thus our 90th percentile response time is 150ms.
> 

Sometimes taking the <b><span style='color: #87CEEB'>average x-th percentile response time</span></b> might be more useful. Instead of finding the x-th percentile we just <b><span style='color: #FFD700'>take the average</span></b>.
# Types of Performance Tests
---
There are a few types of performance testing:
- **Load** testing
- **Stress** testing
- **Spike** testing
- Recovery testing
- Volume testing
- Capacity testing
- Soak / endurance testing

The **first 3 are the most common** forms of performance testing done:
![[Load vs Stress vs Spike Testing.png|center]]
## Load Testing

The **aim** of load testing is to <b><span style='color: #FFD700'>verify system performs well under day-to-day traffic</span></b> (*expected user load*) & ensuring it meets the SLAs, by <b><span style='color: #FFD700'>simulating real-world user traffic</span></b> the application or system.

Typically this is <b><span style='color: #FFD700'>done before production deployment</span></b>.

Here we are **evaluating**:
- Response times
- Throughput
- Resource usage / utilisation
- Error rate

>[!success] Helps identify performance bottlenecks before going live

>[!success] Helps determine the system's maximum operating capacity

>[!success] Ensures reliability & scalability under normal & peak conditions

To **conduct load testing**:
1) <b><span style='color: #FFD700'>Identify the flow</span></b> you want to test (*so you know what components are being tested*)
2) <b><span style='color: #FFD700'>Identify a test strategy</span></b> (*test environment, how many concurrent users / actions etc*)
3) <b><span style='color: #FFD700'>Identify key metrics</span></b>, you want to observe (*can be any of the metrics above*)
4) <b><span style='color: #FFD700'>Gradually increase the load</span></b> from nothing to the normal levels

**After conducting the test** you will then be able to find:
- <b><span style='color: #FFD700'>Bottlenecks identification</span></b> and therefore what needs to be fixed
- Components which <b><span style='color: #FFD700'>performs as expected</span></b>

>[!info] You can alter the test environment to see the impact on different aspects
>Such as how user load, data volume changes affects your application.
## Stress Testing

Different from [[Year 3/Sem 2/CS4218 - Software Testing/Performance Testing.md#Load Testing|load testing]] where we <b><span style='color: #FFD700'>test the system beyond its normal limits to find its breaking point</span></b> (*fails or degrades unacceptably*). This can be under heavy traffic and loads.

This is done to <b><span style='color: #FFD700'>prepare the system for the worse case scenarios</span></b>.

Here we are **evaluating**:
- Response times (*higher median response times signals potential bottlenecks in high loads*)
- Error rate (*high error rates means potential overloaded servers, code bugs or network problems*)

>[!success] Helps identify how the system behaves under extreme load
>It can also <b><span style='color: #98FB98'>identify key functionalities</span></b> of the system. Since as we observe how the system behaves we <b><span style='color: #FFD700'>also can tell which functionalities are the ones under high load, denoting its importance</span></b>.
>
>It can also <b><span style='color: #FFD700'>identify bottlenecks</span></b>.

>[!success] Identify points of failures or crash points & how the system recovers / fails
>If too much traffic does it gracefully degrade itself (*slow down*) or just crash. And then <b><span style='color: #FFD700'>how does it recover from it</span></b>.

>[!success] Evaluates stability, error handling & robustness under pressure as well as system's scalability

To **conduct stress testing**:
1) <b><span style='color: #FFD700'>Identify the flow</span></b> you want to test (*so you know what components are being tested*)
2) <b><span style='color: #FFD700'>Identify a test strategy</span></b> (*test environment, how many concurrent users / actions etc*)
3) <b><span style='color: #FFD700'>First test with normal load</span></b>, then <b><span style='color: #FFD700'>slowly ramp up</span></b> the traffic until the application begins to exabit performance degradation

>[!example] Stress tests are usually executed using Apache JMeter
### Spike Testing

It is a **type of stress testing** <b><span style='color: #FFD700'>focused on sudden and extreme increases in load</span></b> (*essentially abrupt spikes in traffic due to like flash sales or viral events*).

Here we are **evaluating**:
- Average response time (*for critical functions*)
- Error rate
- Throughput
- CPU & Memory utilisation
- Connection time (*how many with your application or database*)
- Latency (*is there a delay in response because of the spike*)
- Scalability (*how fast and how many new instances are deployed*)

>[!success] Evaluates how the system handles rapid changes in load volume

>[!success] Helps assess stability, responsiveness, and recovery after the spike
>Essentially how the sudden spike impacts our users in any way.

>[!success] Detects issues like server crashes, slowdowns, or throttling

To **conduct spike testing**:
1) <b><span style='color: #FFD700'>Identify the flow</span></b> you want to test (*so you know what components are being tested*)
2) <b><span style='color: #FFD700'>Identify a test strategy</span></b> (*test environment, how many concurrent users / actions etc*)
3) <b><span style='color: #FFD700'>First test with normal load</span></b>
4) Then <b><span style='color: #FFD700'>determine a spike trigger</span></b>, which says how much to increase the traffic in some amount of time
5) <b><span style='color: #FFD700'>Determine the spike duration</span></b>, how long to main the spike for
6) Then <b><span style='color: #FFD700'>recover from the spike</span></b>, basically ramps down the load over some about of time
7) Then do a <b><span style='color: #FFD700'>post spike observation</span></b>, here we see how our app behaves when back in normal load for some amount of time

>[!info] Notice that we are actually just simulating a spike where there is a sudden increase then decrease
## Volume Testing

Also known as <b><span style='color: #87CEEB'>flood testing</span></b>, tests <b><span style='color: #FFD700'>system performance with a large volume of data</span></b>. Typically it focuses on database size, file size or input data.

The **goal** of volume testing is to <b><span style='color: #FFD700'>determine the threshold at which the system becomes unstable or crashes</span></b> & <b><span style='color: #FFD700'>how changes in data insertion and user simulation frequency affect this threshold</span></b>.

>[!success] Checks how the system handles high data volumes over time

>[!success] Helps identify issues like data overflow, slow queries, and memory usage
>Hopefully we will encounter issues when data scales.

>[!success] Ensures the system remains stable and responsive with large datasets

To **conduct volume testing**:
- We need to use <b><span style='color: #FFD700'>2 thread groups</span></b> to be used in parallel
	1) **Database data loader** (*is like an engine to create our test environment*)
	2) **Simulated user actions**

Here are the **tasks for the 2 thread groups**:

|     Purpose     |                                 Database data loader                                 |                                     Simulated user actions                                      |
| :-------------: | :----------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------: |
|     Purpose     | <b><span style='color: #FFD700'>Simulate a progressively growing database</span></b> | <b><span style='color: #FFD700'>Simulate real-world user behavior on the application</span></b> |
|     Threads     |                            1 (*isolate growth behavior*)                             |                        20 (*or more just to simulate concurrent users*)                         |
| Ramp-up period  |                                         N/A                                          |                                           20 seconds                                            |
|   Loop count    |                                         1000                                         |                                               500                                               |
| Iteration delay |                             Delay to run each iteration                              |                                   Delay to run each iteration                                   |
|   Core logic    |                At each iteration inserts an increasing number of data                |                                            Simulates                                            |
|    Rational     |                              Mimics a growing business                               |                Test the application under concurrent use with a growing dataset                 |
| implementation  |                                  Project dependent                                   |                                        Project dependent                                        |
| Listeners used  |                                  Project dependent                                   |                                        Project dependent                                        |
With our test formulated we can **track** things such as:
- Response times
- Error rate
- Latency
- etc..
## Recovery Testing

Also known as <b><span style='color: #87CEEB'>reliability testing</span></b>, tests <b><span style='color: #FFD700'>how well a system recovers from crashes, failures, or unexpected interruptions</span></b> (*restore operations after hardware, software or network failures*).

Here we <b><span style='color: #FFD700'>simulate failure scenarios</span></b> like power outages, system reboots, or database crashes.

>[!success] Evaluates data integrity, availability, and session continuity post-recovery

>[!success] Ensures minimal data loss and downtime during recovery
>We can also know how fast it takes to recover.

>[!success] Can identify critical components
>For example if the database is down then the application cannot run. Therefore we will need backup / secondary databases to ensure minimal downtime.

To **conduct spike testing**:
1) <b><span style='color: #FFD700'>Trigger a failure</span></b> (*database down or network issues*)
2) <b><span style='color: #FFD700'>Monitor the systems reaction</span></b> (*what it does and how long does it take*)
3) Analyse the user experience (*what error messages is shown and are they helpful*)
4) <b><span style='color: #FFD700'>Verify data integrity and state</span></b> (*ensure that after recovery the database is in a valid state*)
## Capacity Testing

A type of performance test that <b><span style='color: #FFD700'>determines the maximum number of users</span></b> a system can handle <b><span style='color: #FFD700'>while still meeting its performance goals</span></b>.

We can look at some **metrics** like:
- Maximum load capacity
- Error rate
- Latency / TTFB (*TTFB is JMeters equivalent to latency*)
- CPU, memory

>[!tldr] Essentially we want to find the upper limit of a system's capacity before performance starts to degrade unacceptably
>This "performance" can be for any of the metrics that you want to observe like response time, latency and so on.

>[!question] Load vs Capacity vs Stress what is the difference
>**Load** testing is to test on expected load, **capacity** goes beyond by finding the maximum number of users we can support. **Stress** testing goes beyond this maximum and see how our system fails.

To **conduct capacity testing**:
1) <b><span style='color: #FFD700'>Set a threshold</span></b> (*some limit for our system like 75th percentile for latency cannot exceed 1800ms*)
2) Then start from no load and <b><span style='color: #FFD700'>gradually increase until the threshold has been exceeded</span></b>
## Soak Testing

Also known as <b><span style='color: #87CEEB'>endurance testing</span></b>, evaluates a system's <b><span style='color: #FFD700'>stability and reliability when subjected to a typical production workload over a long period</span></b> (*can the system operate consistently without issues for very long periods of time*).

>[!success] Uncover bugs that only manifest over time
>Some of these include:
>- Memory leaks (*system fails to release memory leading to slowing down or crashing*)
>- Resource exhaustion (*gradual depletion of finite system resources like CPU cycles or file handles*)
>- Performance degradation (*System response times get slower the longer it runs*)
>- Unexpected crashes (*Failures that occur after prolonged continuous operation*)

>[!success] Ensures long term health & reliability
>With this it <b><span style='color: #FFD700'>gives confidence</span></b> that the system will continuously perform reliably for users.

We can look at some **metrics** like:
- Throughput
- Response time
- HTTP error rate

>[!question] What is the difference between soak & stress testing
>**Soak** testing is to test endurance & stability under <b><span style='color: #FFD700'>normal workload for a long period of time</span></b>.
>
>**Stress** testing on the other hand is to test the breaking point under <b><span style='color: #FFD700'>extreme workloads for a short amount of time</span></b>.

To **conduct capacity testing**:
1) <b><span style='color: #FFD700'>Define a test environment</span></b>
2) <b><span style='color: #FFD700'>Define user actions and simulate user behaviour</span></b> for a long period (*some tools to use are JMeter*)

