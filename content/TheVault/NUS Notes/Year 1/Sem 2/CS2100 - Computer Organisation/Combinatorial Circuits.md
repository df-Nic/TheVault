---
title: Combinatorial Circuits
Date Created: 2024-03-17
tags:
  - CS2100
  - Hardware
  - Design
---
# Type Of Circuits
---
![[Types of Circuits.png|Center]]

# Design Methods
---
There are <span style='color:#fa8231'>2 ways to deign a circuit</span> :
- **Gate-level design**, or **SSL** (Using logic gates)
- **Block-level design** (Using functional blocks)

<span style='color:#fa8231'>Objectives</span> in circuit design :
- Reduce Cost (Number of gates or integrated circuits used)
- Increase Speed
- Design simplicity
## Gate-Level Design

Here is a <span style='color:#fa8231'>guideline</span> to start designing :
1) Know the problem
2) Know what are the inputs and expected output
3) Draw out the truth table
4) Express the <span style='color:#f7b731'>outputs in terms of inputs</span> (SOP / POS)
5) Draw the logic diagram

Lets design a <span style='color:#8854d0'>full adder</span>, which is used to add any binary value. It has 3 inputs, $x, y, z$ where $z$ is for the <span style='color:#f7b731'>carry in bit</span>.

![[Gate Level Design.png|center]]

The green boxes are just <span style='color:#8854d0'>half adders</span>, thus a <span style='color:#f7b731'>full adder is just 2 half adders</span>.

<span style='color:#8854d0'>Code converters</span>, takes in some input code and <span style='color:#f7b731'>translate into an equivalent output</span> code.

**For example** : BCD to [[Number Systems#Excess Representation|Excess-3]] code converter

<span style='color:#0fb9b1'>BCD</span> stands for **binary coded decimal**, which only applies for <span style='color:#f7b731'>numbers 0 to 9</span>.

## Block-Level Design

This method is used when the <span style='color:#f7b731'>circuit can be complex</span>. The general method of approach is to decompose the <span style='color:#f7b731'>main problem into smaller sub problems</span> recursively until it is small enough to be solved by blocks.

Example of a <span style='color:#8854d0'>parallel adder</span>, which adds 2 binary numbers together.
![[Parallel Adder Block Design.png]]
<div style="page-break-after: always;"></div>

# Magnitude Comparator
---
![[Magnitude Comparator Circuit Diagram.png|center]]

![[Magnitude Comparator Block Diagram.png|center]]
<div style="page-break-after: always;"></div>

# Circuit Delays
---
For each <span style='color:#0fb9b1'>logic gate</span> where will be some <span style='color:#f7b731'>delays</span>. The time delay for the whole circuit is the <span style='color:#f7b731'>time taken for the longest path in the circuit</span>.

![[Delay In a Parallel Adder.png|center]]

For this example, the <b><mark style='background:#0fb9b1'>propagation delay</mark></b> for the <span style='color:#8854d0'>parallel adder</span> is <span style='color:#f7b731'>proportional to the number of bits</span> it handles.