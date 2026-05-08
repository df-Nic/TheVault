---
title: Introduction to C
Date Created: 2024-01-17
tags:
  - CS2100
  - C
---
# von Neumann Architecture
---
It describes a computer which consist of :
1) **Central Processing Unit (CPU)**
	- Registers
	- A control unit containing an instruction register and program counter
	- An arithmetic / logic unit (ALU)
2) **Memory**
	- <span style='color:#f7b731'>Stores both program and data</span> in a random access memory (RAM)
3) **I/O Devices**
# C Language
---
It is some what similar to <span style='color:#8854d0'>Java</span> in that it is a<span style='color:#f7b731'> strongly typed language</span>.

One additional thing to note is that a <mark style='background:#f7b731'>variable that is not initialized contains an unknown variable</mark> and not 0.

In <span style='color:#8854d0'>C</span>, <span style='color:#3867d6'>boolean</span> values are represents in digits 1 and 0.

On the topic of <span style='color:#3867d6'>boolean</span>, <span style='color:#8854d0'>C</span> has a <span style='color:#0fb9b1'>short-circuit evaluation</span> (Lazy evaluation). Where if in a and operation, if the LHS is false it will not evaluate the RHS.
```C
int a = 0;
int b = 10;
// After C knows a != 0 is false it will not evaluate b/a, this can help save space
if ((a != 0 && b/a > 3)) { 
	printf(...);
}
```
## Programming Structure

In a basic <span style='color:#8854d0'>C</span> program it consist of <span style='color:#f7b731'>4 main parts</span>.

### Pre-processor Directives

The pre-processor consist of the following :

1) Inclusion of<span style='color:#0fb9b1'> header files</span>, these are essentially <span style='color:#8854d0'>C</span> libraries
2) <span style='color:#0fb9b1'>Macro expansions </span>, a global variable that <mark style='background:#eb3b5a'>cannot be reassigned</mark> and is mainly used for <span style='color:#f7b731'>constant values</span>
3) <span style='color:#0fb9b1'>Conditional compilation</span>
<div style="page-break-after: always;"></div>

### Input

Some basic input and output commands : 
```c
#include <stdio.h> /*This is the libary for the printf and scanf functions (Header files)*/
#define pi 3.124 /*constants which cannot be edited (Macro expansions)*/

int age;
double cap; // cumulative average point
printf("What is your age? ");/*This is to print something*/
scanf("%d", &age); /*This is to read user input*/
printf("What is your CAP? ");
scanf("%lf", &cap);
printf("You are %d years old, and your CAP is %f\n", age, cap); /*Outputing with formating*/
```
### Compute

In <span style='color:#8854d0'>C</span> or any programming language, computation is done through <span style='color:#f7b731'>functions</span>. One such function is  `main`.
```C
/* This function is where the program begins */
int main(void) {
	/* Do something */
	return 0;
}
```

In a function, there are **2 types of statements**:
1) <span style='color:#0fb9b1'>Declaration statements</span>, which is used to declare variables
	 Note that <span style='color:#0fb9b1'>standard identifiers</span> (Function names) if <mark style='background:#eb3b5a'>declared as a variable can be overridden</mark> and will no longer act as a function
2) <span style='color:#0fb9b1'>Executable statements</span>, which is the logical statements
#### Switch Statements

Instead of `if else` statements, a switch statement can also be used
```C
/* variable or expression must be of discrete type */
switch ( <variable or expression> ) { 
	case value1: 
		Code to execute if <variable or expr> == value1 
		break; // This break is needed, if not it will execude ALL the code below
	... 
	default: 
		Code to execute if <variable or expr> does not
		equal to the value of any of the cases above
		break; 
}
```
<div style="page-break-after: always;"></div>

### Output

There are a few text formatting which <span style='color:#8854d0'>C</span> allows the users to do:

| Placeholder |               Var Type                |            Function Use            |
| :---------: | :-----------------------------------: | :--------------------------------: |
|     %c      |             char (1 byte)             |         `printf` &`scanf`          |
|     %d      | int (4 bytes or it depends on the MA) |         `printf` & `scanf`         |
|     %f      |   float (4 byte) or double (8 byte)   |              `printf`              |
|     %f      |                 float                 |              `scanf`               |
|     %lf     |                double                 |              `scanf`               |
|     %e      |            float or double            | `printf` (for scientific notation) |
|     %p      |               Pointers                |              `printf`              |
*MA* is machine architecture.

To specify how many <span style='color:#f7b731'>decimal places</span>, use the following place holder `%<d.p>d`.

To print a % character using the `printf` function do `%%`.


