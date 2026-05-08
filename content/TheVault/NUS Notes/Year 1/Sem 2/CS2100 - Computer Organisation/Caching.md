---
title: Caching
Date Created: 2024-04-14
tags:
  - CS2100
  - Hardware
---
# Memory Technology
---
Here are a few types of <span style='color:#fa8231'>memory technology</span> :

| Memory Device | Capacity  |  Latency   | Cost / GB |
| :-----------: | :-------: | :--------: | :-------: |
|   Registers   | 100 Bytes |   20 ps    |    $$$    |
|     SRAM      |  100 KB   | 0.5 - 5 ns |    $$     |
|     DRAM      |  100 MB   | 50 - 70 ns |     $     |
|   Hard Disk   |  100 GB   | 5 - 20 ms  |   Cents   |
DRAM is also known as **DDR SDRAM** which stands for <span style='color:#0fb9b1'>double data rate synchronous dynamic ram</span>, which <span style='color:#f7b731'>delivers memory on the positive and negative edge</span> of a clock that is why it is called double rate.

The <span style='color:#fa8231'>ideal memory</span> is obviously, **high in capacity, low in latency and cheap**.

According to Moore's Law
> Number of transistors used roughly <span style='color:#f7b731'>doubles</span> every year

This causes a bottleneck between memory and the CPU as the CPU is getting faster and faster.

Remember that for byte conversion from byte to KB to MB to GB and so on is just multiples of 1024
# Caching
---
The idea of caching is to <span style='color:#f7b731'>minimise the amount of times to access memory</span> by <span style='color:#f7b731'>storing frequently and recently used data in smaller buy faster memory devices</span>.

This works because of the <span style='color:#0fb9b1'>principle of locality</span>
>Program accesses a small portion of memory address space within a small time interval

**Types of locality**
1) **Temporal Locality** (Time)
	 >Items reference will tend to be <span style='color:#f7b731'>referenced again</span>
2) **Spatial Locality** (Space)
	><span style='color:#f7b731'>Nearby items</span> to the item being reference will tend to be <span style='color:#f7b731'>referenced soon</span>
<div style="page-break-after: always;"></div>

To make slow main <span style='color:#fa8231'>memory appear faster</span> :
- **Add caches** (A small but fast SRAM near the CPU)
- **Manage the hardware** (Transparent to the programmer)

To make small main <span style='color:#fa8231'>memory appear larger</span> :
- Use **virtual memory**
- **OS managed** (Transparent to the programmer)

**Caching Terminology :**
1) <span style='color:#20bf6b'>Hit</span>, which is when data is in the cache
	- **Hit Rate** - In the long run, the fraction of memory access that hit
	- **Hit Time** - Time taken to access the cash
2) <span style='color:#eb3b5a'>Miss</span>, data is not in the cash and needs to be fetch from memory
	- **Miss Rate** - 1 minus the hit rate
	- **Miss Penalty** - Time taken to replace the cache block (Reading into cash will be in chunks) + hit time

The <span style='color:#0fb9b1'>average access time</span> can be calculated as such :
$$
\text{Average access time } = \text{Hit rate} \times \text{Hit time} + (1 - \text{Hit rate}) \times \text{Miss penalty}
$$
If data takes 1 word to store, a <span style='color:#0fb9b1'>cache block/line</span> is <span style='color:#f7b731'>typically larger in size</span>. In MIPS 1 word is 4 bytes, then a cache block can be 16-bytes long.

In MIPS a memory address is 32 bits, and given a $2^{N}$ byte <span style='color:#0fb9b1'>cache block</span>, all the memory address within this cache block :
- Have the same $32 - N$ MSB, meaning <span style='color:#f7b731'>Bits</span>$\color {#f7b731} {[31:N]}$ are <span style='color:#f7b731'>exactly the same</span> and this is called the <span style='color:#0fb9b1'>block number</span>
- The remaining <span style='color:#f7b731'>Bits</span>$\color {#f7b731} {[N - 1:0]}$ are called the <span style='color:#0fb9b1'>block offset</span> within the block

So why not <span style='color:#fa8231'>increase the cache block</span>, to <span style='color:#fa8231'>load in more data</span> :
- The <span style='color:#eb3b5a'>miss penalty will be higher</span>, more data is needed to be read from memory into cache, thus more time needed
- The larger the block the smaller the cache index, the larger the size the less blocks in cache, <span style='color:#eb3b5a'>increasing the miss rate</span>

The <span style='color:#fa8231'>best block size</span> is when the **average access time is at its minimum**.
<div style="page-break-after: always;"></div>

# Direct Mapped Cache
---
![[Direct Mapped Cache Example.png|center]]

In direct map caching, the <span style='color:#f7b731'>cache has</span> $\color {#f7b731} {2^{m}}$ <span style='color:#f7b731'>blocks</span>, where $m$ is the number of bits used. Remember that now the <b><mark style='background:#f7b731'>block number is used</mark></b> and not the address, so the last $m$ bits are the <span style='color:#0fb9b1'>cache index</span>.

If 2 bits is used then the number of cache blocks is $2^{2} = 4$ and a block number of $\dots10$ will go to slot 2. A simple formula for getting the cache index is just `Cache Index = Block Number % Number of Cache Blocks`. 

What about the unused bits on the left (N-m). Those bits are called the <span style='color:#0fb9b1'>tag number</span> and to get it is just `Tag number = Block Number / Number of Cache Blocks`.

This <span style='color:#f7b731'>tag number is unique</span> as it allows to <span style='color:#f7b731'>identify</span> which cache block is currently stored in the cache.

**In general** if the cache index uses $m$ bits and a cache block uses $n$ bits
- Size of 1 cache block is $2^{n}$ (Bytes)
- Number of cache index/blocks is $2^{m}$
- Offset is $n$
- Index is $m$
- Tag is $32 - (N + M)$ bits

Inside the cache, it will need another bit called `valid` to indicate weather the cache line contains valid data or not.
<div style="page-break-after: always;"></div>

**Example of how data is stored and pulled from cache**
![[How Data is Stored in Cache Using Direct Mapped Caching.png|center]]

Take note that <b><mark style='background:#f7b731'>1 block in memory must be the same as 1 block in cache</mark></b>.

The block offset depends on the number of words in the block, if 1 block has 2 words ($2^{1}$) then use the MSB only (Bit$[N:N-1]$).
## Writing of Data into Memory

When data is written into memory, there can be a <span style='color:#eb3b5a'>cache data mismatch</span>. However just changing in cache is not sufficient.

There are <span style='color:#fa8231'>2 ways to solve this issue</span> :
1) Write through cache
	><span style='color:#f7b731'>Write</span> data into both <span style='color:#f7b731'>cache and into main memory</span> which can be <span style='color:#eb3b5a'>slow</span>

A <span style='color:#fa8231'>solution</span> to this is to add a <span style='color:#f7b731'>write buffer</span> (Job queue). The processor will write into cache and <span style='color:#f7b731'>sends the data into the buffer where the memory controller will write</span> whatever is in the buffer, so that the processor can continue instead of waiting to write.

2) Write back cache
	><span style='color:#f7b731'>Write</span> data into cache first, only when <span style='color:#f7b731'>cache block is replaced</span> then write into memory, which can be <span style='color:#eb3b5a'>complicated</span>

It can be <span style='color:#eb3b5a'>wasteful to always write back when replaced</span>, one solution is to add a <span style='color:#0fb9b1'>dirty bit</span>, which just <span style='color:#f7b731'>indicates if there is any update to the cache data</span> or not. If there is then write into memory when replaced.
<div style="page-break-after: always;"></div>

## Types of Cache Misses

1) **Compulsory misses**
	>When the <span style='color:#f7b731'>block is first access</span>, the data must be brough into cache from memory this is also called cold miss or first reference misses (As long as the block was never loaded int cache before it is a cold miss).
2) **Conflict misses**
	>Occurs when <span style='color:#f7b731'>several cache blocks are mapped to the same index</span> in cache
3) **Capacity misses**
	>Occurs when <span style='color:#f7b731'>blocks are discarded from cache</span> as cache cannot contain all the blocks needed
## Handling Cache Misses

1) **Read misses**
	- Just load the data from memory into cache
2) **Write Misses**
	- Write allocate - Load the data into cache and write based on<span style='color:#0fb9b1'> write through</span> or <span style='color:#0fb9b1'>write back</span> policy
	- Write around - Don't load into memory but write directly into memory

# Set Associative Cache
---
This type of cache is one solution to the <span style='color:#0fb9b1'>conflict misses</span>. The idea is that currently only 1 block can be stored in 1 index but now with set associative cache, <span style='color:#f7b731'>more than 1 block can be stored in the same index</span>.

**N-way set associative cache**
>$n$ number of blocks in each set that can be stored

How to <span style='color:#fa8231'>get the number of sets</span> in the cache, remember that the number of cache blocks that can be stored is `Cache size / block size`

Now the <span style='color:#fa8231'>number of sets</span> given that it is a $N$-way is `Number of blocks / N`. So lets say the number of sets is $256 = 2^{8}$, then the <span style='color:#0fb9b1'>set index</span> requires 8 bits ($2^{m}$).

Thus for the set associative cache, the <span style='color:#f7b731'>cache index is replaced with the set index</span>. The rest of the calculations remain the same.
<div style="page-break-after: always;"></div>

**Example of a set associative cache**
![[Set Associative Cache Diagram.png|center]]

A rule of thumb, a direct mapped cache of size $N$ has the <span style='color:#f7b731'>same miss rate</span> as a 2-way associative cache size of $N/2$.

# Fully Associated Cache
---
The idea now is that instead of having a designated slot for the cache block, just<span style='color:#f7b731'> insert it anywhere in the cache with an empty slot</span>.

The advantage is that it is <span style='color:#20bf6b'>not restricted by the index or set index</span> but the downside is that <span style='color:#eb3b5a'>all blocks have to be searched</span>. Therefore this is only useful for small cache sizes.

Since the index is not needed, then the <span style='color:#f7b731'>full block number will be the tag</span>.
<div style="page-break-after: always;"></div>

**Example of a fully associated cache**
![[Fully Associated Cache Diagram.png|center]]

# Block Replacement Policy
---
With set and fully associated cache, <span style='color:#f7b731'>there is a choice on which block to be removed</span> in order for new data to be stored.

A policy is needed to determine which on to be removed and one of them is called the <span style='color:#0fb9b1'>least recently used</span> (**LRU**) policy.

It is a basically a <span style='color:#f7b731'>data structure that keeps track on which block is called recently</span>, can imagine as a queue, any block called will be bumped to the back of the queue. The one at the front is the least used.

One drawback however is that it can be <span style='color:#eb3b5a'>hard to keep track</span>, there are other policies such as :
- First in first out (**FIFO**)
- Random Replacement (**RR**)
- Least frequent used (**LFU**)
<div style="page-break-after: always;"></div>

# Multilevel Caching
---
Each type of memory hardware has its own level and thus it can be combined to create a workflow for the processor

**Example of multilevel caching**
![[Multilevel Caching Diagram.png|center]]