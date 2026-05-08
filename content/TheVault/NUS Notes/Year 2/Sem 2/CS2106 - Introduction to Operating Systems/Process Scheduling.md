---
title: Process Scheduling
Date Created: 2025-02-01
Last Updated: 2025-09-28
tags:
  - CS2106
  - Processes
  - ProcessScheduling
---
# Concurrent Execution
---
<span style='color:var(--mk-color-turquoise)'>Concurrent processes</span>, is a logical concept to cover multitasked processes, this is achieved through:
- **Virtual parallelism** - One CPU doing many things (*Spilt the running time*)
- **Physical parallelism** - Many CPUs doing things at the same time

> [!note] Timeslicing
> For **1 CPU to do virtual parallelism**, it <span style='color:var(--mk-color-yellow)'>splits the time into segments</span> and allow a <span style='color:var(--mk-color-yellow)'>process to run in this spilt before switching</span> to another process in another spilt.
> 
> In the process of switching processes the **OS will need to do a context switching**, which <span style='color:var(--mk-color-yellow)'>takes time in the spilt also</span>.

> [!question] How the OS do a context switch if its not running?
> When a **process is running** the <span style='color:var(--mk-color-red)'>OS will not be running</span>.
> 
> One way is to utilise the <span style='color:var(--mk-color-yellow)'>timer which raises interrupts</span> (*timer interrupt*), which only the OS can intercept. For <span style='color:var(--mk-color-yellow)'>each time slice, it will count down</span> once it reaches 0, the <span style='color:var(--mk-color-turquoise)'>interrupt service routine</span> (*ISR*) will invoke the **scheduler** in the OS.
> 
> Another way is, if a process needs to [[Process Abstraction#Blocked State|wait for an event]] it will execute the OS code which will <span style='color:var(--mk-color-yellow)'>pass control to another process</span>.
## Scheduling

One main challenge is <span style='color:var(--mk-color-red)'>what process should run next</span>. This is known as the scheduling problem. In the OS there is a <span style='color:var(--mk-color-turquoise)'>scheduler</span> which does these decisions and it uses a <span style='color:var(--mk-color-turquoise)'>scheduling algorithm</span>.

> [!info] Process behaviour
> Each process has its **own CPU time requirement**. This behaviour has <span style='color:var(--mk-color-orange)'>2 phases</span>:
> 1) **CPU Activity** - Does all the computation (*Compute-Bound processes*)
> 2) **IO Activity** - Request and receiving services from I/O devices (*IO-Bound processes*)

> [!tldr] Process environment
> It <span style='color:var(--mk-color-yellow)'>influences</span> the way **processes are allocated**.
> 
> There are <span style='color:var(--mk-color-orange)'>3 types of processing environment</span>:
> 1) **Batch processing** - No user interaction & responsiveness is required
> 2) **Interactive** - Or multiprogramming, where there are active users interacting with the system, it must be responsive & consistent in response time
> 3) **Real time processing** - Usually there are deadlines to meet & they have periodic process

These scheduling algorithms have a <span style='color:var(--mk-color-orange)'>performance citeria</span>:
- **Fairness** - All process should get a fair share of the CPU time or <span style='color:var(--mk-color-green)'>no starvation</span> (*By process or user basis*)
- **Balance** - All parts of the computing system should be utilized equally

> [!question] What are the different scheduling policies?
> There are <span style='color:var(--mk-color-orange)'>2 scheduling policies</span>:
> 1) **Non-preemptive** (*cooperative*) - Process stays running until its <span style='color:var(--mk-color-yellow)'>blocked or it gives up the CPU voluntarily or the time quantile finishes</span>.
> 2) **Preemptive** - Process is given a <span style='color:var(--mk-color-yellow)'>fixed time quota to run</span>, it can also be blocked or give up early also.
### Batch Processing

The idea of <span style='color:var(--mk-color-turquoise)'>batch processing</span> is to take a process and run it on a computer and it <span style='color:var(--mk-color-yellow)'>need not have any human interaction</span>.

And it usually follow the <b><mark style='background:var(--mk-color-yellow)'>non-preemptive scheduling policy</mark></b>, as you **want to finish the process first** before doing something else.

> [!example] Olden bank transfer process
> The bank will compile the **days transactions on a tape** and will pass it to the other bank. The other bank will put the tape on a **tape reader and it will read and update their accounts**.

The **scheduling algorithms used for batch processing** are generally <span style='color:var(--mk-color-green)'>easy to implement</span> and can be improved for other types of systems.

> [!abstract] Evaluation criteria for batch processing 
> 1) **Turnaround time**
> > The turnaround time for a process is $\text{waiting time} + \text{time to finish the process}$. It is related to the <span style='color:var(--mk-color-yellow)'>waiting time</span> for the CPU.
> 2) **Throughput**
> > Total number of <span style='color:var(--mk-color-yellow)'>tasks finished per unit time</span>
> 3) **CPU utilization**
> > **Percentage of time** when <span style='color:var(--mk-color-yellow)'>CPU is working on a task</span>. Not always 100% for instance when waiting for I/O input (*We want this to be high as possible*).
> 4) **Waiting time**
> > It is the <span style='color:var(--mk-color-yellow)'>turnaround time - process time</span>
> 5) **Average waiting time**
> > It is just the average <span style='color:var(--mk-color-yellow)'>waiting time</span>.
> 6) **Response time**
> > It is how long the process wait before starting or the <span style='color:var(--mk-color-yellow)'>starting time - arrival time</span>.
#### First-Come First-Served (FCFS)

Just like <span style='color:var(--mk-color-purple)'>queue</span>, the first process that <span style='color:var(--mk-color-yellow)'>comes first will be served first</span>. Assuming there are **no infinite loops** (*bounded*), there will be <b><mark style='background:var(--mk-color-green)'>no starvation</mark></b> as the number of tasks will always decrease. And it is <b><mark style='background:var(--mk-color-yellow)'>non-preemptive</mark></b>.

> [!info] Starvation
> When there is starvation, it means that <span style='color:var(--mk-color-red)'>not all process will be given a chance to run</span>.
> > [!note] Preemptive scheduling can result in no starvation even with processes not bounded

> [!failure] Shortcomings for first-come first-served
> - Not <span style='color:var(--mk-color-red)'>optimal average waiting time</span>, a simple reordering of the process can reduce this waiting time.
> - A more serious issue is the <span style='color:var(--mk-color-red)'>convoy effect</span>.
>   
>  > [!info] Convoy effect
> > Lets say we have a process **A which takes up a lot of CPU time** (*CPU-bound*) and needs to wait for I/O.
> >
> > Then we have many **smaller shorter process which execute quickly** and wait for I/O. Which results in the <span style='color:var(--mk-color-red)'>CPU not being utilised at all</span> since everyone is waiting for I/O.
#### Shortest Job First (SJF)

Assuming we **know how long each process takes** (*not easy to do*) and they are **ready to be executed**, then the scheduler can <span style='color:var(--mk-color-yellow)'>select the task with the smallest total CPU time</span> first. And it is <b><mark style='background:var(--mk-color-yellow)'>non-preemptive</mark></b>

This **solves an issue from** [[Process Scheduling#First-Come First-Served (FCFS)|FCFS]] by <span style='color:var(--mk-color-green)'>reducing the average waiting time</span>. However this <b><mark style='background:var(--mk-color-red)'>can cause starvation</mark></b> as a continuous queuing of shorter jobs will not allow longer jobs to execute.

> [!question] How do we know how long each process takes?
> We can **predict the CPU usage** by by the <span style='color:var(--mk-color-yellow)'>previous CPU-bound phases</span>.
> 
> A common approach is through <span style='color:var(--mk-color-turquoise)'>exponential average</span>:
> $$\text{Predicted}_{n + 1} = (\alpha) \text{Actual}_{n} + (1 - \alpha)\text{Predicted}_n$$
> 
> Here $\alpha$ which is between 0 to 1 is the **weight** placed on recent events or past history (*which one is more important*).
#### Shortest Remaining Time (SRT)

It is a variation of SJF, but unlike SJF, it is <b><mark style='background:var(--mk-color-yellow)'>preemptive</mark></b>. Instead of just taking the shortest total time, it will take the <span style='color:var(--mk-color-yellow)'>shortest remaining time</span>. This is better if the <span style='color:var(--mk-color-green)'>shorter processes comes in at a later time</span> but it <b><mark style='background:var(--mk-color-red)'>can cause starvation</mark></b>.

> [!example] Example of SRT
> Assuming now task A is running in the CPU & task B comes in. The remaining time for task A is larger than task B. Then task B will now use the CPU while task A is removed from the CPU.
### Interactive Systems

In **interactive systems, scheduling algorithms** are <span style='color:var(--mk-color-yellow)'>usually preemptive</span>. This is to <span style='color:var(--mk-color-green)'>ensure a good response time & good predictability</span>.

> [!abstract] Evaluation criteria for interactive systems 
> 1) **Response time**
> > The **time** it takes <span style='color:var(--mk-color-yellow)'>between a request and the response</span> by the system.
> 2) **Predictability**
> > It is more on the <span style='color:var(--mk-color-yellow)'>consistency of our response time</span>. We want to <span style='color:var(--mk-color-green)'>have less variation</span> for more predictability.

> [!info] Interval of timer interrupt
> Or <span style='color:var(--mk-color-turquoise)'>ITI</span> or inter-tick interrupt. Which the [[Process Scheduling#Concurrent Execution|OS scheduler gets triggered at every interval ]]. Typical intervals are from 1ms (*called a jiffy*) to 10ms.

**Each process** will be given a <span style='color:var(--mk-color-yellow)'>fixed or variable interval</span> (*multiples of  the time interval*) to run, this is known as a <span style='color:var(--mk-color-turquoise)'>time quantum</span>.

Every time the timer interupts, the **scheduler will decrease the time quantum of the process, until it reaches 0** at which case it will hand control over to the next process.

> [!question] Why do we prefer the time quantum to be variable
> Typically, the **time quantum of a process will decrease as it runs**, until it becomes a small enough number. This is to ensure that a <span style='color:var(--mk-color-green)'>more fair distribution of CPU time is given to all processes</span> (*fairness which is another scheduler citeria*).
#### Round Robin (RR)

Similar to [[Process Scheduling#First-Come First-Served (FCFS)|first-come first-serve]]. Take the <span style='color:var(--mk-color-orange)'>first task and run it until</span>:
- Give up the CPU voluntarily
- Task blocks
- Process sleeps
- Until the **time quantum has elapsed**

Afterwards the process will be <span style='color:var(--mk-color-yellow)'>placed at the end of the queue</span>, for a **FCFS** scheduling (*except for blocked task*) awaiting for another turn, thus there will be <b><mark style='background:var(--mk-color-green)'>no starvation</mark></b>.

RR <b><mark style='background:var(--mk-color-green)'>guarantees a response time</mark></b>, given $n$ tasks and $q$ quantum, the time for a task to get the CPU is bounded by $(n - 1)q$.

> [!note] Choice of time quantum is important
> **Long time quantum**
> > It has a <span style='color:var(--mk-color-green)'>better CPU utilization</span> (*assuming no I/O calls*), however the <span style='color:var(--mk-color-red)'>waiting time is longer</span> (*poorer response*).
> 
> **Small time quantum**
> > It has a <span style='color:var(--mk-color-green)'>shorter waiting time</span>, but a <span style='color:var(--mk-color-red)'>larger overhead</span> (*bad CPU utlisation*) because of [[Process Abstraction#Running State|context switching]].
#### Priority Scheduling

Most OS's will have some sort of priority, for instance **foreground applications have a higher priority** (*more important*) than those in the background. All this is to <span style='color:var(--mk-color-green)'>ensure user satisfaction</span>.

Essentially all <span style='color:var(--mk-color-yellow)'>process will have its own priority</span> and the one with the <span style='color:var(--mk-color-yellow)'>highest priority is will be chosen first</span>.

> [!summary] Variants of priority scheduling
> 1) **Preemptive version**
> > <span style='color:var(--mk-color-yellow)'>Lower priority running process can be preempted</span> when a higher priority process comes in.
> 2) **Non-preemptive**
> > Late coming high priority process has to <span style='color:var(--mk-color-yellow)'>wait for the next round of scheduling</span> (*also need to wait for lower priority process waiting for I/O*).

> [!info] Why is 0 / 1 the highest priority generally
> Because the largest number depends on the system (*32 or 64 bit*), however priority's are usually unsigned integer and the smallest is 0 which is constant throughout.

> [!failure] Shortcomings of priority scheduling
> - It <b><mark style='background:var(--mk-color-red)'>can cause starvation</mark></b>, a <span style='color:var(--mk-color-yellow)'>high priority process keeps streaming in</span> and hogging the CPU.
> - <span style='color:var(--mk-color-red)'>Hard to control the exact amount of CPU time given </span>to a process 
> - <span style='color:var(--mk-color-red)'>Priority inversion</span>
> 
> > [!info] Priority inversion
>  > Lets assume we have task C, which locks a resource (*file*). Then a higher priority task B preempts C. Then a even higher process A comes but requires resources used by C. Since it is locked it will go to a blocked state and B will continue executing. And it <span style='color:var(--mk-color-red)'>B hogs the CPU, the higher priority process will never get to run</span>
> 
> > [!question] How can we solve this?
> > One way is by <span style='color:var(--mk-color-yellow)'>decreasing priority of currently running process</span> every time quantum.
> > 
> > Or the <span style='color:var(--mk-color-yellow)'>running process can be given a time quantum</span>. Which can force it to give up the CPU for lower priority processes.
> > 
> > To **solve priority inversion**, the OS can **temporary promote the lower priority task** to the <span style='color:var(--mk-color-yellow)'>same priority as the higher priority task</span>.
#### Multi-level Feedback Queue (MLFQ)

This **solves an issue** which is to <span style='color:var(--mk-color-orange)'>schedule without perfect knowledge</span>. MLFQ unlike other algorithms is <span style='color:var(--mk-color-yellow)'>adaptive</span>. And instead of traditional priority, they use <span style='color:var(--mk-color-yellow)'>priority levels</span> (*Multiple queue / priority queue*).

The goal of MLFQ is to <span style='color:var(--mk-color-green)'>minimise both</span>, **response time I/O bound processes** (*higher priority for I/O bound processes*) and **turnaround time for CPU bound processes** (*higher priority for CPU bound processes*).

> [!example] Example of how MLFQ works
> **Basic rules**:
> - If priority A $\gt$ priority B then A will run
> - If priority A = priority B then both will run in **RR first-come first-serve**
> 
> **Priority changing rules**:
> - When a **new process comes** in it will get the <span style='color:var(--mk-color-yellow)'>highest priority</span> for a <span style='color:var(--mk-color-green)'>good response time</span>
> - When a job **fully utilized its time quantum**, its <span style='color:var(--mk-color-yellow)'>priority will reduce</span>
> - When a job **gives up or gets blocked before the time quantum finishes**, the <span style='color:var(--mk-color-yellow)'>priority retains</span>
> - Some implementation can **periodically bump up the priority**, this <span style='color:var(--mk-color-green)'>reduces starvation</span>
> - Some can check how much CPU usage total, it can **bump down the priority**, this can <span style='color:var(--mk-color-green)'>prevent apps to constantly finish before their time quantum to retain a high priority</span>.

![[MLFQ Example.png|center|500]]

So **why is there good response for I/O bound process**. The program can **make an I/O call** <b><mark style='background:var(--mk-color-yellow)'>right before its quantum finishes</mark></b>, which does not reduce its priority. 

> [!failure] One big issue with this
> The retaining of priority <span style='color:var(--mk-color-red)'>can be abused</span> here, by **making a process to block before the full time quantum** (`sleep`), <span style='color:var(--mk-color-red)'>keeping the high priority status</span>.

Also if the set of jobs is **homogeneous** , it will also result in a <span style='color:var(--mk-color-red)'>worse response time</span>.
#### Lottery Scheduling

Each process will be **given a number lottery tickets** and <span style='color:var(--mk-color-yellow)'>scheduler will randomly pick an eligible ticket</span> and the winner is granted the resource.

Assuming the **randomness is uniformly distributed**, then a **process with a percentage of the tickets** will <span style='color:var(--mk-color-yellow)'>have that percentage chance of winning</span> (*the process holds that % of the CPU time in the long run*).

> [!abstract] Properties of lottery scheduling
> 1) **Responsive**
> > A newly created process can participate in the text lottery.
> 2) **Good level of control**
> > We can <span style='color:var(--mk-color-yellow)'>control how much CPU time is given to a process</span> by giving it a certain amount of tickets. This is <span style='color:var(--mk-color-green)'>good if that process has many child process</span>, the tickets will be distributed to its child, thus that process will not have additional CPU time from its many child processes.
