---
title: Disjoint Memory Allocation
Date Created: 2025-03-14
Last Updated: 2025-09-28
tags:
  - CS2106
  - Memory
---
Previously when managing memory there were [[Memory Management#Contiguous Memory Allocation|2 assumptions]]. Now we will <span style='color:var(--mk-color-orange)'>remove one of these assumptions</span> which is that **each process occupies a contiguous memory region**.
# Paging
---
The idea of paging is to <b><span style='color:var(--mk-color-yellow)'>spilt the program into regions of the same size</span></b> (*spilt the logical memory of the process*). This is known as a <b><span style='color:var(--mk-color-turquoise)'>logical page</span></b>.

These regions can be <b><span style='color:var(--mk-color-yellow)'>loaded into any available memory frame</span></b>. Thus the physical **memory region can be disjoint** but the logical memory space remains contiguous.

The <b><span style='color:var(--mk-color-yellow)'>mapping of the logical page and the physical frame is no longer simple</span></b>, we will need some sort of **lookup table** and this is known as a <b><span style='color:var(--mk-color-turquoise)'>page table</span></b>.

> [!important] Design decisions
> - Keep the frame & page sizes to be of some <b><span style='color:var(--mk-color-yellow)'>power of 2</span></b>
> - The physical frame size is the <b><span style='color:var(--mk-color-yellow)'>same</span></b> as logical page size

Thus our **physical address** will be:
$$
\text{Frame number} \times \text{size of physical frame } + \text{Offset} 
$$
**Example with 4 logical pages & 8 physical frames**
![[Paging Example.png|center]]

With paging, it allows several process to <b><span style='color:var(--mk-color-yellow)'>share the same physical memory frame</span></b> (*page sharing*), this can happen when:
- Programs share the same code page (*libraries, system calls*)
- Implement copy on write (*parent & child process can share a page unit until one tries to write*)

> [!success] Advantages of paging
> - There will be <b><span style='color:var(--mk-color-green)'>no external fragmentation</span></b>. Because the <b><span style='color:var(--mk-color-yellow)'>page size is the same as the physical frame size</span></b>
> - It allows for great flexibility
> - Simple address translation

> [!failure] Disadvantages of paging
> Only for the **last allocated physical frame**, there <b><span style='color:var(--mk-color-red)'>might be internal fragmentation</span></b>.
> 
> Lets say our process takes 23 bytes and the logical page is of 4 bytes, the the last page will have 3 bytes meaning the assigned physical frame will have 1 free byte.
## Implementing the Paging Scheme

One common **pure-software** solution is to <b><span style='color:var(--mk-color-yellow)'>store the page table in the PCB</span></b>, since its part of the memory context of a process.

However this means it will <b><span style='color:var(--mk-color-red)'>require 2 memory accesses for every reference</span></b>. One to the page table and the other to the physical memory.
### Hardware Support

The modern processors provide a <b><span style='color:var(--mk-color-turquoise)'>translation look-aside buffer</span></b> (*TLB, which is a cache for page tables*). It is a <b><span style='color:var(--mk-color-yellow)'>cache</span></b> of a few page table entries.

And in [[Caching|caching]]there will be a **hit and a miss**:
- If an entry is **found** it is called a <b><span style='color:var(--mk-color-green)'>TLB-Hit</span></b>. The frame can be retrieved to generate the physical address
- If the entry is **not found** it is called a <b><span style='color:var(--mk-color-red)'>TLB-Miss</span></b>, it needs to access the page table and the physical frame from memory as well as updating the TLB

**Example of using a TLB**
![[TLB Example.png|center]]

> [!important] TLB context switching
> The **TLB will contain information on 1 process**. It we context switch to another process, the <b><span style='color:var(--mk-color-yellow)'>TLB will need to be swapped</span></b>. This is part of the **hardware context**.
> 
> We can also indicate certain PID's to tell the OS to not remove them. Thus allowing multiple processes to still stay inside TLB.

### Page Sharing

We can allow several processes to **share the same physical memory frame**, but just <b><span style='color:var(--mk-color-yellow)'>using the same addresses</span></b>.

We can also **implement copy on write**, until a <b><span style='color:var(--mk-color-yellow)'>process edits a page it will then make a duplicate</span></b>.
### Protection

Now we do not have a way to prevent other processes from accessing other programs data since the memory is not contiguous. Usually in the <b><span style='color:var(--mk-color-yellow)'>frame number there will be additional bits for protection handled by the OS</span></b>.

One way is to use <b><span style='color:var(--mk-color-turquoise)'>access-right bits</span></b>. Each page table entry has **writable, readable executable bits** which will be checked against when accessing memory.

Another way is to use a <b><span style='color:var(--mk-color-turquoise)'>valid bit</span></b>. Since <b><span style='color:var(--mk-color-yellow)'>not all processes will utilize the whole logical memory range</span></b>. Thus the OS will set valid bits when a process is running. Any access to memory will be checked against this bit and any out-of-range access will be caught by the OS.
# Segmentation Scheme
---
The memory context of a process has [[Process Abstraction#Memory Context|4 different segments]]. And some regions like the heap grows and shrink at execution.

Thus in a segmentation scheme, the **logical memory space** will be <b><span style='color:var(--mk-color-yellow)'>spilt into these 4 segments</span></b> and it will <b><span style='color:var(--mk-color-yellow)'>store a collection of the corresponding segments</span></b>.

![[Segmentation Scheme Example.png|center]]
Each segment must <span style='color:var(--mk-color-orange)'>contain</span>:
1) **Name** of the segment (*Segment ID*)
2) **Limit** to denote the end of the segment (*or the size of the segment*)

Thus now **all memory reference** will be the <b><span style='color:var(--mk-color-yellow)'>segment name</span></b> (*Segment ID*) and some <b><span style='color:var(--mk-color-yellow)'>offset</span></b> from the starting address of the segment.

We can <b><span style='color:var(--mk-color-yellow)'>simply store in a table</span></b>, the base the limit for each segment.

> [!example] Segmentation Scheme Example
> A process will have a logical address of `<SegID, Offset>` it will use the segment ID to get the limit + base
> It will check if the limit is greater than the offset. If it is then it will compute the physical address of $Base + Offset$

**Getting the data from memory**
![[Retrieving Information Using Segmentation Scheme.png|center]]


> [!success] Advantages of Segmentation Scheme
> Each segment is an independent contiguous memory space, meaning it can
> - **Grow and shrink independently**
> - **Protected and shared independently**

> [!fail] Disadvantages of Segmentation Scheme
> Since the segments requires variable-sized contiguous memory regions it can <b><span style='color:var(--mk-color-red)'>cause external fragmentation</span></b>.

# Merging Segmentation With Paging
---
In the our <b><span style='color:var(--mk-color-yellow)'>physical memory will be spilt into pages</span></b> as per paging scheme. But our process will be spilt into segments and <b><span style='color:var(--mk-color-yellow)'>each segment will be broken down into pages</span></b>.

So now <b><span style='color:var(--mk-color-yellow)'>each segment will have its own page table</span></b>. Which we need to check if the page is in the table (*Page limit*).

![[Segmentation & Paging Scheme Example.png|center]]

> [!fail] Disadvantages of merging the 2
> It is just <b><span style='color:var(--mk-color-red)'>computationally more expensive</span></b> as there is more things to lookup and compare.
