---
title: Instruction Set Architecture
Date Created: 2024-02-11
tags:
  - CS2100
  - ComputerLanguage
  - Hardware
---
# 5 ISA Design Concepts
---
## Data Storage

The purpose of this concept is to <mark style='background:#fa8231'>determine where to get the data</mark>.

Before determining the storage, a <span style='color:#0fb9b1'>storage architecture</span> needs to be defined. A familiar architecture is the **general purpose register architecture** used by <span style='color:#8854d0'>MIPS</span>. 

These <span style='color:#0fb9b1'>storage architecture</span> defines :
- Where to store operands
- Where to store the result
- How to specify operands

Now given a instruction `a = b + c`, there are 3 operands and 1 operator, and these <span style='color:#f7b731'>operands can be implicit or explicit </span>(Registers).
### Common Data Storage Architectures

- **Stack Architecture**
>Just like the <span style='color:#3867d6'>stack data structure </span>, <span style='color:#f7b731'>operands</span> are implicitly at the <span style='color:#f7b731'>top of the stack</span>.

- **Accumulator Architecture**
>A special register called the <span style='color:#0fb9b1'>accumulator</span> <span style='color:#f7b731'>implicitly stores one operand</span>. It will always store a copy of the value inside it.

- **General-purpose register architecture** (**GPR**)
>There are 2 sub classes, <span style='color:#0fb9b1'>register-memory</span> and <span style='color:#0fb9b1'>register-register</span> (**load-store**) architecture, which only handles <span style='color:#f7b731'>explicit operands</span>.

- **Memory-memory architecture**
>All operands are in <span style='color:#f7b731'>stored in memory</span>.

Out of the 4, **GPR** is the most common choice : 
- **RISC** (Reduced Instruction Set Computer) typically use <span style='color:#0fb9b1'>load-store</span> design because it <span style='color:#20bf6b'>simplifies hardware design</span> and it <span style='color:#20bf6b'>balances the pipeline</span>, which is an optimisation to performance
- **CISC** (Complex Instruction Set Computer) uses a mixture of <span style='color:#0fb9b1'>register-register</span> and <span style='color:#0fb9b1'>register-memory</span>
<div style="page-break-after: always;"></div>
## Memory Address Modes

The purpose of this concept is to <mark style='background:#fa8231'>determine how to get data from memory</mark>.

Recall that each memory slot stored 1 byte and given a k-bit address, the total space will be $2^{k}$ starting from 0 till $2^{k} - 1$.

In the **CPU**, there are 2 special registers :
- <span style='color:#0fb9b1'>Memory address register</span> (MAR), <span style='color:#f7b731'>stores the address</span> the processor needs to read and write from. It is connected to a k-bit <span style='color:#f7b731'>address BUS</span> which is <mark style='background:#f7b731'>unidirectional</mark>
- <span style='color:#0fb9b1'>Memory data register</span> (MDR), <span style='color:#f7b731'>stores the data</span> read from memory or to be written into memory. It is connected to a n-bit <span style='color:#f7b731'>data BUS</span> which is <mark style='background:#f7b731'>bidirectional</mark>

Besides the BUS, there is also a <span style='color:#0fb9b1'>control line</span> that <span style='color:#f7b731'>determines</span> if the access to memory is a <span style='color:#f7b731'>read or write access</span>.

There are the types of addressing modes :
1) **Register mode**, operands are represented as registers
2) **Immediate Mode**, one of the operands will be a register and the other a immediate / constant
3) **Displacement Mode**, operand is in memory and its address is calculated as a base address in a register + some offset
4) **Register indirect**, the operand will be a register with its <span style='color:#f7b731'>effective address</span>
5) **Indexed / Base**, similar to displacement mode, but the <span style='color:#f7b731'>offset will be in a register</span>
6) **Direct or absolute**, the <span style='color:#f7b731'>address</span> will be an <span style='color:#f7b731'>immediate</span> operand
7) **Memory indirect**, where the <span style='color:#f7b731'>register points to another address</span>
8) **Auto-increment**, the register will contain some address, then after reading, the <span style='color:#f7b731'>address will be incremented</span>
9) **Auto-decrement**, similar to auto-decrement, but instead of being incremented it will be <span style='color:#f7b731'>decremented</span>
10) **Scaled**, to get the effective address, it will be the <span style='color:#f7b731'>offset + base + index * scaling factor</span>
### Endianness

It is the <span style='color:#fa8231'>relative ordering</span> of the bytes stored in memory.

There are 2 types of endianness :
1) <span style='color:#0fb9b1'>Big-endian</span> - Store the <mark style='background:#f7b731'>MSB first</mark> (Used by <span style='color:#8854d0'>MIPS</span>)
2) <span style='color:#0fb9b1'>Little-endian</span> - Store the <mark style='background:#f7b731'>LSB first</mark>

![[Endianness Example.png|center|250]]

For <span style='color:#0fb9b1'>little-endian</span>, there is <mark style='background:#f7b731'>no need to swap the order</mark> of the bytes.
## Operations in the Instruction Set

The purpose of this concept is to <mark style='background:#fa8231'>determine the types of operations supported by the processor</mark>.

Firstly, <span style='color:#f7b731'>define all the frequently used instructions</span>, this will enable<span style='color:#20bf6b'> better optimisation</span> in hardware during implementation.

This is because, knowing what instructions is frequently used, if it can be optimised then these instructions will run better.

**Standard Operations**
![[ISA Standard Operations.png|center|350]]
## Instruction Formats

The purpose of this concept is to <mark style='background:#fa8231'>determine the types of instruction formats</mark>.

There are 2 things to consider :
1) **Length of instruction**

It can be <span style='color:#0fb9b1'>variable-length</span> which is mainly used in <span style='color:#8854d0'>CISC</span> and requires <span style='color:#f7b731'>multi-step fetch and decode</span>, as it depends an initial value which will load the next segment. This approach is more <span style='color:#20bf6b'>flexible and compact instruction set</span> but it can be <span style='color:#eb3b5a'>complex</span>.

It can be <span style='color:#0fb9b1'>fixed-length</span> which is mainly used in <span style='color:#8854d0'>RISC</span> and allows <span style='color:#f7b731'>easy fetch and decode</span>. This approach <span style='color:#20bf6b'>simplifies pipelining and parallelism and is easy to handle</span> but the <span style='color:#eb3b5a'>instruction bits are scarce and is less flexible</span>. 

For 64 bit instructions like <span style='color:#8854d0'>ARM</span>, either load all 64 bits or segregate into 2 32 bits segment. These are called <span style='color:#0fb9b1'>very long instruction word</span> architecture (VLIW).

There is also a <span style='color:#0fb9b1'>hybrid instructions</span>, which consist of the 2 but it is rarely used.

2) **Instruction fields (Type & Size of Operands)**

It consist of :
1) `opcode`, which is a <span style='color:#f7b731'>unique code</span> to specify a operations
2) `operands`, how many additional information needed (Can be 0)
<div style="page-break-after: always;"></div>

**Typical types & sizes**
- Character (8 bits)
- Word (4 Bytes), Half-word (2 Bytes)
- Single-precision floating point (1 Word)
- Double-precision floating point (2 Words)

For a <span style='color:#fa8231'>32-bit architecture</span>, it must support, 8, 16, 32 bit integers and 32, 64 bit floating point operations (By using 2 32 bit registers). For a <span style='color:#fa8231'>64-bit architecture</span>, it is the same as before but it include 64 bit integers.
## Encoding the Instruction Set

The purpose of this concept is to <mark style='background:#fa8231'>determine how instructions are converted into binary bits</mark>.

When encoding instructions, compromises which needs to be made between, <span style='color:#f7b731'>code size, performance and complexity</span>. For example, with <span style='color:#20bf6b'>more simple instructions</span>, <span style='color:#eb3b5a'>program size will increase</span>.

**Things to Decide**
- Number of Registers (If there are $n$ registers how many bits are required)
- Number of addressing modes (More addressing nodes, more complex processor)
- Number of operands in an instructions

**Competing Forces**
- Number of registers and addressing nodes
- How to reduce code size
- Have instruction lengths which are easy to handle (Fixed length is easier to handle)

This results in  <span style='color:#fa8231'>3 types of encoding choices</span>, [[#Instruction Formats|variable, fixed ad hybrid]].
### Fixed Length Instruction Encoding

A challenge with this is how to<span style='color:#f7b731'> fit multiple instructions</span> into a <span style='color:#eb3b5a'>limited amount of bits</span>. The solution is to <span style='color:#f7b731'>work with the most constrained instruction types first</span>. Which leads to the <span style='color:#0fb9b1'>expanding opcode scheme</span>.

![[Fixed Length Instruction Encoding.png|center|450]]

The example above shows how to maximise one type, but what about <span style='color:#fa8231'>minimising</span>. Then just do the opposite, which is to <mark style='background:#f7b731'>maximise opcode with the least number of bits</mark>.

When designing an encoding architecture, start from the <mark style='background:#f7b731'>most restrictive case</mark> (Case with the smallest number of instructions).