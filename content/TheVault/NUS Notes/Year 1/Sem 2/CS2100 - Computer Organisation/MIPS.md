---
title: MIPS
Date Created: 2024-02-03
tags:
  - CS2100
  - MIPS
  - ComputerLanguage
  - Hardware
---
# Instruction Set Architecture
---
Before beginning, <span style='color:#0fb9b1'>MIPS</span> stands for **microprocessor without interlocked pipelined stages**.

<span style='color:#fa8231'>Process</span> on how a computer understands a program :

Write programs on various languages $\rightarrow$ <span style='color:#0fb9b1'>Compiler</span> translate it into <span style='color:#f7b731'>MIPS language</span> $\rightarrow$ <span style='color:#0fb9b1'>Assembler</span> translates <span style='color:#8854d0'>assembly</span> language into <span style='color:#f7b731'>machine language instructions</span> for the processor (MIPS)

An <span style='color:#0fb9b1'>Instruction Set Architecture</span> (**ISA**) is a form of abstraction on the <span style='color:#f7b731'>interface between hardware and software</span>. Think of it as a <span style='color:#f7b731'>set of instructions which a processor can support</span>.
- Includes everything programmers need to know how the machine code is processed
- Allows the computer (CPU) designers to talk about functions independently from hardware that perform them

Thus if a program is compiled for a certain **ISA**, then <span style='color:#f7b731'>any processor that uses that ISA can be executed</span> on.

| Machine Code | MIPS Language |
| :--: | :--: |
| In binary | In MIPS language |
| Hard to read and code | Easier to write and is readable |
| 1000 1100 1010 000 | <- Assembler <- add A, B |
| Can be in hexadecimal for a more readable format | Can produce pseudo instructions (Set of instructions / Macro) |
|  | Considering performance, only real instructions are counted |
# Breakdown on How MIPS Instructions as Processed
---
The first step is that any <span style='color:#fa8231'>code will be transformed by the GCC into <span style='color:#8854d0'>MIPS</span> code</span>.
```C
int res = 0;
for (int i = 1; i <10; i++) {
	res = res +1
}

/* In MIPS (Not real but for intuition)
res <- res + 1
i <- i + 1
if i < 10, repeat
*/
```
<div style="page-break-after: always;"></div>

A computer has 2 <span style='color:#fa8231'>major components</span> which are the <span style='color:#f7b731'>processor</span> and <span style='color:#f7b731'>memory</span>.
- Processor performs computations using an <span style='color:#f7b731'>arithmetic and logic unit</span> (ALU)
- Memory or RAM, stores code (<span style='color:#f7b731'>instructions</span>) and <span style='color:#f7b731'>data</span>
- <span style='color:#f7b731'>Bus</span> which is a data connection between processor and RAM
# Registers
---
Inside a processor there are <span style='color:#0fb9b1'>registers</span> that has <span style='color:#f7b731'>32 raw bits</span>, which allows <span style='color:#f7b731'>fast access to data</span>. Which acts as a faster memory. However there are a <span style='color:#eb3b5a'>limited number</span> of them (typically 16 - 32). For <span style='color:#f7b731'>MIPS, they have 32 registers</span>, all represented by 5 bits.

A compiler <span style='color:#f7b731'>associates</span> (does the mapping) variables with <span style='color:#0fb9b1'>registers</span>. However the difference is that registers has <mark style='background:#f7b731'>no data type</mark> as data is assumed to be stored correctly and the <span style='color:#f7b731'>instructions will interpret its data type</span>.

Registers for MIPS are in the form of `$0` or `$a0` (name).

**List of registers in MIPS :**

| Name | Register Number | Usage |
| :--: | :--: | :--: |
| $zero or $0 | 0 | Constant value of 0 no matter what |
| $at | 1 | Reserved for the assembler (Not used) |
| $v0 - $v1 | 2 - 3 | Values for results and expression evaluation or return value (Value register) |
| $a0 - $a3 | 4 - 7 | Arguments, used to pass parameters into functions |
| $t0 - $t7 | 8 - 15 | Temporaries, used to store intermediate values  |
| $s0 - $s7 | 16 - 23 | Program variables |
| $t8 - $t9 | 24 - 25 | More temporaries |
| $k0 - $k1 | 26 - 27 | Reserved for operating system (Not used) |
| $gp | 28 | Global pointer |
| $sp | 29 | Stack pointer, points to the top of the function call stack |
| $fp | 30 | Frame pointer |
| $ra | 31 | Return address, shows the program where to return after a function |
Note that for the last 4 registers (28 - 31), it <mark style='background:#eb3b5a'>should not be altered or touched</mark>.
# MIPS Assembly Language
---
In <span style='color:#8854d0'>MIPS</span>, <mark style='background:#f7b731'>each line contains 1 instruction only</mark>. While `#` are used for comments.

A typical instruction will contain <mark style='background:#f7b731'>at most 3 operands</mark>, <span style='color:#eb3b5a'>2 sources</span> and <span style='color:#20bf6b'>1 destination</span>.
![[General Instruction Syntax for MIPS.png|center|500]]

Most <span style='color:#fa8231'>MIPS arithmetic operations</span> are mainly, <span style='color:#f7b731'>register to register</span>, this just means that everything from the destination to the source will be on the register.
# MIPS Instruction Classification
---
There are <span style='color:#fa8231'>3 types</span> of classifications :
1) **R-format**, which are instructions for <span style='color:#f7b731'>registers only</span>
2) **I-format**, instructions that requires <span style='color:#f7b731'>registers and immediate values</span>
3) **J-format** for instructions with <span style='color:#f7b731'>only one immediate value </span>

Note that to <span style='color:#fa8231'>convert a register into their binary</span> representation refer to the <span style='color:#8854d0'>MIPS Sheet</span>.
## R-Format

It uses the <mark style='background:#f7b731'>register addressing mode</mark>.

| opcode (Operation Code) | rs (Src Register) | rt (Target Register) | rd (Dest Register) | shamt (Shift Amount) | funct |
| :--: | :--: | :--: | :--: | :--: | :--: |
| 6 Bits | 5 Bits | 5 Bits | 5 Bits | 5 Bits | 6 Bits |
**Take note** :
- A <span style='color:#0fb9b1'>register</span> is a <span style='color:#f7b731'>5 bit representation</span>
- The total number of<span style='color:#f7b731'> bits used is 32</span> (0 - 31)
- Shift amount is 5 bits because, shifting 32 bits <span style='color:#f7b731'>clears the register</span>, this will be <mark style='background:#f7b731'>0 for non shift instructions</mark>
- `opcode` and `funct` will combine their values together to <span style='color:#f7b731'>determine what functions to use</span>. (Refer to reference sheet)

**Example of Converting Instructions into Binary / Hexadecimal :** `add $8, $9, $10`

|  | opcode | rs | rt | rd | shamt | funct |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| **Value** | 0 | 9 | 10 | 8 | 0 | 32 |
| **Binary** | 000000 | 01001 | 01010 | 01000 | 00000 | 100000 |
The last step is to <span style='color:#fa8231'>convert into hexadecimal</span> which will be $012A4020_{16}$, for human readability.
<div style="page-break-after: always;"></div>

## I-Format

It uses the <mark style='background:#f7b731'>immediate addressing mode</mark>.

A downside of the <span style='color:#0fb9b1'>R-Format</span>, is that if instructions with immediate values are used, the `shamt` <span style='color:#eb3b5a'>can only represent 0 to 31</span>. To <span style='color:#20bf6b'>compromise</span> this, the I<span style='color:#0fb9b1'>-Format</span> created is partially consistent, keeping <span style='color:#20bf6b'>implementation simple and nearly similar</span>. 

What has changed is that the `rt`,  `shamt` and `funct` <span style='color:#f7b731'>are removed</span>.

| opcode (Operation Code) | rs (Src Register) | rt (Target Register) | Immediate Value |
| :--: | :--: | :--: | :--: |
| 6 Bits | 5 Bits | 5 Bits | 16 Bits |
**Take note** :
- `opcode` now is <span style='color:#f7b731'>uniquely specifies</span> an instruction since `funct` is removed
- `immediate` or <span style='color:#0fb9b1'>signed integer</span> ([[Number Systems#2's Compliment|2's Compliment]]), except for bitwise operations can represent up to $2^{16}$
- Converting to binary is similar with the R-format.
## J-Format

It uses the <mark style='background:#f7b731'>pseudo - direct addressing mode</mark>.

| opcode (Operation Code) | Label (Target Address) |
| :--: | :--: |
| 6 Bits | 26 Bits |
Recall that a `jump` instruction has only the <span style='color:#f7b731'>label</span>. Therefore, for <span style='color:#f7b731'>consistency</span>. `opcode` is 6 bits then the remaining <span style='color:#f7b731'>26 bits</span> is for the <span style='color:#f7b731'>target address</span>.

**Take note** :
- The `target address` can be obtained by <span style='color:#f7b731'>removing 4 MSBs and 2 LSB</span> from the address of the instruction to be jumped to. Thus the result will be 26 bits.
- This <mark style='background:#fa8231'>only works if</mark> the first 4 bits of the next instruction is the same as the instruction being jump to

To know the <span style='color:#0fb9b1'>effective address</span> to where it will jump to :
1) Take the <span style='color:#f7b731'>4 MSB from</span> $\text{PC } + 4$
2) Take the 26 bit target address
3) The last 2 bits are default to 00 due to MIPS being word address (Last 2 bits, 2 and 1 will always be 0)

## Base Addressing (Displacement Addressing)

This is mainly used for `lw` and `sw`, since the memory location is <span style='color:#f7b731'>some offset times a register</span>.

## PC - relative Addressing

Mainly used for `beq` and `bne`, where the address is some <span style='color:#f7b731'>sum of PC and a constant</span>.
<div style="page-break-after: always;"></div>

# Instruction Address
---
A register called <span style='color:#0fb9b1'>Program Counter</span> (PC) which keeps the <span style='color:#f7b731'>address of next instruction</span> to be executed.  

Commands like `beq` & `bne` <span style='color:#f7b731'>changes the instructions address</span> inside the PC. However recall that <span style='color:#eb3b5a'>immediate values holds 16 bits but instruction addresses are 32 bits</span>. Therefore for branches the <span style='color:#f7b731'>change in PC is very small</span> (50 instructions).

A solution is to <span style='color:#f7b731'>specify the address relative </span>to the <span style='color:#0fb9b1'>PC</span>, $\text{ PC value } +$ `immediate` value. This can branch up to $\pm 2^{15}$ <mark style='background:#f7b731'>instructions</mark>. But this can be further extended. Since MIPS is word aligned, addressed are in multiples of 4. Therefore the immediate value can<span style='color:#f7b731'> indicate the number of words instead</span>, increasing the range to $\pm 2^{17}$ <mark style='background:#f7b731'>bytes</mark>. This is for <span style='color:#0fb9b1'>I-format</span>.

For a branch to <span style='color:#fa8231'>go beyond its maximum</span> range, combine the `bne` / `beq` with a `jump` instruction.

There are 2 situations :
1) Branch <span style='color:#fa8231'>not taken</span>, $\text{PC} + 4$
2) Branch <span style='color:#fa8231'>taken</span> $(\text{PC } + 4) + ($ `immediate` $\times 4)$ 

For <span style='color:#0fb9b1'>J-format</span> it will be $2^{26}$ <mark style='background:#f7b731'>instructions</mark> and $2^{28}$ <mark style='background:#f7b731'>bytes</mark>. Thus it <span style='color:#eb3b5a'>can't really cover all</span> $2^{32}$ memory addresses and its <span style='color:#fa8231'>maximum jump range</span> is <mark style='background:#f7b731'>256MB boundary</mark> ($2^{28} = 256$).

To <span style='color:#fa8231'>go beyond the maximum</span> range the instruction `jr`, jump range can be used where the <span style='color:#f7b731'>target address is specified in a register</span>.
# Arithmetic Instructions
---
Arithmetic operations directly work on registers. And <span style='color:#f7b731'>constants are directly taken</span> as well.

Therefore any arithmetic operations <span style='color:#20bf6b'>can be faster</span> with <span style='color:#0fb9b1'>registers</span>, since it is faster to take from it than from memory. Results are then return to the respective registers.
### Addition
Given the following <span style='color:#8854d0'>C</span> statement to do addition, this is what it will look like in <span style='color:#8854d0'>MIPS</span> :
```C
int a = 0; /* $s0 */
int b = 1; /* $s1 */
int c = 2; /* $s2 */

a = b + c /* In MIPS this will be : add $s0, $s1, $s2 */
```

This can be used to <span style='color:#f7b731'>copy a value</span> to another register, by adding a 0.
<div style="page-break-after: always;"></div>

### Subtraction
Given the following <span style='color:#8854d0'>C</span> statement to do subtraction, this is what it will look like in <span style='color:#8854d0'>MIPS</span> :
```C
int a = 0; /* $s0 */
int b = 1; /* $s1 */
int c = 2; /* $s2 */

a = c - b; /* In MIPS this will be : sub $s0, $s2, $s1 */

/* How about something more complex */
a = b + c - a;
/* In MIPS this will be spilt into 2 :
1) add $t0, $s1 $s2 // Notice the usage of the tempoary registers
2) sub $s0, $t0, $s0
*/
```

It can also be used to copy a value, by subtracting 0 when comparing with another register.
### Constant / Immediate Operands

The term <span style='color:#0fb9b1'>immediate values</span> are just numerical constants, which MIPS supplies a set of operations such ass `addi`.
```C
int a = 0; /* $s0 */

a = a + 4 /* In MIPS this will be : addi $s0, $s0, 4 */
```

For these types of operations, the <span style='color:#f7b731'>2nd source is a constant</span>, and this constant has a range from $-2^{15}$ to $2^{15} - 1$, which is just the [[Number Systems#2's Compliment|16 bit 2s compliment number system]]. Therefore `subi` does not exist as a negative number can be added.
### Register Zero

Simple things like assigning a variable to some number requires the number 0. This can be provided in MIPS using the `$0` or `$zero` register which has the value of 0.
```C
int a = 10; /* $s0 $*/
int b = a; /* In MIPS this will be : add $s1, $s0, $zero */

/*This is common that MIPS made a pseudo operation called move $0, $s1 which will be replaced by add*/
```
This `move` operation is a <span style='color:#0fb9b1'>pseudo - instructions</span>, which are fake instructions which gets <span style='color:#f7b731'>translated by MIPS for convenience</span>.
## Logical Operations

Some addition operations not known are **NOR** and **XOR**.

For **NOR** (Not or), <span style='color:#f7b731'>both</span> $a$ and $b$ <span style='color:#f7b731'>must be 1</span> (True) for the <span style='color:#fa8231'>result to be 1</span>, otherwise is 0.

For **XOR** (Exclusive or), for the <span style='color:#fa8231'>result to be 1</span>, <span style='color:#f7b731'>both</span> $a$ and $b$ must be of <span style='color:#f7b731'>different value</span>, otherwise is 0.
<div style="page-break-after: always;"></div>


### Shift Left logical / Shift Right Logical

Or `sll` <span style='color:#f7b731'>moves all bits to the left</span> by the specified number of positions. In <span style='color:#8854d0'>C</span>, this is denoted by `<<`.
```C
int a = 1 /* $s0 : 1011 1000 0000 0000 0000 0000 0000 1001 */
a << 4; /* In MIPS this will be : sll $t2 $0, 4 */
/* $t2 : 1000 0000 0000 0000 0000 0000 1001 0000 */
```

This the left most $n$ bits will be <span style='color:#f7b731'>removed</span>, and <span style='color:#f7b731'>add in</span> $n$ number of <span style='color:#f7b731'>0s at the right</span>.

The <span style='color:#fa8231'>max number of shits</span> that can be done is <mark style='background:#f7b731'>31 shifts</mark> (0 - 31).

`srl`, is similar to `sll` but instead of shifting to the left, it <span style='color:#f7b731'>shits to the right</span>, denoted by `>>` in <span style='color:#8854d0'>C</span>.

Whenever, <span style='color:#fa8231'>shifting</span> to the left / right by $n$ bits, it is the same as <span style='color:#f7b731'>multiplying / dividing by </span>$2^{n}$, which is faster.

### Bitwise AND

`and` in <span style='color:#8854d0'>MIPS</span> compares the bits stored in 2 registers and outputs the corresponding bits :
- If <span style='color:#f7b731'>both are 1</span> the <span style='color:#f7b731'>resulting bit is 1</span>
- Else the resulting bit is 0
```C
int a = 1 /* $s0 : 0110 0011 0010 1111 0000 1101 0101 1001 */
int b = 2 /* $s1 : 0000 0000 0000 0000 0011 1100 0000 0000 */

a & b /* In MIPS this will be : and $t0 $s0, $s1 */
/* $s0 : 0110 0011 0010 1111 0000 1101 0101 1001 */
/* $s1 : 0000 0000 0000 0000 0011 1100 0000 0000 */ /* This register is known as a mask*/
/* $t0 : 0000 0000 0000 0000 0000 1100 0000 0000 */
```

This <span style='color:#3867d6'>bitwise AND</span> operation is usually <mark style='background:#f7b731'>used for a masking operation</mark>. Thus if the <span style='color:#f7b731'>last 12 bits are of interest</span>, then for the <span style='color:#0fb9b1'>mask</span>, the <span style='color:#f7b731'>last 12 bits will be all 1s</span>, which has an immediate version `andi $t0, $t1, 0xFFF`.

It can also be used to copy a value, by setting all the bits to 1 when comparing with another register.
### Bitwise OR

`or` in <span style='color:#8854d0'>MIPS</span> compares the bits stored in 2 registers and outputs the corresponding bits :
- If <span style='color:#f7b731'>either are 1</span> the <span style='color:#f7b731'>resulting bit is 1</span>
- Else the resulting bit is 0
```C
int a = 1 /* $s0 : 0110 0011 0010 1111 0000 1101 0101 1001 */
int b = 2 /* $s1 : 0000 0000 0000 0000 0011 1100 0000 0000 */

a | b /* In MIPS this will be : or $t0 $s0, $s1 */
/* $s0 : 0110 0011 0010 1111 0000 1101 0101 1001 */
/* $s1 : 0000 0000 0000 0000 0011 1100 0000 0000 */
/* $t0 : 0110 0011 0010 1111 0011 1101 0101 1001 */
```

Thus if the <span style='color:#f7b731'>last 12 bits MUST be 1</span>, then for the <span style='color:#0fb9b1'>mask</span>, the <span style='color:#f7b731'>last 12 bits will be all 1s</span>, which has an immediate version of the following, `ori $t0, $t1, 0xFFF`, where the <mark style='background:#f7b731'>2nd source is a 32 bit integer</mark>.
### Bitwise NOR

Also known as <span style='color:#3867d6'>not or operation</span>, `nor` in <span style='color:#8854d0'>MIPS</span> compares the bits stored in 2 registers and outputs the corresponding bits :
- If <span style='color:#f7b731'>both are 0</span> the <span style='color:#f7b731'>resulting bit is 1</span>
- Else the resulting bit is 0
```C
int a = 1 /* $s0 : 0110 0011 0010 1111 0000 1101 0101 1001 */
int b = 2 /* $s1 : 0000 0000 0000 0000 0011 1100 0000 0000 */

a ~ b /* In MIPS this will be : nor $t0 $s0, $s1 */
/* $s0 : 0110 0011 0010 1111 0000 1101 0101 1001 */
/* $s1 : 0000 0000 0000 0000 0011 1100 0000 0000 */
/* $t0 : 1001 1100 1101 0000 1100 0010 1010 0110 */
```

The <span style='color:#3867d6'>NOT operation</span> `!` can be achieved using `nor` as such `nor $t0, $t0, $zero`. Since 1 is true and 0 is false. 
- Let $b =$`$zero`
- Let $a$ be some <span style='color:#3867d6'>Boolean</span> value in 32 bit
- If $a$ is false, meaning the bits is 0, then `a ~ b` will return 1 which is true
- If $a$ is true, meaning the bits is 1, then `a ~ b` will return 0 which is false
### Bitwise XOR

Also known as <span style='color:#3867d6'>not equal operation</span>, `xor` in <span style='color:#8854d0'>MIPS</span> compares the bits stored in 2 registers and outputs the corresponding bits :
- If <span style='color:#f7b731'>both are different bits</span> the <span style='color:#f7b731'>resulting bit is 1</span>
- Else the resulting bit is 0
```C
int a = 1 /* $s0 : 0110 0011 0010 1111 0000 1101 0101 1001 */
int b = 2 /* $s1 : 0000 0000 0000 0000 0011 1100 0000 0000 */

a ^ b /* In MIPS this will be : xor $t0 $s0, $s1 */
/* $s0 : 0110 0011 0010 1111 0000 1101 0101 1001 */
/* $s1 : 0000 0000 0000 0000 0011 1100 0000 0000 */
/* $t0 : 0110 0011 0010 1111 0011 0001 0101 1001 */
```

The <span style='color:#0fb9b1'>NOT operation</span> `!` can be achieved using `xor` as such `nor $t0, $t0, 0xFFFFFFFF`. Since 1 is true and 0 is false. 
- Let $b =$`$0xFFFFFFFF`,<mark style='background:#f7b731'> which is all 1's</mark>
- Let $a$ be some <span style='color:#3867d6'>Boolean</span> value in 32 bit
- If $a$ is false, meaning the bits is 0, then `a ~ b` will return 1 which is true
- If $a$ is true, meaning the bits is 1, then `a ~ b` will return 0 which is false
<div style="page-break-after: always;"></div>

## Storing Large Constants into a Register

![[Storing Long Constants.png|center|350]]

# Memory Instructions
---
Code inside memory, <span style='color:#f7b731'>runs sequentially</span>. Instructions to the processor are sent through the <span style='color:#f7b731'>BUS</span>. However, the <span style='color:#eb3b5a'>memory is much slower than the processor</span> and time will be wasted.

To <span style='color:#f7b731'>avoid frequent access</span>, temporary storage called <span style='color:#0fb9b1'>registers</span> are used by processors, which <span style='color:#20bf6b'>works as the same speed as the processors</span>. Instructions, <span style='color:#0fb9b1'>load</span> (to register) and <span style='color:#0fb9b1'>store</span> (to memory) can <mark style='background:#f7b731'>only be used to access data in memory</mark>.

<span style='color:#fa8231'>Loading into the register</span> is known as <span style='color:#0fb9b1'>variable mapping</span>. And this is also known as the <span style='color:#0fb9b1'>load-store model</span> as <mark style='background:#f7b731'>all instructions except load and store are done on registers</mark>. This is done by compiler.

Recall that <span style='color:#fa8231'>memory is referring to RAM</span>. Think of memory as a 1D array, where each segment <mark style='background:#f7b731'>stores 1 byte of data</mark> and each storage space has an <mark style='background:#f7b731'>address</mark>. This is called <span style='color:#0fb9b1'>byte addressing</span>.

If the address uses <span style='color:#fa8231'>k-bits</span>, then the <span style='color:#fa8231'>total address space</span> is $2^{k}$.

There is <span style='color:#fa8231'>another way to access memory</span> is through <span style='color:#0fb9b1'>word addressing</span>

Some properties of <span style='color:#0fb9b1'>word addressing</span> :
- The size of a word is given by $2^{n}$ bytes (4 Bytes for MIPS)
- Distinct address for each word
- This is a common unit of transfer between processor and memory
- It coincide with register, integer and instruction size
- Total number of memory words = ${2^{32}}/{2^{2}}$

Now lets say the <span style='color:#fa8231'>memory consist of 8 bytes</span>, and a <span style='color:#0fb9b1'>word</span> consist of <span style='color:#fa8231'>4 bytes</span> ;
- <span style='color:#0fb9b1'>Words</span> are <span style='color:#f7b731'>aligned</span> if they begin at a <span style='color:#f7b731'>byte address multiple of the number of bytes in a word</span>
- Thus is a word is stored at address 0, then it can <span style='color:#f7b731'>store 2 words</span>.

One issue with this is called <span style='color:#eb3b5a'>mis-aligned word</span>. Assuming that some data is stored in bytes 1 to 4. Clearly there is 1 overlap and now the processor needs to <span style='color:#f7b731'>retrieve 2 words at index 0 and 4 and discard the bytes not bring used</span> to properly align the word, <span style='color:#eb3b5a'>making the processor slow</span>. <span style='color:#8854d0'>MIPS</span> does <span style='color:#eb3b5a'>not allow unaligned access</span>.

To know if <span style='color:#f7b731'>something is properly aligned</span>, just take the <span style='color:#f7b731'>address and divide by the number of bytes in a word</span>.
## Load Word Instruction

In <span style='color:#8854d0'>MIPS</span> to <span style='color:#fa8231'>load data from memory into a register</span>, the instruction `lw` is used.

An example on how to use it will be, `lw $t0, 4($s0)`, where :
- `$s0`, is the source register
- `$t0` is the destination register
- 4 bytes, is the <span style='color:#f7b731'>displacement / offset</span>, which is the size of a <span style='color:#0fb9b1'>word</span> (<mark style='background:#f7b731'>Must be a multiple of word size</mark>)

There is also a <span style='color:#3867d6'>load byte instruction</span>, `lb` but instead of 4 bytes it just <span style='color:#f7b731'>load 1 byte</span> of data.

If the source address is 8000 (Base address) and the above instruction is used, the data at 8004 - 8007 will be copied.
## Store Word Instruction

In <span style='color:#8854d0'>MIPS</span> to <span style='color:#fa8231'>store data from register into memory</span>, the instruction `sw` is used.

An example on how to use it will be, `sw $t0, 12($s0)`, where :
- `$s0`, is the destination register
- `$t0` is the source register
- 12 bytes, is the <span style='color:#f7b731'>displacement / offset</span>, which is the size of a <span style='color:#0fb9b1'>word</span> (<mark style='background:#f7b731'>Must be a multiple of word size</mark>)

There is also a<span style='color:#0fb9b1'> store byte instruction</span>, `sb` but instead of 4 bytes it just <span style='color:#f7b731'>store data in 1 byte</span> (Lowest byte of source).

Therefore, lets say the source address is 8000 and the above instruction is used, the data at 8012 - 8015 will store the data.

```C
int arr[11] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10}; /* Lets say this is stored in $s3 */
int h = 11; /* Lets say this is stored in $s2 */
arr[7] = h + A[7];
/* In MIPS :
lw $t0, 40($s3) # This is because $s3 sotres address of idx 0, this to access 10 just *4 
add $s0, $s2, $t0
sw $t0, 28($s3)
*/
```
## Other Instructions

There are pseudo-instructions for <span style='color:#f7b731'>unaligned load and storing</span> of words called `ulw` and `usw`, which <span style='color:#8854d0'>MIPS</span> translates into a sequence of `lb` and `sb` and some other operations.

There are also other instructions such as
- Load and store halfword `lh` and `sh`
- Load and store word left / right `lwl`, `lwr`, `swl`, `swr`
<div style="page-break-after: always;"></div>

## Swapping Elements
```C
void swap(int arr[], int n) { /* n is stored in register $5 and arr in $4*/
	int temp = arr[n]; /* temp is stored in register $15 */
	arr[n] = arr[n + 1];
	arr[n + 1] = temp;
}
/* In MIPS
sll $2, $5, 2 # Takes n and shift left by 2 (2^2) since a word is 4 bytes
add $2, $4, $2 # Adds bytes in $2 to $4 
lw $15, 0($2) # Get data at n, since $2 is the memory at arr[n]
lw $16, 4($2) # Get data at n+1, 4 since arr[n+1] is 4 bytes away from arr[n]
sw $16, 0($2) # Store item in arr[n+1] into arr[n]
sw $15, 4($2) # Store item in temp into arr[n+1]
*/
```
# Control Flow Instructions
---
These instructions <span style='color:#f7b731'>change of control flow</span> based on some <span style='color:#f7b731'>condition(s)</span>. Control flow instructions includes, repetition (loops) and if-else statements.

It can <span style='color:#f7b731'>change the next instructions to be executed</span>. These types of instructions are called "goto" instructions.

**Types of decision making Statements**
1) <mark style='background:#0fb9b1'>Conditional</mark> (**Branch**)

<span style='color:#3867d6'>Branch not equal</span> `bne`, as the name implies, branch to some instruction if the values <span style='color:#20bf6b'>matches</span>. 

It can be used as such `bne $t0, $t1, label` where :
- `$t0` and `$t1` are the <span style='color:#f7b731'>values to be compared with</span>
- `label` is some <span style='color:#f7b731'>pointer to some instruction</span> if the condition is true

<span style='color:#3867d6'>Branch if equal</span> `beq`, as the name implies, branch to some instruction if the values <span style='color:#eb3b5a'>does not</span> match. 

It can be used as such `beq $t0, $t1, label` similar to `bne`.

Take note that <mark style='background:#f7b731'>labels are not instructions</mark>, it is just some anchor or pointer to some instruction and does not require memory. This <span style='color:#0fb9b1'>label</span> <span style='color:#f7b731'>contains the memory address of the instruction</span> it is point to.

2) <mark style='background:#0fb9b1'>Unconditional</mark> (**Jump**)

<span style='color:#3867d6'>Jump</span> or `j` has <span style='color:#f7b731'>no condition</span>, when MIPS sees this instruction, it will just jump to the label. It can be used as such `j lable`. Which is something similar with the `goto` statement in <span style='color:#8854d0'>C</span>. Unlike branches, `jump` has not restriction.

This is equivalent to `beq $s0 $s0, L1`, since `$s0` will always be equal to itself. 

There are <span style='color:#fa8231'>2 types of branches</span> :
1) Selection, which is to branch / jump <span style='color:#f7b731'>down</span>
2) Repetition, which is to branch / jump <span style='color:#f7b731'>up</span>

## IF Statements

```C
int i = 1, j = 1, f = 1, g = 1, h = 1; /* $s0, $1, $2, $3, $s4 */

if (i == j) {
	f = g + h;
} else {
	f = g - h;
}
/* 2 Versions in MIPS
1)
bne $s3, $s4, If # If part
sub $s0, $s1, $s2
j exit
If : add $s0, $s1, $s2
Exit :

2) Condition Inversion
bne $s3, $s4, Else # Else part
add $s0, $s1, $s2 # If part
j exit # If this jump instruction is not here then Else will be executed
Else : sub $s0, $s1, $s2
Exit :
*/
```

From the above there are <span style='color:#fa8231'>2 equivalent translations</span>, however the <span style='color:#20bf6b'>2nd one is more efficient</span> since it can be shorter. Therefore by writing the <span style='color:#0fb9b1'>conditions inversely</span>, it can be <span style='color:#20bf6b'>shorter and more efficient</span>.

What if, the conditions checks for less than or more than. There is no actual instruction called branch less than `blt` (pseudo-instructions). However the <span style='color:#3867d6'>set on less than</span> instruction, `slt` or `slti` can be used.
```C
int i = 1, j = 2; /* $s0, $s1 */
if (i < j) {
	i += 1;
}
/* In MIPS
slt $t2, $s0, $s1 # If $s0 is less than $s1 then $s2 will contain 1 which is true
beq $s2, $zero, Exit # If part (If checking for greater than use bnq, but dont branch to exit)
addi $s0, $s0, 1
Exit :
*/
```
<div style="page-break-after: always;"></div>

## While & For Loop Statements
```C
// Fun fact u can use lables in C programming
int i = 1 , j = 10, k = 0 /* $s3, $s4, $s5 */
while (j == k) { 
	i = i + 1;
}
/* In MIPS
Loop : bne $s4, $s5, Exit # If (j != k) exit
       addi $s3, $s3, 1 # i = i + 1
       j loop # Repeat loop
Exit :
*/

for (int i = 0; i < 10; i++) { /* $s0 */
	a = a + 5; /* $s2 */
}
/* In MIPS
	   add $s0, $zero, $zero # Initlise i as 0 
	   addi $s1, $zero, 10 # This is for the stopping condition i < 10
Loop : beq $s0, 10, Exit # for(int i = 0; i < 10;..), but use beq cause the lable goes to Exit
       addi $s2, $s2, 5 # a = a + 1
       addi $s0, $s0, 1 # for(...; i++)
       j loop # Repeat loop
Exit :
*/
```
## Array Element Access

Here is a <span style='color:#fa8231'>simple flow</span> of what is needed :
1) Initialise variables, loop counter and array pointers
2) Calculate the address
3) Load the data
4) Perform Task
5) Update loop counter and array pointers
6) Compare and branch or exit

```C
int arr[40] = {0,0,1,...}; /* $t0 */
int result = 0; /* $t8 */
i = 0; /* $t7 */

while (i < 40) {
	if (arr[i] == 0) {
		result ++;
	}
	i++;
}
/* In MIPS
1) Using i as a stopping point
	   addi $t8, $zero, 0
	   addi $t7, $zero, 0 # i
	   addi $t6, $zero, 40 # end point
loop : beq $t6, $t7, end # Condition for while loop
	   sll $t1, $t7, 2 # Get pointer based of i, *4 to number
	   add $t2, $t0, $t1 # Change array pointer
	   lw $t3, 0($t2) # load data
	   bne $t3, $zero, skip # If not equals to 0 then continue the loop 
	   addi $t8, $t8, 1 # result ++
skip : addi $t7, $t7, 1 # i++
	   j loop
Exit :
*/

int arr[40] = {0,0,1,...}; /* $t0 */
int result = 0; /* $t8 */
int *ptr = arr; /* $t7 */
int *end = &arr[40]; /* $t6 */

while (ptr < end) {
	if (*ptr == 0) {
		result ++;
	}
	ptr++;
}
/* In MIPS
2) Using array address as a stopping point
	   addi $t8, $zero, 0
	   addi $t7, $t0, 0 # ptr at index 0
	   addi $t6, $t0, 160 # end point using address (4 * 40 = 160)
loop : beq $t6, $t7, end # Condition for while loop
	   lw $t3, 0($t7) # load data from pointer
	   bne $t3, $zero, skip # If not equals to 0 then continue the loop 
	   addi $t8, $t8, 1 # result ++
skip : addi $t7, $t7, 4 # Increment pointer by 4 bytes!!
	   j loop
Exit :
*/
```

From the 2 implementations, <span style='color:#f7b731'>they are identical</span> but the <span style='color:#fa8231'>second implementation</span> using pointers as a stopping point is <span style='color:#20bf6b'>faster</span> as it is shorter, thus <span style='color:#20bf6b'>more efficient</span>.