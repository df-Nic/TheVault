---
title: Processor Control
Date Created: 2024-02-26
tags:
  - CS2100
  - Hardware
---
# Generating Control Signals
---
When learning about [[Datapath|Datapath]], there are various control signals which <span style='color:#f7b731'>controls and direct the flow of data</span>.

How this is generated is <span style='color:#f7b731'>based on the instruction</span>, more specifically the `Opcode`.
- For [[MIPS#R-Format|R-type]] instructions, the<span style='color:#f7b731'> function code</span> will be used.

Design a <span style='color:#0fb9b1'>combinational circuit</span>, to generate signals based on `Opcode` and `Function code`. With the <span style='color:#0fb9b1'>control unit</span>.
>A **combinational circuit** is a circuit that takes in 2 inputs and it <span style='color:#f7b731'>output changes as the 2 inputs change</span>.

## Types of Control Signals

1) `RegDst`
> If this signal is <span style='color:#fa8231'>set to 1</span> (**True**), then the <span style='color:#f7b731'>destination register</span> will be an input to the <span style='color:#f7b731'>write register</span>, <span style='color:#f7b731'>else</span> it will be the <span style='color:#f7b731'>target register</span>

2) `RegWrite`
>If this signal is <span style='color:#fa8231'>set to 1</span> (**True**), then the <span style='color:#f7b731'>value in write register will be written into the register</span> inside write register, else it will do nothing.

3) `ALUSrc`
>If this signal is <span style='color:#fa8231'>set to 1</span> (**True**), then the 2nd operand input for the ALU will be the <span style='color:#f7b731'>sign extended immediate value</span>, else it will be the <span style='color:#f7b731'>register in read data 2 output</span>.

4) `MemRead`
>If this signal is <span style='color:#fa8231'>set to 1</span> (**True**), then the data will be <span style='color:#f7b731'>read from the address</span> and will be outputted to read data, else it will not read

5) `MemWrite`
>If this signal is <span style='color:#fa8231'>set to 1</span> (**True**), then the <span style='color:#f7b731'>value from register data 2 will be written</span> to the memory address, else it will not write into the address

6) `MemToReg`
>This signal is <b><mark style='background:#fa8231'>swapped</mark></b>. If this signal is <span style='color:#fa8231'>set to 1</span> (**True**), the<span style='color:#f7b731'> value from read data</span> will be <span style='color:#f7b731'>written into the register</span>, else it will be the <span style='color:#f7b731'>ALU output what will be written</span> instead

7) `PCSrc`
>If this signal is <span style='color:#fa8231'>set to 1</span> (**True**), if it is <b><mark style='background:#f7b731'>a branch instruction and the branch is taken</mark></b>, using a <span style='color:#0fb9b1'>AND gate</span>. If it is a 1, then PC will be updated with `pc + 4 + 4 * immediate`, else it will be `pc + 4`


There is one more which is the `ALUControl` signal which will be discussed more in detail later.

# Closer Look in the ALU
---
The **ALU**, is essentially a <span style='color:#0fb9b1'>combinational circuit</span>, which can perform several arithmetic operations. It contains a table of <span style='color:#f7b731'>functions</span> which are <span style='color:#f7b731'>mapped to a specific</span> `ALUcontrol` value.

![[1-Bit ALU Layer.png|center|500]]

An ALU, consists of <span style='color:#f7b731'>32 of these 1-Bit layers</span>, each for 1 bit (32 Bit).

There is an `Ainvert` and `Binvert`, which tells the <span style='color:#f7b731'>MUX to take the inverse</span> (**1**) as input or not. This inverse is just changing the bit between 0 and 1.

Lastly, `operation`, which chooses between 1 of 3 results.

|           | `ALUcontrol` |             | Function |
|:---------:|:------------:|:-----------:|:--------:|
| `Ainvert` |  `Binvert`   | `Operation` |          |
|     0     |      0       |     00      |   AND    |
|     0     |      0       |     01      |    OR    |
|     0     |      0       |     10      |   add    |
|     0     |      1       |     10      | subtract |
|     0     |      1       |     11      |   slt    |
|     1     |      1       |     00      |   NOR    |
For <span style='color:#3867d6'>subtract</span>, which is ($A - B$), is done by, ($A + B' + 1$) which is ($A + (-B)$). This is why the `Binvert` is 1. Also, the <span style='color:#0fb9b1'>0 slice</span> (Layer for bit 0), the `Cin` is set to 1, for the $+ 1$.

For the <span style='color:#3867d6'>NOR</span> operation, the usage of $A'$ <span style='color:#3867d6'>AND</span> $B'$, through <span style='color:#3867d6'>De Morgan's law</span>, $(A + B)' = A' . B'$.

# Multilevel Decoding
---
When designing the `ALUcontrol` signal, it depends on the `Opcode` and the `function code`. There is a <span style='color:#0fb9b1'>brute force approach</span> which <span style='color:#eb3b5a'>can take very long</span> since there is $2^{12}$ combinations.

Thus the <span style='color:#20bf6b'>faster way</span>, called the <span style='color:#0fb9b1'>multilevel decoding approach</span> which uses some input to reduce the number of cases.

**Intermediate Signal :** `ALUop`
>The <span style='color:#0fb9b1'>control circuit</span>, will take in the `Opcode` of the instruction to generate a 2-bit `ALUop` signal

| Instruction Type | ALUop |
| :--------------: | :---: |
|     lw / sw      |  00   |
|       beq        |  01   |
|      R-type      |  10   |

If it is an [[MIPS#R-Format|R-type]] instruction, the <span style='color:#0fb9b1'>control circuit</span> will take in the `Opcode` and generate an `ALUop`. Afterwards the <span style='color:#0fb9b1'>ALU control circuit</span> will take in the `ALUop` and the `Function Code` and output a `ALUcontrol` (**4-bits**), based on the <b><mark style='background:#0fb9b1'>truth table</mark></b>.
## ALU Truth Table
![[ALU Truth Table.png|center|600]]

The $X$, in the table is called a <span style='color:#0fb9b1'>don't care term</span>, where the <span style='color:#f7b731'>bit can be 0 or 1</span> and it will not matter. The bits that are labeled as don't care terms are <span style='color:#f7b731'>not unique identifiers</span> in distinguishing them from the others.

**Some patterns for the output**
- $A3$ is always 0 no matter what
- $A2$ is `ALUop1` <span style='color:#3867d6'>OR</span> `ALUop2` <span style='color:#3867d6'>AND</span> `F1`
- $A1$ and $A2$ will be discussed later
## ALU Control Unit Design
![[ALU Control Unit Design Diagram.png|center|600]]

## Control Unit Outputs
![[Control Unit Outputs.png|center]]

The above shows what the control unit, <span style='color:#fa8231'>outputs</span> to the various control signals <span style='color:#fa8231'>inside the Datapath</span>.
<div style="page-break-after: always;"></div>

## Combinational Circuit Implementation
![[Combinational Circuit implimentation.png|center|550]]

**How does this work :**
- At the start <span style='color:#f7b731'>certain bits are negated</span> and if it is <span style='color:#20bf6b'>correct combination</span>, the resulting <b><mark style='background:#f7b731'>6 bits will be all 1</mark></b> and the output all the way below will tell us
- Assume that all <span style='color:#0fb9b1'>don't care terms</span> will be 0
- Based on the output, the <span style='color:#0fb9b1'>decoder circuit</span> will determine the output for the different control signals. 

For example, the table shows that `lw` and `sw` functions have a 1 for the `ALUSrc`, looking at the circuit, there is a <span style='color:#3867d6'>OR</span> gate connecting to `lw` & `sw` output. If the `Opcode` matches to either one, the <span style='color:#fa8231'>one of their outputs will be 1</span> which will result in `ALUSrc` be 1. Else, <span style='color:#fa8231'>both of them are 0</span>, meaning it is not a `lw` or `sw` function, thus `ALUSrc` is 0.

# Execution Cycle
---
In general an <span style='color:#fa8231'>instruction execution</span> is as such :
- **Read contents** of required registers
- **Perform computation** through combinational logic
- **Write results** into memory or register

All of these are performed with in <span style='color:#f7b731'>one clock period</span> (First rising clock edge to the next one) and this is called <span style='color:#0fb9b1'>single cycle execution</span>. However this has some downsides where <span style='color:#eb3b5a'>all instructions are as slow as the slowest one</span>.

There are <span style='color:#fa8231'>2 solutions</span> to this:
1) Multicycle Implementation, where <span style='color:#f7b731'>each step takes one clock cycle</span> instead
2) Pipelining, steps are done in <span style='color:#f7b731'>parallel</span> in one block cycle

**MUX** delay only waits for the chosen input, if the other input has nothing or is waiting then it does not need to wait.