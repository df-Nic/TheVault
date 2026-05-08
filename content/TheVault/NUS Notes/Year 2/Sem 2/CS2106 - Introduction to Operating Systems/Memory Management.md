---
title: Memory Management
Date Created: 2025-03-06
Last Updated: 2025-09-28
tags:
  - CS2106
  - Memory
---
# Basics of Memory
---
We have many <span style='color:var(--mk-color-orange)'>types of memory</span>, ordering **from fastest to slowest** we have:
1) CPU registers
2) Cache
3) RAM (*random access memory*)
4) Hard disk
5) Off-line storage (*tape drivers*)

When talking about memory we will be **focusing on RAM**.

> [!abstract] Random Access Memory
> [[Sequential Logic & Memory#Memory Cell|RAM]] can be seen as <b><span style='color:var(--mk-color-yellow)'>an array of bytes</span></b> (*1 byte has 8 bits*) and each byte has a **unique index** known as a <b><span style='color:var(--mk-color-turquoise)'>physical address</span></b>.
> 
> RAM is a <b><span style='color:var(--mk-color-yellow)'>contiguous memory region</span></b>, **each address is next to each other**. 

We learn that a program will be stored in memory into [[Process Abstraction|different segments]]. We need to know **where in memory** is it stored and weather the **size will change or not** (*code does not change but data does*).

> [!info] Types of data
> 1) **Transient**
> > They are local data or data that are created (`malloc`) and freed
> 2) **Persistent** 
> > More for global variables
> 
> We need to know that no matter what type data will <b><mark style='background:var(--mk-color-yellow)'>not be constant it can grow or shrink in size</mark></b>. 

The OS handles a lot of memory related tasks such as:
- **Allocate** memory for processes
- **Manage** memory space for processes (*all our multithreading and concurrencies and context switches*)
- **Protect** memory space from other processes (*segmentation fault*)
- **System calls** for processes
- **Internal usage** of memory for the OS

> [!important] Fragmentation
> Fragmentation is an event that occurs when allocating memory and there are <span style='color:var(--mk-color-orange)'>2 types</span>:
> 1) **Internal** fragmentation: Is when in a <b><span style='color:var(--mk-color-yellow)'>partition or block of memory it is not fully utilised</span></b> by the process
> 2) **External** fragmentation: After <b><span style='color:var(--mk-color-yellow)'>allocating chunks of memory, there will be holes</span></b> in the whole memory location.

**Memory conversion**

| Prefix   | Abbreviation | Power of 2 | Exact Conversion in Bytes                       |
| -------- | ------------ | ---------- | ----------------------------------------------- |
| **Kibi** | KiB          | 2¹⁰        | 1 KiB = 1,024 bytes                             |
| **Mebi** | MiB          | 2²⁰        | 1 MiB = 1,048,576 bytes                         |
| **Gibi** | GiB          | 2³⁰        | 1 GiB = 1,073,741,824 bytes                     |
| **Tebi** | TiB          | 2⁴⁰        | 1 TiB = 1,099,511,627,776 bytes                 |
| **Pebi** | PiB          | 2⁵⁰        | 1 PiB = 1,125,899,906,842,624 bytes             |
| **Exbi** | EiB          | 2⁶⁰        | 1 EiB = 1,152,921,504,606,846,976 bytes         |
| **Zebi** | ZiB          | 2⁷⁰        | 1 ZiB = 1,180,591,620,717,411,303,424 bytes     |
| **Yobi** | YiB          | 2⁸⁰        | 1 YiB = 1,208,925,819,614,629,174,706,176 bytes |

**Binary Base:** These prefixes use powers of 2 because computer memory and storage are organized in binary.

**Usage:***
-  KiB, MiB, GiB, etc.** are used in computer memory (RAM) and sometimes storage.
- **They are different from decimal-based prefixes** (*kilo, mega, etc*.), where 1 KB = 1,000 bytes instead of 1,024.

# Memory Abstraction
---
## Without Memory Abstractions

**Without abstractions**, a process can <b><span style='color:var(--mk-color-yellow)'>directly use the physical address</span></b>, for instance, this process will use this address and so on.

> [!success] No need for any management of memory
> We are using the physical address, we can directly put it in memory.

> [!failure] Overlapping memory
> What if 2 processes use the same memory location. Then we will <b><span style='color:var(--mk-color-yellow)'>need some kind of memory switching</span></b>.
### Process Relocation

We can simply fix this <b><span style='color:var(--mk-color-red)'>issue of overlapping memory</span></b> by <b><span style='color:var(--mk-color-yellow)'>reallocating memory into the next available space</span></b> (*address reallocation*). However this means that **every address in the process** will need to <b><span style='color:var(--mk-color-yellow)'>offset by a certain amount</span></b>.

> [!failure] Problems with address relocation
> - **Slow loading times**, as we need to <b><span style='color:var(--mk-color-yellow)'>recompute all address with an offset</span></b>
> - **Not easy to distinguish** memory reference from a normal integer constant
## Using Memory Abstractions
### Base + Limit Registers

Instead of changing the entire instruction to be offset by some amount we can instead just ask it to <b><span style='color:var(--mk-color-yellow)'>retrieve an offset from a register</span></b>. This address inside the program instruction is a **logical address**, and it needs a the <b><span style='color:var(--mk-color-yellow)'>offset to map to the physical address</span></b>.

> [!summary] Logical Addresses
> The idea of a program <b><span style='color:var(--mk-color-red)'>using a physical address is a bad idea</span></b>. It will be <b><span style='color:var(--mk-color-green)'>better if it uses a logical address</span></b> which is <b><span style='color:var(--mk-color-yellow)'>how the process views its memory space</span></b>.
> 
> Each process will have its own self-contained, independent logical memory space. And it <b><span style='color:var(--mk-color-yellow)'>requires some mapping</span></b> between logical and physical addresses.

![[Base + Limit Registers Example.png|center]]

> [!info] Base address
> Where the **program starts** and this will be our <b><span style='color:var(--mk-color-yellow)'>offset</span></b>.
> 
> > So if our program starts at address 8000 then our base address is 8000.

> [!info] Base register
> A register to <b><span style='color:var(--mk-color-yellow)'>store the base address</span></b>.

Now we need to **protect the process from being accessed** by other processes. This is known as a <b><span style='color:var(--mk-color-turquoise)'>limit address</span></b>.

> [!info] Limit address / register
> It is essentially how long or the <b><span style='color:var(--mk-color-yellow)'>last address used by the process</span></b>.
> 
> Thus if this processes were to **access a address that is smaller than the base or larger than the limit**, a <b><span style='color:var(--mk-color-red)'>segmentation fault will happen</span></b>.

> [!failure] Additional computation
> Essentially we need to ensure that the `Actual = base + offset` <b><span style='color:var(--mk-color-yellow)'>must be smaller than </span></b> `Limit`.
> 
> Thus we will <b><span style='color:var(--mk-color-red)'>incur a addition and a comparison</span></b> for each memory access.

This idea of offset is very **useful** as:
- It can be <b><span style='color:var(--mk-color-yellow)'>generalised for segmentation mechanisms</span></b>
- Provides a <b><span style='color:var(--mk-color-yellow)'>crude memory abstraction</span></b>
	> Where 2 similar **physical address** are different for the 2 processes
# Contiguous Memory Allocation
---
A process must be in memory during execution:
- **Store memory** concept
- **Load-store memory** execution model

Some **assumptions** to take note of is that:
- Each memory occupies a <b><span style='color:var(--mk-color-yellow)'>contiguous memory region</span></b> (*boarders one another*)
- The physical memory is large enough to **contain more than 1 process** with <b><span style='color:var(--mk-color-yellow)'>complete memory space</span></b> (*it can load everything into memory not partially*).

If we want to **support multitasking**, <b><span style='color:var(--mk-color-yellow)'>multiple processes must be in physical memory at the same time</span></b> for switching.

If at any time the <b><span style='color:var(--mk-color-red)'>physical memory is full</span></b>, we can do the following:
1) Remove terminated processes
2) Swap blocked processes to secondary storage (*disk storage*)
## Memory Partition

The physical memory region can be <b><span style='color:var(--mk-color-yellow)'>dissected into different contiguous partitions</span></b>. And there are **2 types of allocation schemes**.
### Fixed-Sized Partition

 The physical memory is spilt into a <b><span style='color:var(--mk-color-yellow)'>fixed number of partitions</span></b> and the <b><span style='color:var(--mk-color-yellow)'>process will occupy a partition</span></b>. This is known as a <b><span style='color:var(--mk-color-turquoise)'>physical frame</span></b>.

![[Fixed-Sized Partition Example.png|center|400]]

We **only need to know which partition is free and which is not**.

> [!success] Advantages of fixed-sized partitioning
> - It is **easy to manage** as we need to know which partition is available
> - It is **fast to allocate**, since every partition is the same size

 > [!failure] Disadvantages of fixed-sized partitioning
 > - We need to make sure that the **partition size is large enough for the biggest process**
 > - There will be **wasted memory space if the process is smaller than the partition size**, this is known as <b><span style='color:var(--mk-color-pink)'>internal fragmentation</span></b>
### Variable-Sized Partition

Also known as <span style='color:var(--mk-color-turquoise)'>dynamic partitioning</span>. Each <b><span style='color:var(--mk-color-yellow)'>partition is based on the actual size of the process</span></b>. The **OS will need to keep track of memory** by performing splitting and merging when necessary.

![[Variable-Sized Partition Example.png|center|400]]

As for the scenario above, there can be a lot of [[Process Abstraction#Dynamically Allocated Memory|holes]] in memory because of **creating, termination or swapping of processes** and thus we <b><span style='color:var(--mk-color-yellow)'>need to merge</span></b> these so that it can <b><span style='color:var(--mk-color-green)'>accommodate more processes</span></b>.

<b><span style='color:var(--mk-color-yellow)'>Where the process is allocated is up to the OS</span></b>. From the example above if a small process can fit into any of the 2 free memory locations, it can go in any it just depends on the OS.

 > [!success] Advantages of variable-sized partitioning
 > - It is **flexible** and it can **remove internal fragmentation** by merging
 
 > [!failure] Disadvantages of variable-sized partitioning
 > - **Harder to maintain** as the OS will need more information about memory
 > - It is **time consuming to allocate** a proper region as we need to know how big the processes is, do we have the memory available, do we need to merge free memory etc.
### Dynamic Allocation Algorithms

If we have a process of size n then all we need to do is find a hole that is big enough. There are <span style='color:var(--mk-color-orange)'>several variants</span>:
- **First-fit**: Take the first hole that is large enough (*fast, but potentially not efficient memory usage*)
- **Best-fit**: Take the smallest hole that is large enough (*good memory usage. but is slower*)
- **Worst-fit**: Take the largest hole (*is not bad is just it is slow as we need to manage fragmentation by merging*)

The **OS** will need to **know the partitions used and the size of the holes**. Once a hole has been found it will be <b><span style='color:var(--mk-color-yellow)'>spilt into used and left over space</span></b> (*new hole*).

![[Example of how the OS Records Holes.png|center]]

**While allocating memory** the OS will need to <span style='color:var(--mk-color-orange)'>do 2 important tasks</span> which is to **merge** & **compact**, since <b><span style='color:var(--mk-color-yellow)'>storing of processes needs to be contiguous</span></b>.

> [!info] Merging
> When a occupied **partition is freed**, it will <b><span style='color:var(--mk-color-yellow)'>merge with adjacent holes</span></b> if possible.

> [!info] Compaction
> **Move occupied partitions** around to <b><span style='color:var(--mk-color-yellow)'>create consolidated holes</span></b>.
> 
> This however cannot be invoked too frequently as it is <b><span style='color:var(--mk-color-red)'>time consuming</span></b> (*expensive, no real work is done*).

The **simplest way** of allocating memory is to <b><span style='color:var(--mk-color-yellow)'>keep track of where is free and where is occupied</span></b> (*using a linked list*).

**When a processes needs memory**
- Check all holes
- If a hole is big enough, mark the space that is occupied
- The remaining space will remained free

**When a processes finishes**
- The space that was marked as occupied will then be relabelled as free

> [!failure] Issues with this simple method
> - It is **time consuming**, as time goes we will have <b><span style='color:var(--mk-color-yellow)'>more pockets of information</span></b> of where if free or occupied
> - Blocks are **not evenly spaced out**, thus the time taken to <b><span style='color:var(--mk-color-yellow)'>find a suitable hole can take time</span></b>.
> 
#### Buddy System

It is a better algorithm to allocate memory. Essentially a <b><span style='color:var(--mk-color-yellow)'>free space will divide itself into half repeatedly</span></b> until it just meets the process requirements.

![[Buddy System Example.png|center|400]]

When splitting, the 2 halves form <b><span style='color:var(--mk-color-turquoise)'>sibling blocks</span></b> (*buddy blocks*). When **both are free**, they will be <b><span style='color:var(--mk-color-yellow)'>merged</span></b> into a bigger block.

> [!important] Internal fragmentation of 50% or higher is impossible
> Lets say we want to allocate 8 bytes or 128. If we were to have < 50% internal fragmentation we will use a block of 512.
> 
> However, from the algorithm we will allocate to a block with $2^{8}$ instead of $2^{9}$ because we can spilt it further into smaller blocks.

> [!success] Advantages of buddy system
> - More **efficient partition splitting**
> - Better **memory allocation**
> - More **efficient de-allocation and coalescing**

We can implement this through an **array of size k** where all of available memory is $2^{k}$. And `A[J]` is the free block of size $2^{J}$.

A block **can just be the starting address of the block in memory**, so if 0 is at index 5 means at address 0 to 0 + $2^{5}$ there is a free block.

Each block will be indicated by the <b><span style='color:var(--mk-color-yellow)'>starting address</span></b>. However take note that there might be **small block sizes** which are <b><span style='color:var(--mk-color-red)'>not cost effective to manage</span></b>.

**To allocate space**:
Assuming we have a process of size N
1) Find the <b><span style='color:var(--mk-color-yellow)'>smallest J</span></b> such that $2^{J} \ge N$ and $J \le K$ where **K is the largest power 2 which represents all of memory**
2) Now check if there is a free block at index $J$, there can be <span style='color:var(--mk-color-orange)'>2 scenarios</span>:
	1) At index $J$ **there is a free block**, then <b><span style='color:var(--mk-color-yellow)'>just remove the block</span></b> and <b><span style='color:var(--mk-color-yellow)'>assign the process</span></b> to that block
	2) If there is **no free block at index** $J$ then do the following:
		1) From $J + 1$ to $K$ find a available block.
		2) Once we find the block, <b><span style='color:var(--mk-color-yellow)'>repeatedly spilt the block</span></b> until its of size $J$ and assign it. Taking 1 half each spilt if we need to spilt further (*usually take the smaller starting address*)
		3) If we reach $K$ and there is no free block, then we <b><span style='color:var(--mk-color-red)'>cannot allocate</span></b>

**To deallocate the space**:
1) Find where the process is in memory
2) Set the space / partition to be free
3) If its a **buddy** then we <b><span style='color:var(--mk-color-yellow)'>can merge the 2 together to make a bigger sized block</span></b> and store it at index $J + 1$

> [!question] Who is my buddy?
> If we spilt a larger block into a smaller block, then <b><span style='color:var(--mk-color-yellow)'>one of its bits will be 1</span></b>.
> 
> Thus 2 blocks are buddy of size $2^{S}$ if, the <b><span style='color:var(--mk-color-yellow)'>S bit of B and C are a complement</span></b> (*one is 1 the other is 0*). In addition, the <b><span style='color:var(--mk-color-yellow)'>leading bits are all the same</span></b> (*the ones to the left*).
> 
> We can use use the XOR function based on the size of the block.
> 
> > [!example] Example
> > Assuming we have a big block $A$ of size 32 ($2^{5}$). After dividing we will have block B and C of size 16 ($2^{4}$).
> >
> > The starting address of B will be 0 or 000000 in binary, while for process C it will be 100000 in binary. We can see the **5th bit is complement of each other**.




