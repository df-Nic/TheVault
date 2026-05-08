---
title: Inter-Process Communication
Date Created: 2025-02-15
Last Updated: 2025-09-28
tags:
  - CS2106
  - IPC
  - Processes
---
# IPC
---
One issue is that it is <span style='color:var(--mk-color-red)'>difficult to share information</span> as <span style='color:var(--mk-color-yellow)'>memory space is independent</span>. For example a global variable will be independent of the processes after `fork()`.

There are **2 common IPC mechanisms**:
- **Shared-memory**
- **Message passing**

There are **2 Unix-specific IPC mechanisms**:
- **Pipe**
- **Signal**
## Shared Memory

![[IPC Shared Memory Example.png|center|400]]

The **creation and attachment** of the shared memory region is all <span style='color:var(--mk-color-yellow)'>system calls</span>.

Basic **steps to use** shared memory:
1) Create a shared memory `M`, using `shmid = shmget( IPC_PRIVATE, 40, IPC_CREAT | 0600);`
2) Attach `M` to a process, using `shm = (int*) shmat( shmid, NULL, 0 );`
3) Read / write to `M`
4) Detach `M` from process after use
5) **Destroy** `M` if not it will still use up memory and only <span style='color:var(--mk-color-yellow)'>1 process needs to do this</span> when there is <b><mark style='background:var(--mk-color-yellow)'>no other process attached</mark></b> to it.

> [!info] Advantages & disadvantages of shared-memory
> > [!success] Advantages
> > - **Efficient**: The <span style='color:var(--mk-color-green)'>only OS calls are when creating and attaching</span>, the rest are just pointer operations
> > - **Easy to use**
>
> > [!failure] Disadvantages
> > - **Synchronization**: We <span style='color:var(--mk-color-red)'>cannot wait for another process</span> to update something before continuing.
## Message Passing

We need to <span style='color:var(--mk-color-orange)'>figure out a few things</span>:
1) **Naming**: How to identify the other party
2) **Synchronization**: Behavior of sending / receiving operations

Within the **OS**, there will be a <span style='color:var(--mk-color-yellow)'>region of memory for communication</span> (*message passing*). This means, **sending and receiving** are <span style='color:var(--mk-color-red)'>all kernel calls and this are slow</span>.

> [!note] Naming schemes
> 1) **Direct naming scheme**
> > **Sender** will <span style='color:var(--mk-color-yellow)'>indicate the sender</span>, and the **receiver** will <span style='color:var(--mk-color-yellow)'>specify who the sender</span> is.
> 2) **Mailbox scheme**
> > Each process will have a **mailbox** (*or port*), then any <span style='color:var(--mk-color-yellow)'>process will send the message to this mailbox</span>. The receiver will just need to check the mailbox and <span style='color:var(--mk-color-yellow)'>no need to specify the process</span>.

> [!note] Synchronization mechanisms
> 1) **Synchronous** (*Blocking*)
> >The sender <span style='color:var(--mk-color-yellow)'>needs to wait</span> for the receiver to respond before sending the message (*Both process will block if the other party is not ready, like a phone call*).
>
> 2) **Asynchronous** (*Non-blocking*)
> > The sender can <span style='color:var(--mk-color-yellow)'>send anytime</span> and the receiver can <span style='color:var(--mk-color-yellow)'>receive anytime</span> (*No need to wait, like a text message*).

> [!info] Advantages & disadvantages of message-passing
> > [!success] Advantages
> > - **Portable**: Can be <span style='color:var(--mk-color-green)'>created in a library</span> and use it in any OS
> > - **Easy synchronization**: Synchronous mechanism
>
> > [!failure] Disadvantages
> > - **Inefficient**: If every send and receive is a <span style='color:var(--mk-color-red)'>kernel call</span>
> > - **Hard to use**: Have to use send and receive instead of using pointer operations
# Unix Pipes
---
 **Each process will have 3 standard files**:
1) `stdin` or standard in: <span style='color:var(--mk-color-yellow)'>Default input for the process</span> and usually it is connected to the keyboard
2) `stderr` or standard error: Use for <span style='color:var(--mk-color-yellow)'>printing error message</span>, and <span style='color:var(--mk-color-red)'>cannot be redirected to a file</span>
3) `stdout` or standard out: What ever is written to the standard out file will be <span style='color:var(--mk-color-yellow)'>printed on the screen</span> or <span style='color:var(--mk-color-yellow)'>to another file</span>

In <span style='color:var(--mk-color-purple)'>Unix</span>, we can **pipe an standard out into a standard in** by using the `|` symbol. 

We can think of **pipes** as a <span style='color:var(--mk-color-yellow)'>communication channel</span>, and this pipe will have a <span style='color:var(--mk-color-yellow)'>writing end and a reading end</span> and it is <span style='color:var(--mk-color-yellow)'>a file</span>.

> [!note] Pipes are character oriented
> Pipes will <span style='color:var(--mk-color-yellow)'>read and write character by character</span>.

**Pipe functions** as <span style='color:var(--mk-color-yellow)'>circular bounded byte buffer</span> with <span style='color:var(--mk-color-yellow)'>implicit synchronization</span>:
- Writers wait when buffer is full
- Readers wait when buffer is empty

> [!example] Example C code to create a pipe
> ```C
> int main() {
> 	int pipeFd[2], pid, len; // Create a array of 2 integers, index 0 to read and index 1 to write
> 	pipe( pipeFd ); // It creates a file descriptor which tells where to read / write
> 	if ((pid = fork()) > 0) { // parent
> 		close( pipeFd[READ_END] ); // Close the reading end before writing
> 		write( pipeFd[WRITE_END], str, strlen(str)+1 ); // +1 because we need to write the null terminator
> 		close( pipeFd[WRITE_END] ); // Close the writing end and writing
> 	} else { //child process
> 		close( pipeFd[WRITE_END] ); // Close the writing end before reading
> 		len = read( pipeFd[READ_END], buf, sizeof (buf) ); // Need a buffer to write to and the size of it
> 		printf("Proc %d read: %s\n", pid, buf);
> 		close( pipeFd[READ_END] ); // Close the reading end after reading
> 	}
> }
> ```
> We need to **close the opposite end** because when we close the end, <span style='color:var(--mk-color-yellow)'>it will send a signal</span> so they can do what they need to do.

The above example shows 1 variant which is known as <span style='color:var(--mk-color-turquoise)'>half-duplex</span> (*unidirectional*). There is another variant known as <span style='color:var(--mk-color-turquoise)'>full-duplex</span> (*bidirectional*), where <span style='color:var(--mk-color-yellow)'>any end can be for reading or writing</span>.

> [!note] Piping from 1 application to another
> We will connect the **writing end** to `stdout` and the **reading end** to `stdin`. If not we will be <span style='color:var(--mk-color-red)'>reading from the keyboard and writing to the screen</span>.

# Unix Signal
---
A **signal is a form of IPC** which is <span style='color:var(--mk-color-yellow)'>asynchronous</span> regarding an event (*exceptions or errors*), for example `SIGINT`, when we do ctrl + c.

These <span style='color:var(--mk-color-yellow)'>signals will need to be handled</span> by either:
- Using default set of handlers
- Use your own handlers (*for some signals, example SIGKILL cannot be chought*)

> [!example] Example code to make your own handler
> ```C 
> void myOwnHandler( int signo ) { // Must be a return of void and 1 integer argument
> 	if (signo == SIGSEGV) { // A signal is some integer and SIGSEGV is a segmentation fault
> 		printf("Memory access blows up!\n");
> 		exit(1);
> 	}
> }
> int main(){
> 	int *ip = NULL; // Pointing to null means address 0
> 	// Signal is a function to catch a signal and pass to your handler and see if the assignment of the signal is successful
> 	if (signal(SIGSEGV, myOwnHandler) == SIG_ERR) 
> 		printf("Failed to register handler\n");
> 	*ip = 123;
> 	return 0;
> }
> ```
