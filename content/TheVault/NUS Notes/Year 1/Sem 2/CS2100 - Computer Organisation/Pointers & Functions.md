---
title: Pointers & Functions
Date Created: 2024-01-24
tags:
  - CS2100
  - C
---
# Pointers
---
In <span style='color:#8854d0'>C</span> a <span style='color:#fa8231'>variable has 3 attributes</span> :
1) Name or Identifier
2) Data type
3) <span style='color:#0fb9b1'>Memory address</span> 

This <span style='color:#0fb9b1'>address</span>, tells <span style='color:#f7b731'>where this data is stored in the memory</span>, and to get this address <span style='color:#8854d0'>C</span> has a <span style='color:#f7b731'>address operator</span> `&`!

**Example :**
```C
int a = 123;
prinf("a = %d\n", a); /* This prints the integer */
prinf("&a = %d\n", &a); /* This prints the memory address */
```

The <span style='color:#0fb9b1'>address</span> which is in <span style='color:#f7b731'>hexadecimal format</span> ($x_{16}$), is <span style='color:#f7b731'>decided by the operating system</span> and <span style='color:#f7b731'>varies from run to run</span> as the OS just finds any free memory.

Now a <span style='color:#0fb9b1'>pointer</span> (pointer variable), is a variable that <span style='color:#f7b731'>stores the memory address</span> of some object. Thus this points to a specific memory location. This <span style='color:#0fb9b1'>pointer</span> has it <mark style='background:#f7b731'>own memory address</mark> also!

To declare a <span style='color:#0fb9b1'>pointer</span> use the `*` keyword; `int *a_ptr`, this means that this pointer will contain an <mark style='background:#f7b731'>address that stores an integer</mark>.
## Accessing Memory

Once a <span style='color:#0fb9b1'>pointer</span> has been created, the variable can be indirectly accessed using it. To do this use the `*` keyword; 
```C
int a = 123;
int *a_ptr = &a;
printf("a = %d\n" , *a_ptr); /* Print 123 */
*a_ptr = 456; /* a - 456 */
printf("a = %f\n" , *a); /* Error as a is not a pointer */

(*a_prt)++ /* Increment by 1. Note that * has a lower precidence than ++ */
/* With no () it will increment the address by 1 instead of the value*/
```

<span style='color:#8854d0'>C</span>, will do something called <mark style='background:#0fb9b1'>dereferencing</mark>, which basically <span style='color:#f7b731'>follows the stored address</span> to retrieve the value.
<div style="page-break-after: always;"></div>

## Incrementing Pointers
---
Remember that each data type in <span style='color:#8854d0'>C</span> takes up a <span style='color:#f7b731'>certain number of bytes</span> (x number of 8-bits).

When a pointer is being <span style='color:#fa8231'>incremented</span> `a_ptr ++`, the memory, it will <mark style='background:#f7b731'>increment by the number of bytes</mark> based on the data type.

```C
int a; /* Int used 4 bytes */
int *a_ptr;
a_prt ++; /* Increment by 4 bytes */
a_prt +=; 3 /* Increment by 4 * 3 bytes */
```

<mark style='background:#eb3b5a'>Segmentation fault</mark>, occurs when a <span style='color:#f7b731'>variable is stored in a random memory location that is occupied</span>. This is also known as <span style='color:#0fb9b1'>core dumped</span> which can take up a lot of space.
## Why Use Pointers

It is used when<span style='color:#f7b731'> passing in variables into functions</span> in a program; 
- To pass the addresses of two or more variables to a function so that the function <span style='color:#f7b731'>can pass back to its caller new values</span> for the variables.
- To pass the [[Arrays, String & Structures#Arrays|address of the first element]] of an array to a function so that the function can <span style='color:#f7b731'>access all elements in the array</span>, through <mark style='background:#f7b731'>pointer arithmetic</mark>.

# Functions
---
Similar to <span style='color:#8854d0'>Java</span>, <span style='color:#8854d0'>C</span> has library packages which brings in <span style='color:#0fb9b1'>function prototypes</span>.

Constants, should always be declared as [[Introduction to C#Pre-processor Directives|macro statements]]. To minimise changes.

How to <span style='color:#fa8231'>write a function</span> :
```C
// Template to write a function in C
<return type> <function name> (<arg type> <args>, ...){
	/* code */
	return <variable>;
}
```

What are <span style='color:#0fb9b1'>function prototypes</span>, think of it as function templates which the <span style='color:#f7b731'>program may or may not use in the future</span>. <span style='color:#f7b731'>Without it</span>, the compiler will <span style='color:#eb3b5a'>give a error/warning messages</span>.

A<span style='color:#0fb9b1'> function prototype</span> <span style='color:#fa8231'>includes</span> :
1) **Return type**
2) **Function name**
3) **Data type of parameters**
4) **Parameter Names (Optional)**

**Example :**
```C
/* Program */
#include <stdio.h>
#include <math.h>
#define PI 3.14159

/* Functional Prototypes */
double circle_area(double);

/* Main Function */
int main(void) {
	/* Do something */
	return 0;
}
double circle_area(double diameter) {
	return PI * pow(diameter/2, 2);
}
```

## Pass by Value

In <span style='color:#8854d0'>C</span>, when parameters are passed into functions, the <b><mark style='background:#f7b731'>value gets copied over</mark></b> (**Pass by reference**).

Pointers are useful as, it <span style='color:#20bf6b'>allows functions to directly edit / change variables</span> passed into function.

**Example :**
```C
#include <stdio.h>
void swap(int *, int *);

int main(void) {
	int a, b;
	printf("Enter two integers: ");
	scanf("%d %d", &var1, &var2);
	swap( &a, &b );
	printf("var1 = %d; var2 = %d\n", var1, var2);
	return 0;
}
void swap(int *ptr1, int *ptr2) {
	int temp;
	temp = *ptr1; *ptr1 = *ptr2; *ptr2 = temp;
```

<span style='color:#0fb9b1'>Scope rule</span>, states that <span style='color:#0fb9b1'>local parameters</span> and variables are only <span style='color:#f7b731'>accessible in the function they are declared in</span>.
### Types of Variables

<mark style='background:#0fb9b1'>Local variable</mark> - Variables that are declared in functions are<span style='color:#f7b731'> local to that function</span>.

<mark style='background:#0fb9b1'>Global variable</mark> - They are <span style='color:#f7b731'>variables that can be accessed anywhere</span>, like macro statements.

<mark style='background:#0fb9b1'>Automatic variables</mark> - When a function is called an <span style='color:#0fb9b1'>activation record</span> is created in the <span style='color:#f7b731'>call stack and memory will be allocated</span>. Once it is done, this <span style='color:#f7b731'>record will be removed and memory will be released</span>.

<mark style='background:#0fb9b1'>Static variables</mark> - Variables that <span style='color:#f7b731'>exist in memory</span> even <span style='color:#f7b731'>after</span> the function is <span style='color:#f7b731'>executed</span>.