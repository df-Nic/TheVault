---
title: Sequential Logic & Memory
Date Created: 2024-03-29
tags:
  - CS2100
  - Hardware
---
# Sequential Circuits
---
There are <span style='color:#fa8231'>2 types</span> of sequential circuits :
1) **Synchronous** - Output changes at a <span style='color:#f7b731'>specific time</span>
2) **Asynchronous** - Output changes at <span style='color:#f7b731'>any time</span>

These circuits <span style='color:#f7b731'>depend on memory element</span> which are made out of <span style='color:#0fb9b1'>multivibrators</span> :
1) **Bistable** (2 stable states)
2) **Monostable** or **one-shot** (1 stable state)
3) **Astable** (no stable state)

For now lets focus on <span style='color:#fa8231'>bistable logic devices</span>, which has <span style='color:#fa8231'>2 methods</span> to change its state :
1) **Latches**
2) **Flip-flops**
# Memory Element
---
It is a device that can <span style='color:#f7b731'>remember a value indefinitely</span> or <span style='color:#f7b731'>change</span> on command <span style='color:#f7b731'>based on inputs</span>.

There are come which has a [[Datapath#Clock Signal|clock]] which its commands are only <b><mark style='background:#f7b731'>effective at a particular time</mark></b>.

**Visualisation of a clock**
![[Clock Example.png|center]]

Positive pulses / edges are 1 while negative pulses / edges are 0.
<div style="page-break-after: always;"></div>

With a clock, there are <span style='color:#fa8231'>2 types of activation / triggering</span> :
1) **Pulse Triggered**
- Uses <span style='color:#f7b731'>latches</span>
- It is ON when it is 1 and OFF when it is 0 (It is possible for the complete opposite)

2) **Edge Triggered**
- Uses <span style='color:#f7b731'>flip-flops</span>
- <b><span style='color:#0fb9b1'>Positive edge triggered</span></b> - ON from 0 to 1
- <b><span style='color:#0fb9b1'>Negative edge triggered</span></b> - ON from 1 to 0

In general, the <b><mark style='background:#f7b731'>flip-flops makes up the memory</mark></b> by remembering past states.
# Latches
---
## S-R Latches

It contains <span style='color:#fa8231'>2 inputs</span> :
1) $S$ for <span style='color:#f7b731'>set</span>
2) $R$ for <span style='color:#f7b731'>reset</span>

It also has <span style='color:#fa8231'>2 complementary outputs</span> $Q$ and $Q'$ :
1) $Q$ = HIGH, the latch is in a <span style='color:#2d98da'>SET state</span>
2) $Q$ = LOW, the latch is in a <span style='color:#2d98da'>RESET state</span>
3) $Q'$ is the <span style='color:#f7b731'>opposite</span> of what $Q$ is

An **active-high input S-R latch** also known as a <span style='color:#0fb9b1'>NOR gate latch</span> :
- $Q$ is LOW (<span style='color:#2d98da'>RESET state</span>) if $R$ is HIGH and $S$ is LOW
- $Q$ is HIGH (<span style='color:#2d98da'>SET state</span>) if $R$ is LOW and $S$ is HIGH
- $Q$ does not change if both $R$ and $S$ are LOW
- $Q$ is <b><span style='color:#eb3b5a'>invalid</span></b> if both $R$ and $S$ are HIGH as $Q$ and $Q'$ <span style='color:#f7b731'>will be 0</span>.

There is also a **active-low input S-R latch** which uses NAND gates and is the <span style='color:#f7b731'>complete opposite</span> of a active-high S-R latch.

The **general formula** for $Q(t+1) = S + R' \cdot Q$ 
### Gated S-R Latch

Unlike the standard S-R latch, there is <span style='color:#f7b731'>an addition enable input</span> ($EN$) and <span style='color:#f7b731'>2 more NAND gates</span>.

Outputs change when $EN$ is **high** (1). If it is 0, then both $S$ and $R$ will be 1 no matter the input.

The $EN$ changes a <span style='color:#f7b731'>active low latch into a active high</span>.
<div style="page-break-after: always;"></div>

## Gated D Latch

For this, <span style='color:#f7b731'>instead of using</span> $\color {#f7b731} {R}$, <span style='color:#f7b731'>instead use</span> $\color {#f7b731} {D'}$ which is just $S$ but renamed to $D$ and in addition to the $EN$ enable input.

This <span style='color:#0fb9b1'>D latch</span>, <span style='color:#20bf6b'>eliminates the invalid state</span> which the **S-R latch has**.
# Flip-flops
---
They are <span style='color:#f7b731'>synchronous bistable devices</span>, whose output changes depending on the clock, either on the rising or falling edge. Registers uses it.

In a block diagram, most inputs shown are pulse triggered, but for an <span style='color:#f7b731'>edge triggered device</span> it is <span style='color:#f7b731'>denoted with</span> a $\color {#f7b731} {>}$, which also denotes a **positive edge triggered flip-flop**.

If there is a <span style='color:#f7b731'>negator</span> then it will be a **negative edge triggered flip-flop**. These are known as <span style='color:#0fb9b1'>triggering edge</span>.
## S-R flip-flop

Given a <span style='color:#fa8231'>positive edge-triggered S-R flip-flop</span> :
- $Q$ is LOW (<span style='color:#2d98da'>RESET state</span>) if $R$ is HIGH and $S$ is LOW
- $Q$ is HIGH (<span style='color:#2d98da'>SET state</span>) if $R$ is LOW and $S$ is HIGH
- $Q$ does not change if both $R$ and $S$ are LOW
- $Q$ is <b><span style='color:#eb3b5a'>invalid</span></b> if both $R$ and $S$ are HIGH as $Q$ and $Q'$ <span style='color:#f7b731'>will be 0</span>.

And a **negative edge-triggered** will be the <span style='color:#f7b731'>complete opposite</span>.

### D flip-flop

And same as before, $R$ will become $S'$ but $S$ is now denoted as $D$.

This <span style='color:#0fb9b1'>D flip-flip</span>, <span style='color:#20bf6b'>eliminates the invalid state</span> which the **S-R flip-flop has**.

## J-K flip-flop

Unlike the **S-R flip-flop**, the outputs for $Q$ and $Q'$ are <span style='color:#f7b731'>fed back to the pulse-steering NAND gates</span>.
- $Q$ is LOW (<span style='color:#2d98da'>RESET state</span>) if $J$ is HIGH and $K$ is LOW
- $Q$ is HIGH (<span style='color:#2d98da'>SET state</span>) if $J$ is LOW and $K$ is HIGH
- $Q$ does not change if both $J$ and $K$ are LOW
- $Q$ is <b><span style='color:#20bf6b'>still valid</span></b> if both $J$ and $K$ are HIGH as this will cause a <span style='color:#f7b731'>toggle</span> where the state will go from low to high and vice versa.
<div style="page-break-after: always;"></div>

**J-K flip-flop diagram**
![[J-K Flip-flop diagram.png|center]]

### T flip-flop

Which is also known as a toggle flip-flop, is the <span style='color:#f7b731'>same concept as a D flip-clop</span>.

Where same as before, $K$ will become $J'$ but $J$ is now denoted as $T$.

# Asynchronous Inputs
---
Now what was mentioned above are <span style='color:#f7b731'>all synchronous inputs</span> but for <span style='color:#0fb9b1'>asynchronous inputs</span>, the state is <span style='color:#f7b731'>independent of the clock</span>.

There can be 2 possible additional inputs such as **preset (PRE) and clear (CLR)** or **direct set (SD) and direct reset (RD)**.

When PRE is HIGH then $Q$ is <span style='color:#f7b731'>immediately</span> set to HIGH and when CLR is high instead then it will be LOW.

Normal operations occurs when both PRE and CLR are both LOW.
<div style="page-break-after: always;"></div>

**Example of a Asynchronous inputs**
![[Example of a Asynchronous Inputs.png|center]]

Input with a bar like, $\overline{PRE}$ means it is <b><mark style='background:#f7b731'>active low input</mark></b>, meaning it has to be set to 0 to be active.

# Analysing Sequential Circuits
---
The goal is to <span style='color:#f7b731'>determine the behaviour</span> by <span style='color:#f7b731'>deriving its state table</span> and thus its state diagram.

This requires the <span style='color:#f7b731'>state equations and the output functions</span> using $A(t)$ and $A(t+1)$ or $A$ and $A^{+}$.

The <span style='color:#fa8231'>size of a state table</span> is $2^{m + n}$ where, $m$ is the number of flip-flops and $n$ is the number of inputs.

**Finding the state equation and output function**
![[Finding State Equation & Output Function.png|center]]
<div style="page-break-after: always;"></div>

**Form the state table**
![[State Table Example.png|center]]

**Formulate the State Diagram**
![[State Diagram Exmaple.png|center]]
<div style="page-break-after: always;"></div>

# Building Sequential Circuits
---
When designing sequential circuits, an <span style='color:#0fb9b1'>excitation table</span> is used.

A <span style='color:#0fb9b1'>excitation table</span>, shows that is needed to <span style='color:#f7b731'>transition from present state to next state</span>.

**Excitation tables**
![[Excitation Table.png|center|400]]

## Making the Excitation Table

With the state diagram, the excitation table can be created, the below shows an example using only the **J-K flop-flop**.

![[Making the Excitation Table.png|center]]

Next with the excitation table, make the **flip-flop input functions**. This has to be done for <span style='color:#f7b731'>all next state outputs and normal outputs</span>.

![[Forming the Flip-flop Functions.png|center]]

Now what if there are <span style='color:#f7b731'>missing states</span>, then just fill in the rest as a <span style='color:#f7b731'>don't care bit</span>.

Once the [[Simplification#K-Maps|K-map]] is completed then the **circuit can be drawn**.

![[Circuit Diagram based on K-map.png|center]]
<div style="page-break-after: always;"></div>

# Memory
---
<span style='color:#0fb9b1'>Memory</span> just stores programs and data.

**Measurements**
- 1 KB (Kilo-Byte) is $2^{10}$ bytes
- 1 MB (Mega-Byte) is $2^{20}$ bytes
- 1 GB (Giga-Byte) is $2^{30}$ bytes
- 1 TB (Tera-Byte) is $2^{40}$ bytes

Some <span style='color:#20bf6b'>desirable properties</span> for memory are :
- Fast access
- Large capacity
- Cheap
- Non-volatile

However **most memory devices** <span style='color:#f7b731'>do not possess all the desirable properties</span>.

As mentioned previously, if there are $k$ addressing bits, then there are $2^{k}$ addresses. However, what is not mentioned is that the <span style='color:#f7b731'>address is passed through the address bus which has</span> $k$-bits (Wire).

These <span style='color:#fa8231'>address are generated</span> by a register known as the <span style='color:#0fb9b1'>memory address register</span>.

The data stored from memory is stored under the <span style='color:#0fb9b1'>memory data register</span> in the processor which is <span style='color:#f7b731'>transferred through a data bus</span> of $n$-bits.

There is also a <span style='color:#0fb9b1'>control line</span> which <span style='color:#f7b731'>instructs weather to read or write from memory</span> ($R/\bar{W}$). And usually there is one more control signal which is called <span style='color:#0fb9b1'>memory enable</span> as long as <span style='color:#f7b731'>this is 0 nothing will happen</span>.

## Memory Cell

There are <span style='color:#fa8231'>2 types of RAM</span> (**Random Access Memory**):
-  Static RAM - <span style='color:#f7b731'>Used in flip-flops</span> as memory cells
- Dynamic RAM - <span style='color:#f7b731'>Uses capacitor charges</span> to represent data which is <span style='color:#20bf6b'>simpler in circuity</span> by have to be <span style='color:#eb3b5a'>constantly refreshed</span>

Each memory cell <span style='color:#f7b731'>holds 1 bit</span> and its logic diagram looks as such :
<div style="page-break-after: always;"></div>

**Logic Diagram of a Memory Cell**
![[Memory Cell Logic Diagram.png|center|400]]

**Example of Memory**
![[Example of Memory.png|center]]