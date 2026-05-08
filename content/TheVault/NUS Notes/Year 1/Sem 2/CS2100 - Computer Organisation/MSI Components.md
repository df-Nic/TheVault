---
title: MSI Components
Date Created: 2024-03-24
tags:
  - CS2100
  - Hardware
---
# Decoders
---
It is a circuit that converts a binary information of <span style='color:#f7b731'>n input lines</span> to a <span style='color:#f7b731'>maximum of 2<sup>n</sup> output lines</span>.

The <span style='color:#0fb9b1'>decoder</span> is also known as a <span style='color:#0fb9b1'>n-m line decoder</span> or simply n:m or n x m. This is useful to <span style='color:#f7b731'>generate 2<sup>n</sup> minterms of n input variables</span>.

One <span style='color:#fa8231'>functionality</span> of a <span style='color:#0fb9b1'>decorder</span> is that it can be designed to <span style='color:#f7b731'>express a Boolean function</span> in a [[Boolean Algebra#Canonical Forms|sum-of-minterms]] format with it or with <span style='color:#f7b731'>m OR gates</span>.

![[Using a Decoder to Make a Half Adder.png|center]]

These <span style='color:#0fb9b1'>decoders</span> usually come with a <span style='color:#f7b731'>enable control signal</span> denoted by $E$. Its purpose is to <span style='color:#f7b731'>enable to disable the decoder</span>.

If $E = 1$ to enable, it is called a <span style='color:#0fb9b1'>one-enable</span>
If $E = 0$ to enable, it is called a <span style='color:#0fb9b1'>zero-enable</span> (**Used by MSI encoders**)

Thus with the image above just <span style='color:#f7b731'>add one more input to each gate</span> for the enable control signal.

It is possible to construct a <span style='color:#f7b731'>larger decoder with smaller ones</span>.
<div style="page-break-after: always;"></div>

**Making a 3 x 8 Decoder using two 2 x 4 Decoders**
![[3 x 8 Decoder with Two 2 x 4 Decoder.png|center]]

So far the <span style='color:#f7b731'>output</span> for each of the decoder is <span style='color:#f7b731'>normal</span> (**active high outputs**) but in practice it uses something called <span style='color:#f7b731'>negated outputs</span> (**active low outputs**).

**MSI Sample Encoder**
![[MSI Sample Decoder Diagram.png|center]]

There are <span style='color:#fa8231'>many ways to implement a decoder</span> based on the function:
<div style="page-break-after: always;"></div>

Given : $f(Q,X,P) = \sum m(0,1,4,6,7) = \prod M(2,3,5)$

- Using a decoder with active-high outputs with an **OR gate** :
	- f(Q,X,P) = m0 + m1 + m4 + m6 + m7
- Using a decoder with active-low outputs with a **NAND gate** :
	- f(Q,X,P) = (m0' × m1' × m4' × m6' × m7' )'
- Using a decoder with active-high outputs with a **NOR gate** :
	- f(Q,X,P) = (m2 + m3 + m5 )' = M2 × M3 × M5 
- Using a decoder with active-low outputs with an **AND gate** :
	- f(Q,X,P) = m2' × m3' × m5'

# Encoders
---
It is the **opposite of a decoder**, where it takes <b><mark style='background:#f7b731'>exactly one high input</mark></b> while the rest are low and output the <span style='color:#f7b731'>corresponding high input line</span>.

Contains $2^{n}$ input lines and $n$ output lines and it can be <span style='color:#f7b731'>implemented with OR gates</span>.

**Example of an encoder**
![[Encoder Example.png|center]]

## Priority Encoder

The <span style='color:#fa8231'>difference</span> is that a <span style='color:#0fb9b1'>priority encoder</span> <span style='color:#f7b731'>allows inputs with 2 or more high inputs</span>, where the highest priority takes precedence.

But if all inputs are 0, then it is still <span style='color:#eb3b5a'>invalid</span>.
<div style="page-break-after: always;"></div>

**Example using the same truth table as above**
![[Priority Encoder Example.png|center]]

# Demultiplexers
---
<span style='color:#0fb9b1'>Demultiplexers</span> and <span style='color:#0fb9b1'>Multiplexers</span> work together to transmit information from a source to a destination.

A <span style='color:#0fb9b1'>demultiplexer</span> has only <span style='color:#f7b731'>1 input and a set of outputs</span> (**selection lines**). This is designed **identical** to a <span style='color:#f7b731'>decoder with an enable control signal</span>. Thus it can be used in place of it.

# Multiplexers
---
A <span style='color:#0fb9b1'>multiplexers</span> has only <span style='color:#f7b731'>1 output and a set of outputs</span> (**selection lines**).

It <span style='color:#f7b731'>steers one of 2<sup>2</sup> inputs</span> to a single output line, <span style='color:#f7b731'>using n selection lines</span>. Also known as a <span style='color:#0fb9b1'>data selector</span>.

The <span style='color:#fa8231'>output</span> can be expressed as such: 
- $Y = I_{0} \cdot (S_{1}' \cdot S_{0}') + I_{1} \cdot (S_{1}' \cdot S_{0}) + I_{2} \cdot (S_{1} \cdot S_{0}') + I_{3} \cdot (S_{1} \cdot S_{0})$ 
- In terms of **minterms notation**,  $Y = I_{0} \cdot m_{0} + I_{1} \cdot m_{1} + I_{2} \cdot m_{2} + I_{3} \cdot m_{3}$

Therefore, a $2^{n}$ to 1 multiplexer is a n to $2^{n}$ decoder and adding $2^{n}$ input lines into each AND gate.
<div style="page-break-after: always;"></div>

**Example of a multiplexer design**
![[Multiplexer Design.png|center]]

**Using smaller multiplexers to make larger ones**
![[Using 4x1 and 2x1 multiplexers to make 8x1 multiplexer.png|center]]

To <span style='color:#fa8231'>implement a function using a multiplexer</span> is as follows:
![[Function Implementation Using a Multiplexer.png|center]]
<div style="page-break-after: always;"></div>

It is also possible to create the above <span style='color:#f7b731'>using only 1 smaller multiplexer</span> :
![[Using Smaller Multiplexers to Make a Function.png|center]]