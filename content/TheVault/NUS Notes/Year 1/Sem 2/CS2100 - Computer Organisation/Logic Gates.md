---
title: Logic Gates
Date Created: 2024-03-09
tags:
  - CS2100
  - Hardware
  - ComputerLanguage
---
# Types of Gates
---
**Gate Symbols**
![[Types of Gates & their Symbols.png|center|550]]

**XOR :** $(a' . b) + (a . b')$

With this $a + b = (a \oplus b) + a . b$

**XNOR :** $(x . y) + (x' . y')$
# Logic Circuits
---
In a working circuit, <span style='color:#f7b731'>every input must be connected</span>. And another word for input is called <b><span style='color:#0fb9b1'>Fan-in</span></b>, where each gate can have <span style='color:#f7b731'>2 or more Fan-ins</span>.

**Every Boolean expression** can be <span style='color:#f7b731'>implemented as a logic circuit</span>.
<div style="page-break-after: always;"></div>

**Examples :**
![[Boolean Expressions as Logic Gates.png|center|550]]

Take note that the <span style='color:#f7b731'>same input can be used as many times in the same gate</span>, just branch out the lines.
# Universal Gates
---
These <span style='color:#fa8231'>3 gates</span>, <b><mark style='background:#f7b731'>AND, OR, NOT</mark></b> are <span style='color:#f7b731'>sufficient</span> to <span style='color:#fa8231'>build any Boolean function</span>. It is called the <span style='color:#0fb9b1'>compete set of logic</span>.

However <span style='color:#fa8231'>other gates are used</span> because it is 
- **Useful** (XOR gate for parity bit generation)
- **Economical**
- **Self-sufficient** (NAND and NOR gates which are called <b><span style='color:#0fb9b1'>universal gates</span></b>)

The <span style='color:#f7b731'>NAND or the NOR gate itself</span> can be a <span style='color:#0fb9b1'>complete set of logic</span>.

**Using NAND Gates**
![[NAND Gate to form OR, AND, NOT Gates.png|center|550]]
<div style="page-break-after: always;"></div>

**Using NOR Gates**
![[NOR Gate to form AND, OR, NOT Gates.png|center|550]]

## Relationship Between SOP, POS & Universal Gates

**SOP and NAND Circuits**

A [[Boolean Algebra#Standard Forms|SOP]] can be implemented as a <span style='color:#f7b731'>2-level NAND circuit</span>. <span style='color:#eb3b5a'>Inverters does not add to the levels</span>.

![[SOP as a 2-Level NAND Circuit.png|center|500]]

<div style="page-break-after: always;"></div>

**POS and NAND Circuits**

A [[Boolean Algebra#Standard Forms|POS]] can be implemented as a <span style='color:#f7b731'>2-level NOR circuit</span>. <span style='color:#eb3b5a'>Inverters does not add to the levels</span>.

![[POS as a 2-Level NOR Circuit.png|center|500]]

