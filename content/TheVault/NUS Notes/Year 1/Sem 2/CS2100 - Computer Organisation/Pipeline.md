---
title: Pipeline
Date Created: 2024-04-06
tags:
  - CS2100
  - Hardware
---
# Pipeline Stages
---
The reason for <span style='color:#0fb9b1'>pipelining</span> is to <span style='color:#f7b731'>reduce execution time</span> through the whole process (Multiple tasks).

This <span style='color:#fa8231'>timing is limited</span> by the <span style='color:#f7b731'>slowest stage</span> in the process or <span style='color:#f7b731'>any dependencies</span>.

**5 execution stages**
1) `IF` : Instruction fetch
2) `ID` : Instruction decode and register read
3) `EX` : Execute an operation or calculate address
4) `MEM` : Access an operand in data memory (`lw`, `sw`)
5) `WB` : Write back the result into a register (**R or I Type instructions**)

<span style='color:#fa8231'>Each</span> of these <span style='color:#fa8231'>stages</span> <span style='color:#f7b731'>takes 1 clock cycle</span> and the <span style='color:#fa8231'>flow of data</span> is from <span style='color:#f7b731'>one stage to another</span>, with some exceptions.

In a <span style='color:#fa8231'>non-pipeline environment</span>, <span style='color:#f7b731'>all the stages</span> are <span style='color:#f7b731'>done</span> within <span style='color:#f7b731'>1 clock cycle</span>.

**Example of a Pipelining Process**
![[Pipelining Process Example.png|center]]
<div style="page-break-after: always;"></div>

# Datapath Changes
---
There are come <span style='color:#f7b731'>changes needed to be done</span> in the Datapath to <span style='color:#fa8231'>incorporate the pipeline</span>.

The [[Datapath#Complete Datapath|Datapath]] that was previously mentioned is for <span style='color:#f7b731'>single cycle implementation</span>, where the state of all elements are done at the end of a clock cycle.

But for a <span style='color:#fa8231'>pipeline implementation</span>, there needs to be **5 stages one per cycle** and the <span style='color:#f7b731'>data needs to be stored separately for each stage</span>, as instructions are done simultaneously.

This is done through implementing <span style='color:#0fb9b1'>pipeline registers</span> :
- `IF/ID` : Register between `IF` and `ID`
- `ID/EX` : Register between `ID` and `EX`
- `EX/MEM` : Register between `EX` and `MEM`
- `MEM/WB` : Register between `MEM` and `WB`

<span style='color:#fa8231'>No register</span> after `WB` because the <span style='color:#f7b731'>execution is finished</span>.

## Changes in Datapath

**Modified Datapath**
![[Modified Datapath Diagram.png|center]]

The reason why <span style='color:#fa8231'>write register is passed along</span> is because, if it does not do this then <span style='color:#f7b731'>write register may get over written</span> from subsequent instructions.

The rectangles contains many registers not just 1.
<div style="page-break-after: always;"></div>

From the image above :

**`IF` Stage**
- **Stores the instructions** read from instruction memory (PC)
- **Stores PC + 4**, the next instruction

**`ID` Stage**
- At the <span style='color:#f7b731'>beginning</span> of the cycle
	- It **supplies the registers** for reading and writing
	- **Supplies the 16 bit immediate value** to be sign extended
	- **Sends the PC + 4**
- At the <span style='color:#f7b731'>end</span> of the cycle
	- **Stores** the **data** value read **from registers**
	- Stores **32 bit immediate value**
	- Stores **PC + 4**

**`EX` Stage**
- At the <span style='color:#f7b731'>beginning</span> of the cycle
	- It **supplies data from registers**
	- **Supplies the 32 bit immediate value**
	- **Sends the PC + 4**
- At the <span style='color:#f7b731'>end</span> of the cycle
	- **Stores** the **(PC + 4) + (Immediate * 4)**
	- Stores **ALU Result**
	- Stores `isZero` output
	- Stores data from **data read 2 register**

**`MEM` Stage**
- At the <span style='color:#f7b731'>beginning</span> of the cycle
	- It **supplies (PC + 4) + (Immediate * 4)**
	- Supplies **ALU result**
	- Supplies `isZero` output
	- Supplies data from **data read 2 register**
- At the <span style='color:#f7b731'>end</span> of the cycle
	- **Stores** the **ALU result**
	- Stores memory read data

**`WB` Stage**
- Supplies **ALU result**
- Supplies memory read data
- **Writes** into register if applicable
<div style="page-break-after: always;"></div>

## Changes in Control path

At each stage, there are **different control signals needed**, therefore, the <span style='color:#0fb9b1'>pipeline registers</span> will <span style='color:#f7b731'>store and carry the control signals to each stage</span>.

**Grouping the control signal by stages**
![[Control Signal Grouping for Pipelining.png|center]]


With this, here is the **modified control path** for pipelining :
![[Modified Control Path for Pipelining.png|center]]
<div style="page-break-after: always;"></div>

# Determining Efficiency
---
## Types of Implementation

**There are 3 types of implementation**
![[Types of Implimentation.png|center]]

**Assume the following for the analysis**

|    Instruction    | Inst Mem | Reg Read | ALU | Data Mem | Reg Write | Total |
| :---------------: | :------: | :------: | :-: | :------: | :-------: | :---: |
| **ALU (eg: add)** |    2     |    1     |  2  |    0     |     1     | 6 ns  |
|      **lw**       |    2     |    1     |  2  |    2     |     1     | 8 ns  |
|      **sw**       |    2     |    1     |  2  |    2     |     0     | 7 ns  |
|      **beq**      |    2     |    1     |  2  |    0     |     0     | 5 ns  |
Also assume that **100 instructions** are executed.
### Analysing Single Cycle Processor

The <span style='color:#fa8231'>cycle time</span> can be computed as such :
$$
CT_{seq} = max(\sum^{n}_{k=1} T_{k})
$$
**Where :**
- $T_{k}$ is the time for an operation in **stage** $k$
- $N$ total number of **stages**

The <span style='color:#fa8231'>execution time</span> can be computed as such :
$$
Time_{seq} = I \times CT_{seq}
$$
**Where :**
- $CT_{seq}$ is the <span style='color:#0fb9b1'>cycle time</span>
- $I$ total number of instructions executed

**Therefore :**
- Cycle time is **8ns**
- Execution time is **800ns**
### Analysing Multi Cycle Processor

The <span style='color:#fa8231'>cycle time</span> can be computed as such :
$$
CT_{multi} = max(T_{k})
$$
**Where :**
- $T_{k}$ is the time for an operation in **stage** $k$

The <span style='color:#fa8231'>execution time</span> can be computed as such :
$$
Time_{multi} = I \times CT_{multi} \times \text{Average CPI}
$$
**Where :**
- $CT_{multi}$ is the <span style='color:#0fb9b1'>cycle time</span>
- $I$ total number of instructions executed
- Average CPI, is the **average clock cycle** per instruction

**Therefore :**
- Assuming average CPI is 4.6
- Cycle time is **2ns**
- Execution time is **920ns**
### Analysing Pipeline Processor

The <span style='color:#fa8231'>cycle time</span> can be computed as such :
$$
CT_{pipeline} = max(T_{k}) + T_{d}
$$
**Where :**
- $T_{k}$ is the time for an operation in **stage** $k$
- $T_{d}$ is the **overhead** of the pipeline (Accessing pipeline register)

The <span style='color:#fa8231'>execution time</span> can be computed as such :
$$
Time_{pipeline} = (I + N - 1) \times CT_{pipeline}
$$
**Where :**
- $CT_{pipeline}$ is the <span style='color:#0fb9b1'>cycle time</span>
- $I$ total number of instructions executed
- $N$ is the total number of stages
- $I + N - 1$ is the **total number of cycles**

**Therefore :**
- Assuming $T_{d} = 0.5$
- Cycle time is **2.5ns**
- Execution time is **260ns**

The <span style='color:#fa8231'>ideal speedup</span> is when :
- Every stage takes the same amount of time ($T_{1}$)
- No pipeline overhead
- The number of instructions is much larger than stages

$$
\text{Speedup}_\text{pipeline} = \frac{\text{Time}_\text{seq}}{\text{Time}_\text{pipeline}} = \frac{I \times N \times T_{1}}{(I \times N - 1) \times T_{1}}
$$
If given :
- Total **number of cycles**
- And the **Hz of the clock**

The time can be calculated as such :
$$
\text{Time } = \frac{\text{Total number of cycles}}{\text{Cycles per Second}}
$$
**Where**
- The Hz of the clock will tell the number of cycles per second

# Pipeline Hazards
---
It is <span style='color:#f7b731'>not always possible</span> for an <span style='color:#f7b731'>instruction</span> to be immediately <span style='color:#f7b731'>loaded into the pipeline in every cycle</span>.

There can be problems that prevent the next instruction to be loaded :
**Structural hazards**
> This happens then <span style='color:#eb3b5a'>2 instructions uses the same hardware at the same clock cycle</span>
<div style="page-break-after: always;"></div>

To solve this either :
1) <span style='color:#f7b731'>Stall</span> and start the other instruction at another clock cycle
2) Allocate <span style='color:#f7b731'>2 or more of the same hardware</span>. This is why MIPS has 2 memory 1 for instruction 1 for data to sole this hazard
3) What if 2 instructions are reading and writing into a register. This cannot be spilt into 2 so the solution is to <span style='color:#f7b731'>spilt the cycle into half</span>, first half to write, the other to read

The reason why write is first is because, the <span style='color:#f7b731'>instructions are executed top down</span>, thus the lower **instructions are dependent on those at the top of the pipeline**.

**Data hazards**
> Known as <span style='color:#0fb9b1'>data dependency</span>, happens when <span style='color:#eb3b5a'>2 instructions read and write to the same register</span>.
> <span style='color:#0fb9b1'>Control dependency</span>, is when an <span style='color:#eb3b5a'>instruction depends on another</span> like `beq`

**Types of dependencies**
- **Read-after-write** (RAW) - Also known as true data dependency occurs when 1 later instruction <span style='color:#f7b731'>reads from the same register to be written by an earlier instruction</span>
- Write-after-read (WAR) - <span style='color:#20bf6b'>Do not cause pipeline hazards</span>
- Write-after-write (WAW) - <span style='color:#20bf6b'>Do not cause pipeline hazards</span>

The 2 will cause issues when **instructions is executed out of order** (In modern super scalar processor)

This can be solved by :
1) <span style='color:#f7b731'>Forwarding</span> or <span style='color:#0fb9b1'>bypassing</span> the results from one stage to another and bypassing (replacing) the original data (**Using data from the pipeline**)

**Example of Forwarding**
![[Solving RAW with Forwarding.png|center|600]]

It <span style='color:#fa8231'>can only forward</span> if it is in the <b><mark style='background:#f7b731'>same CC</mark></b> (Clock Cycle) or <b><mark style='background:#f7b731'>in the future</mark></b>.

Forwarding to a branch instruction, need to see if its early (`ID`) or late decision (`EX`)

2) If forwarding does not work then just <span style='color:#f7b731'>stall</span> the pipeline
<div style="page-break-after: always;"></div>

**Example of Stalling**
![[Solving RAW with Stalling.png|center]]

**Control hazards**
> This happens then there is a <span style='color:#eb3b5a'>change in the flow of the program</span> (`beq`, `bne`, `jump`)

This means that the instruction is <span style='color:#0fb9b1'>control dependent</span>. The problem is that the branch decision is done in the `Mem` stage which is <span style='color:#f7b731'>too late</span>.

One way is to <span style='color:#fa8231'>stall</span> until the decision to branch or not has been made, then fetch the corresponding instructions however this can be <span style='color:#eb3b5a'>costly as some clock cycles will be wasted</span>.

On average about 20% of code contains branch / jump instructions which can scale up the cost.

To solve this by :
1) <span style='color:#f7b731'>Early Branch Resolution</span>
>The aim of this is to make the decision in a earlier stage (`ID`) instead of `MEM`.

The modifications to be made are :
- **Move the branch target address calculation** to the `ID` stage
- **Move the register comparison** to the `ID` stage and do not use the ALU

![[Early Branch Resolution Example.png|center]]

This reduces a 3 clock cycle delay to a <span style='color:#f7b731'>1 clock cycle delay</span>.

However one issue is if what if the `beq`, `bne`, `jump` instruction is after a R-type or a load word instruction, then the `bne` instruction for example the `ID` stage will need to be <span style='color:#eb3b5a'>stalled for more than 1 cycle</span>, since it needs to wait for `MEM` stage to be executed or `EX`.

2) <span style='color:#f7b731'>Branch Prediction</span>
>The idea is to <span style='color:#f7b731'>predict what will be the next instruction</span> and load it into the pipeline.

A simple prediction is to predict that the <b><mark style='background:#f7b731'>branch will not be taken</mark></b>. It is <span style='color:#20bf6b'>true</span> then there is <span style='color:#20bf6b'>no stalling needed</span>, if <span style='color:#eb3b5a'>false</span> then <span style='color:#eb3b5a'>flush the successor instruction</span> (Instruction the label is at) into the pipeline.

**Example of flushing**
![[Wrong Prediction in Pipeline.png|center]]

**What it looks like in the pipeline**
![[Calculating Total Cycles Needed for Branch Prediction.png|center]]

The above example uses <span style='color:#0fb9b1'>early branch resolution</span>.

3) <span style='color:#f7b731'>Delayed Branching</span>
>Branch decision takes $X$ number of cycle to be know, thus it needs $X$ cycles of stalling. Thus the idea is to <span style='color:#f7b731'>move non-control dependent instructions</span> to these $X$ slots, this is known as <span style='color:#0fb9b1'>branch-delay slots</span>.
<div style="page-break-after: always;"></div>

**Example of delayed branching**
![[Delayed Branching Example.png|center]]

The <span style='color:#eb3b5a'>worst case</span> is that <span style='color:#f7b731'>no such instruction can be found</span>, in this situation a no-op (nop) instruction will be in the branch-delay slot which <span style='color:#f7b731'>tells the pipeline to do nothing</span>.

The re-ordering is done by the compiler through program optimization. The <span style='color:var(--mk-color-yellow)'>re-ordering can only be on instructions above not below</span>.

For **early branching** just need to find <span style='color:#f7b731'>1 instruction</span>, as for **late branching** need to find <span style='color:#f7b731'>3 instructions</span>.

