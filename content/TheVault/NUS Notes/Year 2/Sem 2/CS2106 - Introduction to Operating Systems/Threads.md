---
title: Threads
Date Created: 2025-02-11
Last Updated: 2025-09-28
tags:
  - CS2106
  - Processes
  - Concurrency
---
# Why use Threads?
---
**Processes** are <span style='color:var(--mk-color-red)'>expensive</span>. When we do `fork()`, it [[Process Abstraction#Process Creation|duplicates]] the <span style='color:var(--mk-color-yellow)'>memory space & process context</span> (*Not entirely true for memory space*). There is also a <span style='color:var(--mk-color-yellow)'>need to do context switching</span>.

There is <span style='color:var(--mk-color-red)'>no possible way to communicate between processes</span>. Since <span style='color:var(--mk-color-yellow)'>each process has its own memory space</span> there is no easy way to pass information. And we have to **make use of inter-process communication** (*IPC*) to solve this issue.

> [!note] Basic idea of threads
> Every process has a **single thread of control** (*one instruction stream only*). Thus with **multiple threads** we can have <span style='color:var(--mk-color-yellow)'>multiple instruction streams</span> (*execute different parts of the program concurrently*).

> [!example] Multi-threading example
> ![[Multi-threading Example.png|center|500]]
> 
> Now with <span style='color:var(--mk-color-yellow)'>3 threads 1 process can do 3 things at a time</span> and if we were to `fork()` this process, the 2 processes can now do 6 things at a time.
> 
> **Without multi-threading**, we will be <span style='color:var(--mk-color-red)'>forking 3 processes each only doing 1 thing</span>.

Thus with multiple threads we can <span style='color:var(--mk-color-orange)'>share information with other threads</span>, but what <span style='color:var(--mk-color-green)'>can we share</span>?:
- **Memory context** (*Text, data, heap*)
- **OS context**

What can we <span style='color:var(--mk-color-red)'>not share</span>?:
- **Thread ID**: This is unique for each thread
- **Registers**: Instructions for each thread will use the registers differently
- **Stack**: Technically in <span style='color:var(--mk-color-yellow)'>practice it is sharing the same stack</span>, but you can segment the stack to each thread

Therefore in **context switching between threads** only <span style='color:var(--mk-color-yellow)'>involves the hardware context</span>. Thus threads are lighter process and are called <span style='color:var(--mk-color-turquoise)'>lightweight process</span>.

> [!info] Advantages & disadvantages to threads
> > [!success] Advantages
> > - **Economy**: No need to duplicate memory as much as processes
> > - **Resource sharing**: Can share resources with one another without an additional mechanism
> > - **Responsiveness**: More responsive than processes
> > - **Scalability**: It can take advantage of multiple CPUs
>
> > [!failure] Disadvantages
> > - **System call concurrency**: There might be a case where it <span style='color:var(--mk-color-red)'>causes an re-entrancy problem</span> or <span style='color:var(--mk-color-red)'>not thread safe</span>
> >
> > > [!info] Re-entrancy problem
> > > For instance if 2 threads A & B modifies a static variable, then just when A uses the static variable, it switches to thread <span style='color:var(--mk-color-yellow)'>B and it modifies the value</span>. This will cause <span style='color:var(--mk-color-yellow)'>thread A to operate on the wrong value</span>.
> >
> > - **Process behaviour**: Certain <span style='color:var(--mk-color-red)'>functions can cause undesirable outcomes</span>. Like `exit()` it kills the process but what about the other threads. For `exec()` will it replace the instructions in other threads.
# Thread Models
---
There are 2 types of thread implementation, <span style='color:var(--mk-color-turquoise)'>user</span> and <span style='color:var(--mk-color-turquoise)'>kernel threads</span>.

> [!abstract] User Thread
> They are <span style='color:var(--mk-color-yellow)'>implemented as a user library</span> and is **managed** by a <span style='color:var(--mk-color-yellow)'>runtime system</span> in the process.
> 
> > [!success] Advantages of user threads
> > - Can have <span style='color:var(--mk-color-green)'>multithreaded programs on any OS</span>, even it they do not support it.
> > - They are **just library calls** (*function calls*), no need to switch to kernel mode.
> > - More <span style='color:var(--mk-color-green)'>configurable and flexible</span>
> 
> > [!failure] Disadvantage of user threads
> > - The OS is **not aware of the threads**, and thus the OS will <span style='color:var(--mk-color-red)'>schedule at a process level</span>. If the thread is blocked then the **whole process is blocked**
> > - It <span style='color:var(--mk-color-red)'>cannot use multiple CPUs</span>, the OS will schedule the process not the threads.

> [!abstract] Kernel Thread
> They are <span style='color:var(--mk-color-yellow)'>implemented by the OS</span> and is **handled** as <span style='color:var(--mk-color-yellow)'>system calls</span>. The **scheduling** is done by the <span style='color:var(--mk-color-yellow)'>kernel</span>.
> 
> The kernel can also <span style='color:var(--mk-color-yellow)'>use it for its own executions</span>, making the **kernel multi-threaded**.
> 
>  > [!success] Advantages of kernel threads
> > - They can now <span style='color:var(--mk-color-green)'>schedule on a thread level</span>. Different threads can use multiple CPUs
> 
> > [!failure] Disadvantage of kernel threads
> > - **Thread operations** are all **system calls** which is <span style='color:var(--mk-color-red)'>slower & more resource intensive</span>.
> > - They are also <span style='color:var(--mk-color-red)'>less flexible</span> (*less customisable*), as they are used in other processes as well.

We can **combine the 2** to have a <span style='color:var(--mk-color-turquoise)'>hybrid thread model</span>. Where the <span style='color:var(--mk-color-yellow)'>OS schedules the kernel threads</span> only, while the <span style='color:var(--mk-color-yellow)'>user threads binds to a kernel thread</span>.

> [!success] Advantages of using a hybrid thread model
> The <span style='color:var(--mk-color-green)'>kernel thread can schedule user threads</span>.
> 
> There is also the <span style='color:var(--mk-color-green)'>flexibility of switching between user threads in the user mode</span>. **No need to switch to kernel mode** which is expensive.
> 
> We can also <span style='color:var(--mk-color-green)'>limit the concurrency</span> by assigning these user threads to a specific kernel thread.

> [!info] Simultaneous multi-threading
> In the past threads were a user space library, then it becomes an OS mechanism, and now it is a hardware component. It has **many sets of registers, FP, SP, and many more**.
# POSIX Threads
---
This is one of the many **thread API**. One of these libraries is `pthread`. Defined by IEEE and supported by most Unix variants.

`pthread` however only **shows the interface** not the implementation, thus it can be <span style='color:var(--mk-color-yellow)'>implemented as a kernel or user thread</span>.

> [!note] Basics of `pthread`
> The **header file** is, `#include <pthread.h>`
> 
> To **compile** we need to add in `-lpthread`, for example `gcc xxx.c -lpthread`
> 
> Some useful **datatypes**:
> - `pthread_t`: Is a data type to represent a **thread id** (*TID*)
> - `pthread_attr`: Data type to represent **attributes of a thread**
## Creating a Thread

We can use the function `pthread_create` to **create a new thread**. It will return <span style='color:var(--mk-color-green)'>0 to indicate the thread is created successfully</span>, anything other than that is a failure.

It also takes in **4 arguments**:
- `*tidCreated`: The structure to store the tread ID. Can be empty as its already assigned
- `*threadAttributes`: Use `NULL` for the default attributes, but this is for the behaviour of the thread
- `*startRoutine`: Function pointer to the function to be executed by the thread
- `*argForStartRoutine`: Arguments to be passed into the thread

> [!note] `void *`
> It is a arbitrary pointer, if we <span style='color:var(--mk-color-yellow)'>do not know the type of the pointer type</span>, we can use `void*` and type cast it later
## Terminating a Thread

We can **terminate a thread** by using the function `pthread_exit`. We can do not call this function, but `pthread` will **automatically terminate** at the end of `startRoutine`.

There is only 1 argument `exitValue`, which can be `NULL`. The value to be <span style='color:var(--mk-color-yellow)'>retuned to whoever synchronize with this thread</span>.

And to **sync with another thread** we will use `pthread_join(pthread_t threadID, void ** status)`. Where `status` is a address variable to store the exit value of the target thread.