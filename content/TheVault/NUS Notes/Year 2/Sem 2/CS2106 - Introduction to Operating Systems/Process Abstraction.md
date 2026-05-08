---
title: Process Abstraction
Date Created: 2025-01-22
Last Updated: 2025-09-28
tags:
  - CS2106
  - Processes
---
# Process Abstraction
---
To create a process, it is a <span style='color:var(--mk-color-turquoise)'>process abstraction</span> which <span style='color:var(--mk-color-orange)'>consists of 3 contexts</span>:
1) **Memory context**
	- Code & Data
	- Function call
	- Dynamically allocated memory
2) **Hardware context**
	- Registers
	- PC (*Program counter*)
	- Stack pointer (*SP*)
	- Frame pointer (*FP*)
3) **OS Context**
	- Process State
	- Process properties
	- Resources used

These **processes need to be managed**, and to achieve this there are <span style='color:var(--mk-color-turquoise)'>process control block</span> and <span style='color:var(--mk-color-turquoise)'>process table</span>.

Thus a <span style='color:var(--mk-color-turquoise)'>process</span>, is a **dynamic abstraction for executing programs**.

> [!faq] Why are processes important?
> For example, when **2 programs are executed**, they might **use the same set of registers** (*Which we only have 1 set of*). Thus these **processes** will know <span style='color:var(--mk-color-yellow)'>when to save and load register data</span> when switching between the 2 programs.
> 
> Thus it <b><mark style='background:var(--mk-color-yellow)'>knows what is happening between programs</mark></b>.
# Executables
---
Also known as <span style='color:var(--mk-color-turquoise)'>binary</span> consists of **2 components**, <span style='color:var(--mk-color-yellow)'>instructions</span> and <span style='color:var(--mk-color-yellow)'>data</span>. These executables are program files located in the disk drive.

A binary will consist of a few things <span style='color:var(--mk-color-orange)'>when idle</span>:
**In the header**
- MZ (*Magic number to tell OS it is a valid executable*)
- How much space the instruction require
- How much space the global variables need
- Initial content of the global variable
**In the body**
- Machine instructions or compiled code

During <span style='color:var(--mk-color-orange)'>execution</span> it requires more instructions:
- **Memory context** (*Instructions & Data*)
- **Hardware context** (*General purpose registers, PC, ...*)
- And other types of memory usage
# Memory Context
---
Memory in a process is <span style='color:var(--mk-color-yellow)'>divided into different sections</span> for different types of data.

![[Memory Allocation.svg|center|300]]
## Function Call

> [!bug] Issues to handle during function calls
> 1) **Control flow**
> > Need to <span style='color:var(--mk-color-yellow)'>jump between functions</span> and return to the caller once its done. (*Using <span style='color:var(--mk-color-red)'>PC  + 4 will not work</span> as when we jump we will update PC*)
> 2) **Data storage**
> > <span style='color:var(--mk-color-yellow)'>Pass parameters</span> into a function and <span style='color:var(--mk-color-yellow)'>capture the return result</span>.

How this is solved is **during a function call**, a <span style='color:var(--mk-color-turquoise)'>stack frame</span> (*or calling frame*) <span style='color:var(--mk-color-yellow)'>will be created</span> in the stack region inside of the memory.

> [!info] Inside the stack frame
> Inside a <span style='color:var(--mk-color-orange)'>stack frame will contain the following</span> (*Not fixed there can be many implementations*):
> 
> ![[Stack Frame Visualisation.svg|center|400]]
> 
> > There is <span style='color:var(--mk-color-green)'>no need to follow the ordering</span> of the stack, but **ensure the values saved are correct**.

When invoking a function, the <b><mark style='background:var(--mk-color-yellow)'>values of the parameters will be copied over to the stack frame</mark></b>. Thus, no argument is passed, thus it is <span style='color:var(--mk-color-orange)'>pass by value</span>.

> [!question] Difference between SP & FP
> > [!note] Stack Pointer
> > It **points to the top of the stack** which indicates the <span style='color:var(--mk-color-yellow)'>first unused memory location</span>.
> > 
> > This is usually <span style='color:var(--mk-color-yellow)'>stored in special registers called SP</span>.
> 
> > [!note] Frame Pointer
> > It **points to the start of the stack frame**. This is useful as, the **data in the stack frame** can be <span style='color:var(--mk-color-yellow)'>accessed via a fixed point</span> rather than a dynamic point (*SP can change during execution, for instance saving registers*).
> > 
> > This is usually <span style='color:var(--mk-color-yellow)'>stored in special registers called FP</span>.
### Saving Registers

We know that as **programs / function changes** we will need to <b><mark style='background:var(--mk-color-yellow)'>save a copy of the registers</mark></b> before handing over control (*What to save is known by the compiler*). But what if we have <span style='color:var(--mk-color-pink)'>more variables than registers</span>?

We can do something known as <span style='color:var(--mk-color-turquoise)'>register spilling</span>, essentially we can:
1) Save the value in a register to the <span style='color:var(--mk-color-yellow)'>stack</span> (*Saved registers segment*)
2) Replace the value with a new one
3) Restore the old value when needed from memory
### Setup

How to <span style='color:var(--mk-color-orange)'>set up a stack frame</span>:
**Caller**:
- Save the FP and SP to the stack
- Save the return PC on the stack
- Copy SP to FP and move SP to reserve sufficient space for **parameters**
- Pass arguments with registers onto the stack

Afterwards **control is transfer over** to the callee (*Jump instruction*).

**Callee**:

- Allocate space for **local variables** (*Move SP also*)
- Save registers used by callee (*Ensure the values by caller wont get lost*)
- Write result to stack

> [!question] Where to store the return variable
> Either we can <span style='color:var(--mk-color-yellow)'>allocate when moving the SP</span> or <span style='color:var(--mk-color-yellow)'>overwrite the first argument</span> in the stack frame.
### Teardown

How to <span style='color:var(--mk-color-orange)'>teardown a stack frame</span>:
**Callee**:
- Restore saved registers in the stack (*Used by caller*)
- Fetch return PC

**Transfer control back** to caller <span style='color:var(--mk-color-yellow)'>using saved PC</span>.

**Caller**:
- Retrieve result
- Restore saved registers and FP and SP
- Continue execution

> [!attention] Data in the stack frame does not get deleted
> Notice that we <b><mark style='background:var(--mk-color-yellow)'>only move the SP back</mark></b>, we <span style='color:var(--mk-color-red)'>do not erase the data</span> when tearing down.
> 
> Thus, never assume a new variable will have a initial value of 0.

> [!info] Accessing return result
> How does it access the return result when SP and FP are reverted. This is where <span style='color:var(--mk-color-yellow)'>displacement</span> comes in, `lw $s1, 20($SP)`, we can as the example shows use the SP and displace it by 20 to retrieve relevant data.
> 
> And the compiler will know how much to displace it by, because in <span style='color:var(--mk-color-purple)'>C</span>, we <span style='color:var(--mk-color-yellow)'>declare the return and variable types</span> ahead of time, allowing it to **know how much memory a function requires and where exactly each variable is stored in**.
## Dynamically Allocated Memory

It is <span style='color:var(--mk-color-yellow)'>memory acquired during execution time</span>. It can request or delete memory throughout execution. <span style='color:var(--mk-color-turquoise)'>Dynamic variables</span> are like your objects, arrays, lists.

> [!question] Can we use data or stack regions?
> 
> > [!missing] Cannot place in data region
> >Global variables lifespan is the lifetime of the whole program. The OS will **need to know** before hand how <span style='color:var(--mk-color-yellow)'>much memory to allocate for the data region</span>. However <span style='color:var(--mk-color-red)'>dynamic variables are declared at runtime which the OS will not know how large it will be</span>.
>
> > [!missing] Cannot place in stack region
> A **stack frame only exists until the function returns**, however <span style='color:var(--mk-color-yellow)'>dynamic variables exists until it is deallocated</span>. Thus we cannot place in the stack.

This is where the <span style='color:var(--mk-color-turquoise)'>heap segment</span> of the memory comes in. Thus when we call `malloc()` or `new`, it will allocate space on the heap.

In <span style='color:var(--mk-color-purple)'>C</span>:
- `int *x` is to denote that `x` will store an **address to an integer**
- `x* = 1` or `*x = 1` **access the value** that the address is pointing to.
- `&x` is to **get the memory address of variable** `x` <b><mark style='background:var(--mk-color-red)'>not the address stored in variable</mark></b> `x`.

> [!danger] Issues with managing heap memory
> The size is variable and the allocation and deallocation is not known before hand.

> [!tldr] Holes
> In **heap memory**, there will be **"holes"** (*pockets of free space*), and even if the **total of these pockets are enough to store** more memory, if <span style='color:var(--mk-color-red)'>these pockets are not big enough individually allocation will still fail</span>. 
# OS Context
---
## Process ID & State

### Process ID

> [!info] Process identification
>  This <span style='color:var(--mk-color-turquoise)'>PID</span> is a <span style='color:var(--mk-color-yellow)'>unique</span> id which <span style='color:var(--mk-color-yellow)'>distinguishes processes</span> from each other.

> [!bug] OS dependent issues with PID
> - Will the PIDs be reused
> - Is there a limit to the maximum number of processes
> - Are there reserved PIDs (*Some OS reserve PID for special programs like in linux*)
### Process State

A process state is more than just running or not running. It <span style='color:var(--mk-color-orange)'>can be ready to run but not actually executing</span>. This **state** is an<span style='color:var(--mk-color-yellow)'> indication</span> of the execution status.

With **1 CPU**, there can be <span style='color:var(--mk-color-yellow)'>at most 1 process running</span> and <span style='color:var(--mk-color-yellow)'>1 transitions at a time</span>. With $n$ CPUs, there can be $\le n$
processes and parallel transitions.

> [!warning] The OS is not a process
> The OS is a <b><mark style='background:var(--mk-color-yellow)'>program</mark></b>. It <span style='color:var(--mk-color-yellow)'>does not maintain states</span> of itself and it also <span style='color:var(--mk-color-yellow)'>creates & manages processes</span>.
#### 5-State Process Model

![[5-State Process Model.svg|center]]

This process model is for **1 individual process**, <span style='color:var(--mk-color-yellow)'>each process will have its own state model</span>.
##### The 5 States
###### New State

As mentioned [[Process Abstraction#Executables|before]]an executable itself will contain a set of information. When we **load the program**, the <span style='color:var(--mk-color-yellow)'>OS will need to allocate memory</span> (*for the different segments*) **based on what is in the header**.

At this point, we are **creating a new process** and thus it is in a <span style='color:var(--mk-color-turquoise)'>new state</span>.
###### Ready State

Once the program has <span style='color:var(--mk-color-yellow)'>loaded its instructions, global variables etc</span>, it will be in a <span style='color:var(--mk-color-turquoise)'>ready state</span>.

> [!important] Being ready does not mean it should run. Other / current processes might be more important
###### Running State

When it is time to <span style='color:var(--mk-color-yellow)'>run this application</span>, it will be in a <span style='color:var(--mk-color-turquoise)'>running state</span>. **When to run** is <span style='color:var(--mk-color-yellow)'>determined by a scheduler</span>.

> [!info] Context switching
> When it is time for an application to run, the OS will do a <span style='color:var(--mk-color-turquoise)'>context switch</span>, where it will <span style='color:var(--mk-color-orange)'>do 2 things</span>:
> 1) **Save** the currently running processer's registers
> 2) **Load** the register values used by the new process

The **currently running process** will be released from the CPU and will <span style='color:var(--mk-color-yellow)'>enter a ready state</span>.
###### Blocked State

When a process is <span style='color:var(--mk-color-yellow)'>in a running state and is waiting</span> for something, it will switch into a <span style='color:var(--mk-color-turquoise)'>blocked state</span>.

> [!important] It goes back to a ready state upon the event occurring
> In a blocked state, when the application gets what its needed it will <b><mark style='background:var(--mk-color-yellow)'>go into a ready state</mark></b>. It will <span style='color:var(--mk-color-red)'>not go back to a running state</span> because it might <span style='color:var(--mk-color-yellow)'>not be the most important process</span>.
###### Terminated State

When a **application exits**, it will go into a <span style='color:var(--mk-color-red)'>terminated state</span>. All the <span style='color:var(--mk-color-yellow)'>allocated memory will be freed up</span> to be used by other processes.
##### Queuing Model

![[Queuing Model of 5 State Transition.svg|center]]

These queues are used to <span style='color:var(--mk-color-yellow)'>determine which processes should run</span>. This queue is called a <span style='color:var(--mk-color-turquoise)'>ready queue</span> can be a normal <span style='color:var(--mk-color-purple)'>queue</span> or a <span style='color:var(--mk-color-purple)'>priority queue</span>.

There is also a <span style='color:var(--mk-color-turquoise)'>blocked queue</span>, this is for <span style='color:var(--mk-color-yellow)'>processes in a blocked state</span>.
### Process Table & Control Block

![[Process Table & Control Block Illustration.png|center]]

The <span style='color:var(--mk-color-turquoise)'>process control block</span> (*PCB or process table entry*) contains its <span style='color:var(--mk-color-yellow)'>entire executing context</span>. The **PID**, will tell us <span style='color:var(--mk-color-yellow)'>where the PCB is</span>.

These PCB's are <span style='color:var(--mk-color-yellow)'>maintained by the kernel</span> and stored in a table representing all processes.

> [!danger] Issues with this
> **Scalability** - How many concurrent processes can you have
> **Efficiency** - The OS requires memory as well and should use limited space to allow more processes
# Process Interaction With OS
---
## System Calls

Most **OSs provides an application program interface** (*API*) to allow <span style='color:var(--mk-color-yellow)'>programs to access services</span> in the kernel (*Interact with hardware*).

> [!warning] This is not a function call
> A system call is <b><mark style='background:var(--mk-color-red)'>not a normal function call</mark></b> as it has to <span style='color:var(--mk-color-yellow)'>change from user to kernel mode</span>.
### Making System Calls

In <span style='color:var(--mk-color-purple)'>C / C++</span>, a system call can be <span style='color:var(--mk-color-orange)'>invoked almost directly</span> through:
- **Function wrappers** - A library which <span style='color:var(--mk-color-yellow)'>offers the same name and parameters</span> as the system call
- **Function adapter** - Functions which augments the input and does the system call (*like* `printf()`)

![[System Call Mechanism.svg|center|450]]
## Exception & Interrupt

### Exceptions

When **executing machine level instruction** it can cause <span style='color:var(--mk-color-red)'>exceptions</span>:
- **Arithmetic errors** - Overflows, underflows, division by 0
- **Memory errors** - Illegal memory address, mis-alignment memory access (*Bus error, access instruction not from addresses not divisible by 4*)

> [!info] Exceptions are synchronous
> An exception in synchronous as these exceptions occur <span style='color:var(--mk-color-yellow)'>due to an instruction execution</span>.

The OS will have <span style='color:var(--mk-color-yellow)'>its own exception handler</span>, which acts similar to a forced function call.
### Interrupt

Unlike exceptions, an interrupt occurs from <span style='color:var(--mk-color-yellow)'>external events</span> which <span style='color:var(--mk-color-red)'>interrupts the execution of the program</span>.

In the CPU there are <span style='color:var(--mk-color-turquoise)'>interrupt request lines</span> (*hardware*) which <span style='color:var(--mk-color-yellow)'>connects to hardware</span> (*each hardware has its own interrupt request line*).

> [!info] Interrupts are asynchronous
> Hardware is <span style='color:var(--mk-color-yellow)'>independent from instruction execution </span>. When hardware does something it will alter one of these interrupt request lines.

When an **interrupt occurs**, the program execution is suspended and the **CPU will see which interrupt line was triggered** and <span style='color:var(--mk-color-yellow)'>execute the appropriate interrupt handler</span> (*There is a interrupt vector / table to loop up which one to call*).

> [!tldr] Execution flow during exception / interrupt
> When either occurs, **control will be transferred** to a <span style='color:var(--mk-color-turquoise)'>handler routine</span> <span style='color:var(--mk-color-yellow)'>automatically</span> and it will do the following:
> 1) **Save** registers / CPU state
> 2) **Perform necessary tasks**
> 3) **Restore** registers / CPU state
> 4) Return from interrupt (*Changes the request line from high to low*)
>    
> It **needs to save registers** because the <span style='color:var(--mk-color-yellow)'>function can continue executing</span> and may behave as if nothing happen.
# Process Abstraction in Unix
---
In Unix, a process will contain the following:
**Identification**
- PID (*Process ID, an integer value*)
**Information**
- Process State (*PS*):
	- Running, Sleeping, Stopped, **Zombie**
- Parent PID
	- PID of the parent process
- Cumulative CPU time
	- Total amount of CPU time used so far (*decide to run or not run by the scheduler*)
- etc
## Process Creation

We can use `fork()` to **create a new process**. It will <span style='color:var(--mk-color-orange)'>return</span> either:
- **PID** for the newly created process (*parent processes*)
- **0** for <span style='color:var(--mk-color-yellow)'>child processes</span>

We also **require these 2 header files**, `#include <unistd.h>` and `#include <sys/types.h>`.

> [!question] How to find the correct header files?
> <span style='color:var(--mk-color-orange)'>These are system dependent</span> and you might need to do `man <function name>` to get the right files.

> [!info] Child Process
> `fork()` creates a child process which is a <span style='color:var(--mk-color-yellow)'>duplicate of the current executable image</span> (*remainder of the code*).
> 
> It is **identical** even the <b><mark style='background:var(--mk-color-yellow)'>data in the child process the same</mark></b> as the parent.
> 
> Only when the <span style='color:var(--mk-color-yellow)'>data is changed then it will make a copy</span> of it (*copy-on-write or cow*).
> 
> It only <span style='color:var(--mk-color-orange)'>differs</span> in:
> - Process ID
> - Parent ID (*PPID*)
> - `fork()` return value

After creating a new process, both the parent and child process will <span style='color:var(--mk-color-yellow)'>continue executing after</span> the `fork()` call.

> [!question] How to make the child & parent do something different?
> By just doing `fork()` both the parent and child process will <span style='color:var(--mk-color-red)'>do the same thing which is not useful</span>.
> 
> We can make use of the return value from `fork()` for the <span style='color:var(--mk-color-green)'>child process will carry out some work</span> while the <span style='color:var(--mk-color-green)'>parent does something else</span>, using `if else` statements.
## Master Process

There is a <span style='color:var(--mk-color-orange)'>root process</span> and it is called `init`. It is the <span style='color:var(--mk-color-yellow)'>first process created in the kernel</span> during boot up. And it traditionally has a PID of 1, which **processes fork from it and then call exec** 

> [!note] Purpose of `init`
> `init` will `fork` some of the <span style='color:var(--mk-color-yellow)'>important processes</span> (*like `login`, `inetd`*). It will then <span style='color:var(--mk-color-yellow)'>watch over other processes and respawn them when needed</span> (*when an important processes dies & not all will be respawned*).
## Executing An Existing Program

An issue with `fork` is that we need to <span style='color:var(--mk-color-red)'>provide full code for the child process</span>. Instead we can use `execl()` (*or many of its variants*) and <span style='color:var(--mk-color-yellow)'>execute another existing program</span>.

> [!note] `Main` in C
> In <span style='color:var(--mk-color-purple)'>C</span>, `main` takes in 2 arguments, `argc` which is the <span style='color:var(--mk-color-yellow)'>number of variables</span> passed into `main` and `argv`, which is an <span style='color:var(--mk-color-yellow)'>array containing the variables</span>. 
> 
> And `main` is called by the OS.

We can use `execl()` to replace the current executing process image <span style='color:var(--mk-color-yellow)'>with a new one</span>. And we will need the `#include <unistd.h>` header file.

It has some <span style='color:var(--mk-color-orange)'>parameters</span>:
`int excel (const char *path, const char *arg0, .... const char *argN, NULL)`
- `path` - Is the **location** of the executable
- `arg0` - Is the **executable name**
- `arg1` to `argN` - **Arguments** to pass in which <b><mark style='background:var(--mk-color-yellow)'>must end with a NULL</mark></b>
## Termination

When the <span style='color:var(--mk-color-orange)'>process wants to terminate</span> it can use the `exit()` function. And we will need the `#include <stdlib.h>` header file. Usually `exit` is implicitly called (*like in main when we return 0*).

This function takes in 1 argument `status`:
- **0** means <span style='color:var(--mk-color-green)'>normal termination</span> (*successful execution*)
- **Anything other than 1** means it indicates a <span style='color:var(--mk-color-red)'>problematic execution</span>

> This function <span style='color:var(--mk-color-yellow)'>does not return</span>

**Majority** of the process resources are **freed on termination**. However <span style='color:var(--mk-color-orange)'>some are not releasable</span>:
- **PID**
- **Status** from `exit()` (*for parent-children synchronization*)
- **Process accounting information** (*CPU usage time*)
## Parent-Child Synchronization

We can make the parent process <span style='color:var(--mk-color-yellow)'>wait for the child process to terminate</span> using the `wait()` function. We will need the `#include <sys/types.h>` and `#include <sys/wait.h>` header files.

There is also <span style='color:var(--mk-color-orange)'>other versions</span> of `wait` such as `waitpid()` & `waitid()`.

This function takes in 1 argument `status` and it will return:
- **PID** of the <span style='color:var(--mk-color-yellow)'>terminated child process</span>
- And if `status` is not `NULL`, it will <span style='color:var(--mk-color-yellow)'>return the status</span> returned by `exit`

> [!note] Blocking
> `wait` is <span style='color:var(--mk-color-turquoise)'>blocking</span>, which means the <span style='color:var(--mk-color-yellow)'>parent process is blocked until 1 child terminates</span>.
### Zombies

Zombies are **process which have terminated** but its <span style='color:var(--mk-color-red)'>PCB is still in the process table</span>. The reason this still **lingers** is because we <span style='color:var(--mk-color-yellow)'>might needs to pass information from the child to the parent</span>.

> [!important] Killing zombies
> Unlike `exit()`, `wait()` will <b><mark style='background:var(--mk-color-yellow)'>remove the process control block from the table</mark></b>, cleaning up space.

It is possible that the **parent processes terminates before the child**, in which case `init` becomes the <span style='color:var(--mk-color-yellow)'>"pseudo" parent</span>. Once the child terminates it will send a signal to `init` which will call `wait` to cleanup.

> [!fail] Issues if we do not kill these zombie processes
> This will cause the <span style='color:var(--mk-color-red)'>process table to fill up</span>, <span style='color:var(--mk-color-red)'>not allowing you to create new processes</span>.
> 
> > For older versions of Unix you need to reboot to clear this table
