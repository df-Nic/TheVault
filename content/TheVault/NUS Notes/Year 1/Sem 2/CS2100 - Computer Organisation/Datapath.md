---
title: Datapath
Date Created: 2024-02-17
tags:
  - CS2100
  - Hardware
---
# Building a Processor
---
When designing a processor, there are <span style='color:#fa8231'>2 key components</span> :
1) **Datapath**
> Components that <span style='color:#f7b731'>processes data</span> (Arithmetic, logical and memory operations)
2) **Control path**
>Tells <span style='color:#0fb9b1'>Datapath</span>, memory and I/O devices <span style='color:#f7b731'>what to do</span> according to the instructions by sending <span style='color:#0fb9b1'>control signals</span> (From the **opcode**)

# Instruction Execution Cycle
---
There are <span style='color:#fa8231'>5 stages</span> when executing a instruction :
1) **Fetch**
><span style='color:#f7b731'>Get instructions</span> from memory as well as store address of next instruction in PC
2) **Decode**
>Know what operations is required
3) **Operand Fetch**
>Get operands needed
4) **Execute**
>Perform the operation, done in the ALU
5) **Result Write (Store)**
>Store the result of the operation
## Fetching Stage

**Requirements**
- The special register <span style='color:#0fb9b1'>PC</span> (**Program Counter**) is used to <span style='color:#f7b731'>fetch the instruction from memory</span>
- <span style='color:#f7b731'>Increment PC by 4,</span> to get address of <span style='color:#f7b731'>next instruction</span>. With the exception of branch / jump instructions

When passing in an instruction address, the <span style='color:#0fb9b1'>instruction memory</span> will <span style='color:#f7b731'>fetch the corresponding instruction</span>. This instruction will be passed into the next stage to be <span style='color:#f7b731'>executed</span> (<span style='color:#0fb9b1'>Decode</span>).
### Instruction Memory

It is a <span style='color:#0fb9b1'>sequential circuit</span> (Used to store some data) that stores the different to be executed instructions.

Inside this memory, <span style='color:#f7b731'>each instruction is stored</span> in some allocated memory space <span style='color:#f7b731'>as a 32-bit binary</span>. And when the PC has the address of a specific instruction, it will be sent for decoding.
### Adder

It is a <span style='color:#f7b731'>combination logic</span> to implement the a<span style='color:#f7b731'>ddition of 2 numbers</span>. It takes 2 number as input and outputs the addition of both the numbers.

This adder is used to increment the PC by 4.
### Clock Signal

Now, it might seem that reading and updating the PC is done at the same time, since a <b><mark style='background:#f7b731'>PC is a register which implemented by sequential circuits</mark></b>.

However it is not, a special timer named the <span style='color:#0fb9b1'>clock signal</span>, <span style='color:#f7b731'>controls when to update the value in PC</span>.

1 Hz  is 1 cycle per second
1 MHz is $1 \times 10^{6}$ cycles per second
1 GHz is $1 \times 10^{9}$ cycles per second

**How it works :**
![[How Does the Clock Signal Work.png|center|400]]
## Decoding Stage

**Requirements**
- Based on the instruction in binary, <span style='color:#f7b731'>gather the necessary data</span>
- The data includes, knowing what operations and the data from the necessary registers

Once the operation and the operands are gathered, it will be passed into the next stage which is the <span style='color:#0fb9b1'>ALU</span>.

![[Fetch Stage Block Diagram.png|center|600]]

The above is the <span style='color:#fa8231'>block diagram of the fetch stage</span>:
1) Based on the instruction, the corresponding registers specified from in the instructions will be fetched from the <span style='color:#0fb9b1'>register file</span>
2) Their data will then be passed into the next stage which is the <span style='color:#0fb9b1'>ALU</span>
### Register File

It is a <span style='color:#f7b731'>collection of 32 registers, each 32 bit wide</span>. A specific register can be accessed by specifying the register number.

At any instructions it can at <b><mark style='background:#f7b731'>most read 2</mark></b> registers and <b><mark style='background:#f7b731'>write into at most one</mark></b> register.

Aside from what is shown in the image above, there are 2 more addition things
1) **Write data **(Input)
2) `RegWrite` (Signal)

To simply put it, the <span style='color:#0fb9b1'>write data</span> input <span style='color:#f7b731'>store the value to be written</span> into the register in the <span style='color:#0fb9b1'>write register</span> input.

`RegWrite` (**control signal**) on the other hand <span style='color:#f7b731'>tells the register file weather to write or don't write</span> (Indicated by 1 and 0). If it is 0 nothing will happen. This is to <span style='color:#20bf6b'>prevent reading and writing at the same time</span>.
<div style="page-break-after: always;"></div>

#### Decoding a R-format Instruction
![[Decoding R-format Instruction.png|center|500]]
#### Decoding a I-format Instruction

Now, if the <span style='color:#fa8231'>same way of decoding</span> is used for an I-format instruction, there will be <span style='color:#eb3b5a'>2 issues</span> :
1) Our <span style='color:#0fb9b1'>destination register</span> (The register the value will be stored in) will <span style='color:#eb3b5a'>be input for read register </span>
2) The <span style='color:#0fb9b1'>immediate value</span>, will also be in the wrong place as it <b><mark style='background:#f7b731'>needs to be an input into the ALU</mark></b>

![[Decoding I Instructions.png|center|600]]
<div style="page-break-after: always;"></div>

### Multiplexer

<span style='color:#0fb9b1'>Multiplexer</span> or MUX is a device with $n$ number of inputs and have <span style='color:#f7b731'>only 1 output</span>. It determines which to output by using the **control signal**.

If there is $n$ inputs, the <span style='color:#0fb9b1'>control signal</span> will be represented by $log_{2}n$. Thus if the signal in bits represents 1, the the input in line 1 will be outputted.

Thus the above image <span style='color:#fa8231'>uses 2 MUX</span>, to decode R and I instructions. The black MUX determines what goes into write register input. <span style='color:#f7b731'>If it is 0 then the input line A will be the output</span> (`RegDst`).

The red MUX determines what is the input for the <span style='color:#0fb9b1'>ALU</span>, <span style='color:#f7b731'>if it is 1 then the input line D will be the output</span> (`ALUSrc`).
### Sign Extend

This sign extend is to <span style='color:#f7b731'>extend the 16 bit immediate integer into a 32 bit immediate integer</span>

## ALU / Execution Stage

<span style='color:#0fb9b1'>ALU</span> - **Arithmetic Logic Unit**

**Requirements**
- This stage <span style='color:#f7b731'>does the execution</span> of the instructions (Arithmetic, memory operations and branch operations)

Once the computation is done the output will be passed into the <span style='color:#0fb9b1'>Memory Stage</span>.
### ALU
![[ALU Image.png|center|250]]

This <span style='color:#0fb9b1'>ALU</span> consists of 2 32 bit inputs and 2 outputs. The `isZero` just checks if the <span style='color:#f7b731'>result is 0</span>.

`ALUcontrol` is another control signal (4 bit) to <span style='color:#f7b731'>determine the operations</span> to be carried out. It is set based on the `opcode` and `function` field.

| `ALUcontrol` | Operation |
| :----------: | :-------: |
|     0000     |    AND    |
|     0001     |    OR     |
|     0010     |    add    |
|     0110     | subtract  |
|     0111     |    slt    |
|     1100     |    NOR    |
<div style="page-break-after: always;"></div>

#### Branch Instructions
![[Executing a Branch Instruction.png|center|400]]

This is a <span style='color:#f7b731'>special case of a I-format instruction</span>.

The `PCSrc` is <b><mark style='background:#f7b731'>determined by the output from</mark></b> `isZero`, if it is 1 then the value of `PCSrc` is also 1. 

For example if 2 numbers are equal (`beq`) then if they are equal the output is 1. Don't be mislead by it, since it is true, it should take the branch and `PCsrc` must be 1. Therefore `isZero` has to be 1.
## Memory Stage

**Requirements**
- This stage only pertains to the <span style='color:#f7b731'>store and load instructions</span>, the rest will stay idle
- From the memory address calculated in the <span style='color:#0fb9b1'>ALU</span> stage.

Note that the <span style='color:#eb3b5a'>ALU output does not go through this stage</span> but rather it is <span style='color:#f7b731'>passed into</span> the <span style='color:#0fb9b1'>register write</span> stage which is the next part.

![[Memory Stage Block Diagram.png|center|500]]
<div style="page-break-after: always;"></div>

### Data Memory

<span style='color:#0fb9b1'>Data memory</span> store program data which is <span style='color:#f7b731'>different</span> from instruction memory.

Aside from the inputs there are<span style='color:#fa8231'> 2 control signals</span>, they are `MemWrite` and `MemRead`. This restricts to <b><mark style='background:#f7b731'>allow only one write or read instruction</mark></b> and no more.

If `MemWrite` is 1 and `MemRead` is 0, then the value in the input write data will be <span style='color:#f7b731'>stored in the input address</span>.

If `MemWrite` is 0 and `MemRead` is 1 then the <span style='color:#f7b731'>content</span> in the memory address will be <span style='color:#f7b731'>outputted</span>.

If both are 0 then, do nothing, And if <span style='color:#eb3b5a'>both is 1 then something is wrong</span>.

`MemToReg` <span style='color:#f7b731'>determines</span> the <span style='color:#f7b731'>result</span> should come <span style='color:#f7b731'>from the data memory</span>. This is used between non store load instructions.

## Register Write Stage

**Requirements**
- This is the part where the <span style='color:#f7b731'>result</span> of the computation (<span style='color:#0fb9b1'>Memory</span> or <span style='color:#0fb9b1'>ALU</span> stage) is <span style='color:#f7b731'>stored inside some register</span>.
- This applies to most operations <span style='color:#f7b731'>except for store, jump and branch</span> operations and thus these will remain idle.

![[Register Write Block Diagram.png|center|600]]

Basically at the end the value will be passed back to the <span style='color:#0fb9b1'>register file</span> and id there is a need to<span style='color:#f7b731'> store it into a register </span>it will be done in there.
<div style="page-break-after: always;"></div>

# Complete Datapath
---
![[Complete Datapath with Controls Diagram.png|center]]

The above shows the <span style='color:#fa8231'>full data path diagram</span> with the addition of the [[Processor Control|controls circuits]].