---
title: Virtual Memory Management
Date Created: 2025-03-23
Last Updated: 2025-09-28
tags:
  - CS2106
  - Memory
---
# Virtual Memory
---
Previously when managing memory there were [[Memory Management#Contiguous Memory Allocation|2 assumptions]]. Now we will <span style='color:var(--mk-color-orange)'>remove both of these assumptions</span>.

A big problem is that the previous schemes, if the **logical memory of a process is way larger than physical memory** then we will <b><span style='color:var(--mk-color-red)'>not be able to run it</span></b>.

Why not **use secondary storage or disk** storages which are <b><span style='color:var(--mk-color-green)'>larger</span></b> than physical memory capacity. Chunks which **cannot be stored** in physical memory will be <b><span style='color:var(--mk-color-yellow)'>stored on secondary storage</span></b>.

> [!info] Virtual Memory Space
> It is the illusion that we have more memory than we actually have. As virtual memory is just a <b><span style='color:var(--mk-color-yellow)'>part of disk acting as an extension of RAM</span></b>.
> 
> This part of the disk is also known as a <b><span style='color:var(--mk-color-turquoise)'>swap space</span></b> and the frames are known as <b><span style='color:var(--mk-color-turquoise)'>swap pages</span></b>

A popular approach to this will be to extend the [[Disjoint Memory Allocation#Paging|paging scheme]].

> [!abstract] Typically its slow to read from disk thus some programing languages have a buffer to store read/write
> It is <b><span style='color:var(--mk-color-green)'>a lot faster to do 1 large read/write operation</span></b> than many smaller read write operations.
## Extending the Paging Scheme

We will use the same concept but now we need to **identify if the page is in physical memory or secondary storage**, thus we need to use a additional bit called the <b><span style='color:var(--mk-color-turquoise)'>memory resident bit</span></b>. This will be in the page table.

> [!note] When we say memory resident it means the page is in physical memory

If a CPU access a non-memory resident page it results in a <b><span style='color:var(--mk-color-red)'>page fault</span></b>. This requires the physical frame to be <b><span style='color:var(--mk-color-yellow)'>pulled from secondary storage & load it to physical memory</span></b> by the OS, before the CPU can access it.

> [!danger] Trashing
> We know that <b><span style='color:var(--mk-color-green)'>accessing physical memory is a lot faster</span></b> than accessing memory in secondary storage.
> 
> However when a <b><span style='color:var(--mk-color-red)'>page fault commonly occurs it will result in trashing</span></b> (*Using more time to access secondary memory*).

We need to <span style='color:var(--mk-color-orange)'>undertstand 3 concepts</span> in virtual memory:
1) **Page table structures**: Efficient structure because if large logical memory space
2) **Page replacement algorithms**: Which page should be replaced when needed
3) **Frame allocation policies**: Limited physical memory frames how can we distribute evenly
### Locality

In caching it is most likely the <b><span style='color:var(--mk-color-yellow)'>instructions and data fetched will be used again</span></b> when brought in **blocks**.

> [!note] Locality Principles
> **Temporal locality** (*Time*)
> > Memory address (*page*) which is used <b><span style='color:var(--mk-color-yellow)'>is likely to be used again</span></b>.
> 
> **Spatial locality** (*Space*)
> > Memory addresses <b><span style='color:var(--mk-color-yellow)'>close to a used address is likely to be used</span></b>. Page contains contiguous locations.
### Demand Paging

We need to decide if a new process comes in does everything need to be in physical memory? We want to <b><span style='color:var(--mk-color-yellow)'>put as many processes to be memory resident</span></b>.

A simple idea is **no process starts on physical memory**, only <b><span style='color:var(--mk-color-yellow)'>load it when there is a page fault</span></b>.

> [!success] Advantages of demand paging
> - **Fast startup time for new process** (*no need to decide what should go to physical memory*)
> - **Small memory footprint**

> [!failure] Disadvantages of demand paging
> - **Processes may appear sluggish** at the start because of multiple page faults
> - The **faults may have cascading effects on other processes** (*cause other pages to be removed from physical memory*)
# Page Table Structures
---
The page take information takes up physical memory. In modern computer systems they **provide huge logical memory space**.

> [!fail] Problems with huge page tables
> - **High overhead**
> - **Fragmented page table**: It occupies several memory pages

In **direct paging** just <b><span style='color:var(--mk-color-yellow)'>keep all entries in a single table</span></b>. If we have P bits then we can have $2^{P}$ pages in logical memory space.

However it can be <b><span style='color:var(--mk-color-red)'>wasteful</span></b> as **not all processes will use the entire virtual memory space**.
## 2-Level Paging

The idea is to <b><span style='color:var(--mk-color-yellow)'>spilt the page table into regions</span></b>. Only some regions are used and new regions can be allocated if memory grows.

> [!example] Example of 2-level paging
> For example if our virtual address has 32 bits & 1 page is 4Kib = $2^{12}$ and 1 entry takes up 4 bytes ($2^{2}$).
> 
> Then for 2 level paging, 1 page can hold $2^{12} / 2^{2}=2^{10}$ entries. Thus the remaining bits we have left are $32 - 10 - 12 = 10$ since we need 10 bits to find the entry and the last 12 bits for the offset within the page.
> 
> This we will have $2^{10}$ page tables in our page directory and this we only need $2^{10} * 2^{2} = 2^{12}$ bytes of storage

Thus now we need a <b><span style='color:var(--mk-color-turquoise)'>page directory</span></b> to keep track of the smaller page tables. And we can repeatedly add more levels if needed.

![[2-Level Paging Example.png|center|500]]


> [!success] Advantages of 2-level paging
> It <b><span style='color:var(--mk-color-green)'>saves a lot of space</span></b> (*uses a lot less*) as compared to direct paging.
## Inverted Page Table

Here we have a single <b><span style='color:var(--mk-color-yellow)'>mapping of physical frame to the process id and the page number</span></b>. We just need to **know what is inside physical memory**.

![[Inverted Page Table Example.png|center]]

> The page table will have the <b><span style='color:var(--mk-color-yellow)'>same number of entries as the number of physical frames</span></b>.

> [!success] Advantages of inverted page table
> <b><span style='color:var(--mk-color-green)'>Huge savings</span></b>, one table for all processes. Even better than 2-level paging.
> 
> <b><span style='color:var(--mk-color-green)'>Faster updating</span></b> of the page table.

> [!fail] Disadvantages of inverted page table
> <b><span style='color:var(--mk-color-red)'>Slow translation</span></b>. Now the table is mapped to the physical frame. Meaning we need to search the whole table to find what we are looking for.
# Page Replacement Algorithms
---
When the **table is full**, we <b><span style='color:var(--mk-color-yellow)'>need to remove something to make space</span></b> for something new.

Before swapping out we need to **know if the page is clean or not**:
- **Clean page**: When the page has <b><span style='color:var(--mk-color-yellow)'>not been modified</span></b> and thus no need to write back
- **Dirty page**: When the page has <b><span style='color:var(--mk-color-yellow)'>been modified</span></b> and thus it need to be written back

There are many algorithms and some of them are:
- Optimum (*OPT*)
- FIFO
- Least recently used
- Second chance (*clock*)

**Memory references are often modeled** as <b><span style='color:var(--mk-color-turquoise)'>memory reference strings</span></b>, which is just a sequence of page numbers.

We can **evaluate the performance** of the algorithm through the <b><span style='color:var(--mk-color-yellow)'>memory access time</span></b>.
$$
T_{\text{access}} = (1 - P) \times T_{\text{mem}} + P \times  T_{\text{page fault}}
$$
**Where**:
- $P$ is the probability of a page fault
- $T_{\text{mem}}$ is the access time for memory resident page
- $T_{\text{page fault}}$ is the access time if a page fault occurs

Aim to <b><span style='color:var(--mk-color-green)'>keep the probability low</span></b> since <b><span style='color:var(--mk-color-red)'>access time when a page fault occurs is costly</span></b>.
## Optimal Page Replacement (OPT)

The idea is to **replace the page** what will <b><span style='color:var(--mk-color-yellow)'>not be used again for the longest period of time</span></b>. This <b><span style='color:var(--mk-color-green)'>guarantees minimum number of page faults</span></b>.

![[Optimal Page Replacement Example.png|center|400]]

However the main issue is that we <b><span style='color:var(--mk-color-red)'>need to know future memory refences</span></b>.

> [!note] Usefulness of OPT
> OPT is proven to be the best algorithm however because of the constraint its not practical.
> 
> This is used as a <b><span style='color:var(--mk-color-yellow)'>base comparison for other algorithms</span></b>. The **closer an algorithm is to OPT the better the algorithm**.
## First In First Out

It is very simple we will <b><span style='color:var(--mk-color-yellow)'>evict the pages which have been loaded in first</span></b>.

It is very <b><span style='color:var(--mk-color-green)'>simple to implement</span></b>. <b><span style='color:var(--mk-color-green)'>No hardware support needed</span></b>, the **OS** will just need a <b><span style='color:var(--mk-color-blue)'>queue</span></b> of the loaded pages.

![[First In First Out Example.png|center|400]]


> [!failure] Problems with first in first out
> It has <b><span style='color:var(--mk-color-red)'>no understanding of temporal locality</span></b> (*newly loaded in frames might be used frequently in the next few moments*).


> [!info] Belady's anomaly
> Even if we **increase the frames** (*how many is loaded into physical memory*) it does <b><span style='color:var(--mk-color-yellow)'>not guarantee less page faults</span></b>, it can increase. This is known as <b><span style='color:var(--mk-color-turquoise)'>Belady's anomaly</span></b>.
## Last Recently Used

We will address the issues with [[Virtual Memory Management#First In First Out|FIFO]] by <b><span style='color:var(--mk-color-yellow)'>making use of temporal locality</span></b>. We will replace the pages that were not used in the longest time

Attempts to <b><span style='color:var(--mk-color-yellow)'>approximate the OPT</span></b> algorithm, generally good results. And it does <b><span style='color:var(--mk-color-green)'>not suffer from Belady's anomaly</span></b>.

![[Last Recently Used Example.png|center|400]]

> [!important] When we access memory that is already loaded we need to update the last used

However it is <b><span style='color:var(--mk-color-red)'>not easy to implement</span></b> LRU as we need hardware support.
### Implementing LRU

We need to **keep track of the last access time**, thus we need <b><span style='color:var(--mk-color-yellow)'>substantial hardware support</span></b>.
#### Use a Counter

We will have a **counter that increments per time** unit and if there is **a memory reference** we will <b><span style='color:var(--mk-color-yellow)'>store the value as a entry in the page table</span></b> (*time of use*).

We will then <b><span style='color:var(--mk-color-yellow)'>replace the page with the smallest time</span></b>.

> [!failure] Problems with using a counter
> - When replacing, we need to search through all pages
> - It is possible for an **integer overflow** since the timer is increasing forever
#### Use a "Stack"

It is not really a stack. But when a **page gets referenced and is in the stack** it gets <b><span style='color:var(--mk-color-yellow)'>removed</span></b> (*wherever it is inside*) and <b><span style='color:var(--mk-color-yellow)'>placed at the top of the stack</span></b>.

If the **page is not in the stack**, then we can <b><span style='color:var(--mk-color-yellow)'>remove the bottom most entry</span></b> (*least used*). Thus <b><span style='color:var(--mk-color-green)'>no need to search through all entries</span></b>.

> [!failure] Problems with using a stack
> - It is not a pure stack, entries can be removed from any where in the stack thus we still need to look through all entries
> - Hard to implement in hardware

## Second-Change Page Replacement

Also known as the <b><span style='color:var(--mk-color-turquoise)'>CLOCK algorithm</span></b>. Similar to [[Virtual Memory Management#First In First Out|FIFO]], however each page table entry will have a **reference bit**:
- If it is **1** it has <b><span style='color:var(--mk-color-yellow)'>been accessed</span></b>
- If it is **0** it has <b><span style='color:var(--mk-color-yellow)'>not been accessed</span></b>.

When we want to replace a frame, we will start at the front (*queue*) but now we **check if the reference bit**:
- If it is **0** then we will <b><span style='color:var(--mk-color-yellow)'>remove that page table entry</span></b> and <b><mark style='background:var(--mk-color-yellow)'>set the reference bit to 0</mark></b> (*not 1*)
- If it is **1** then <b><span style='color:var(--mk-color-yellow)'>set the reference bit to 0</span></b> and **go to the next page table entry** (*next in queue*) and repeat

> [!important] If everything is 1 then it degenerates into FIFO.

> [!success] This is easier to impliment

![[Second-Change Page Replacement Example.png|center|400]]

> [!important] Notice the pointer does not reset after each replacement or memory reference
# Frame Allocation
---
If we have $N$ physical memory frames and $M$ processes <span style='color:var(--mk-color-orange)'>2 simple approaches</span> will be:
1) **Equal allocation**: Each process will get $N/M$ frames
2) **Proportional allocation**: Take the size of the process divide by the total and then times $N$

We want to **minimise trashing** as it is <b><span style='color:var(--mk-color-red)'>expensive</span></b> (*heavy I/O*) to bring non-resident pages into RAM. And it is difficult to find the right number of frames.
## Frame Replacement Strategies
### Local Replacement

The **algorithms covered** above are doing <b><span style='color:var(--mk-color-turquoise)'>local replacement</span></b>. Where only <b><span style='color:var(--mk-color-yellow)'>frames of that process gets replaced</span></b>.

> [!success] Advantages of local replacement
> The **frames allocated remain constant** thus the <b><span style='color:var(--mk-color-green)'>performance is stable</span></b> between multiple runs (*Get the same frames per run*).

> [!failure] Disadvantages of local replacement
> If the allocated frames is not enough, it will <b><span style='color:var(--mk-color-red)'>hinder the progress of the process</span></b>.
> 
> **Trashing can be limited to 1 process** but it can <b><span style='color:var(--mk-color-red)'>hog I/O and degrades performance</span></b> of other processes.
### Global Replacement

Here a process can <b><span style='color:var(--mk-color-yellow)'>take a frame from another process</span></b>.

> [!success] Advantages of global replacement
> It allows for <b><span style='color:var(--mk-color-green)'>self-adjustment between processes</span></b>. If a process needs more frames it can get from other processes.

> [!failure] Disadvantages of global replacement
> Processes can take advantage by <b><span style='color:var(--mk-color-red)'>getting all the frames from other processes</span></b> (*affecting others*). This also <b><span style='color:var(--mk-color-red)'>causes cascading thrashing</span></b>, where it cause other processes to thrash
> 
> **Frames allocated can differ** from run to run, thus <b><span style='color:var(--mk-color-red)'>performance can be inconsistent</span></b>.
## Finding the Right Number of Frames

The <b><span style='color:var(--mk-color-yellow)'>set of pages referenced by a process is relatively constant</span></b> in a period of time. Known as **locality**.

However, as **time passes**, the <b><span style='color:var(--mk-color-yellow)'>set of pages can change</span></b>. Thus the <b><span style='color:var(--mk-color-turquoise)'>working set model</span></b> (*$\Delta$*), which defines an interval of time (*used in modern machines*).

We denote $W(t, \Delta)$ as the <b><span style='color:var(--mk-color-yellow)'>active pages in the interval at time</span></b> $t$. We want to allocate enough frames in the working set to reduce the possibility of page faults.

![[Working Set Model Visualisation Over Time.png|center]]

if we **set the interval** ($\Delta$) to be:
- **Too small** then we might <b><span style='color:var(--mk-color-red)'>miss pages</span></b> in the current locality
- **Too large** then it may <b><span style='color:var(--mk-color-red)'>contain pages from a different locality</span></b> and will <b><span style='color:var(--mk-color-red)'>prevent other processes to utilize the CPU</span></b>.

![[Working Set Example.png|center]]

> Here $\Delta = 5$, the set at $t1 = \{1, 2, 5, 6, 7\}$ while at $t2 = \{3, 4\}$

