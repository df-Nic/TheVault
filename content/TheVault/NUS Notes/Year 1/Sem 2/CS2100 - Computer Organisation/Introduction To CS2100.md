---
title: Introduction To CS2100
Date Created: 2024-01-16
tags:
  - CS2100
---
# Programming Languages
---
In CS2100, it focuses on <mark style='background:#f7b731'>low level language</mark>, meaning its writing style is similar to what a computer interpretates.

## Language Generations

**How programming languages has developed over the years:** 
1) 1st Generation
	Language is closer to a <span style='color:#f7b731'>machine</span>
2) 2nd Generation
	Assembly language, where it <span style='color:#f7b731'>needs to be translated</span> (Assembled)
3) 3rd Generation 
	It is closer to English language where it <span style='color:#f7b731'>needs to be compiled or interpreted</span>
4) 4th Generation
	Unlike 3rd generation languages (**3GL**) it <span style='color:#f7b731'>requires fewer instructions</span>, mainly used in databases
5) 5th Generation
	Language is mainly <span style='color:#f7b731'>used in AI research</span> such as declarative, function and logical languages

## Scripting vs Programming Languages

| Scripting | Programming |
| :--: | :--: |
| Slower | Faster |
| Interpreted by Machine | Needs to be Compiled |
| JavaScript, Python | C, C++, Java |
However, now with <span style='color:#f7b731'>current hardware capabilities,</span> they are used <span style='color:#f7b731'>interchangeably</span> since programming languages can be executed without being compiled.

The **C** language is a <mark style='background:#f7b731'>imperative procedural language</mark>, it means that the state of the program changes as it <span style='color:#f7b731'>executes line by line</span>.

Where as for <mark style='background:#f7b731'>procedural language</mark>, such as COBOL, is a series of <span style='color:#f7b731'>well-structured procedures</span> which has a systematic order to complete a task or program.

# Abstraction
---
The <span style='color:#f7b731'>process</span> on how a block of <span style='color:#f7b731'>codes gets interpreted and executed by a computer</span> is as follows:

1) Something is coded in a <span style='color:#0fb9b1'>high level language program</span> 
2) Through a <span style='color:#0fb9b1'>compiler</span>, it will be converted into an <span style='color:#0fb9b1'>assemly language</span> like MIPS
3) An <span style='color:#0fb9b1'>assembler</span> is then used to <span style='color:#0fb9b1'>convert it into bits</span>
4) Through an <span style='color:#0fb9b1'>machine interpretation</span>, like a hardware architecture description (Logic), the computer will understand the code
5) Through an <span style='color:#0fb9b1'>architecture implementation</span>, logic circuit description (Logisim) it will execute the code

For CS2100, it focuses on <span style='color:#fa8231'>surface level hardware</span> such as:
- Processor
- Memory
- I/O Systems
- Datapath & Control Design
- Digital Logic Design

There is a link between hardware and software, this is called <mark style='background:#0fb9b1'>Instruction Set Architecture</mark> or **ISA**. It is an interface defines how the <span style='color:#f7b731'>CPU is controlled by the software</span>, <span style='color:#f7b731'>what it can do</span> and <span style='color:#f7b731'>how it does a task</span>.