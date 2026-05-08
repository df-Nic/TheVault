---
title: Number Systems
Date Created: 2024-01-21
tags:
  - CS2100
  - Binary
---
# Data Representation
---
This is beneficial because <span style='color:#f7b731'>electricity</span> it can be <span style='color:#f7b731'>represented as 2 voltages</span>, 0V for 0 and 5V for 1.

**Units**
- **Bit** (One)
- **Byte** (8 Bits)
- **Nibble** (4 Bits)
- **Word** (Multiples bytes together)

If there are <span style='color:#fa8231'>N bits</span>, then there is a <mark style='background:#f7b731'>total of 2 power of N values</mark> ($2^{N}$). And to <span style='color:#fa8231'>represent M values</span>, $\lceil \log_{2}M \rceil$ number of bits is required. And the range is $2^{N} - 1$ because <span style='color:#f7b731'>0 is included</span>.

<span style='color:#0fb9b1'>ASCII Code</span> or American standard code for information interchange are used to <span style='color:#f7b731'>represent characters as numbers</span>. Now <span style='color:#fa8231'>UFT-8</span> is more commonly used. ASCII uses a standard <span style='color:#f7b731'>8 bit binary with one of the bits used to indicate parity</span> (Number of 1's).

# Base 10 Number System
---
Unlike binary which only uses 2 values, the <span style='color:#0fb9b1'>base 10 system</span> (<span style='color:#0fb9b1'>Decimal</span>), uses <span style='color:#f7b731'>10 digits starting from 0</span> to represent 1 digit. <span style='color:#f7b731'>Another term</span> for this is called the <span style='color:#0fb9b1'>weighted-positional number system</span>.

Also unlike binary, <span style='color:#f7b731'>each position has a weight of power of 10</span> instead of 2 ($10^N$). $$217.5 = 2 \times 10^{2} + 1 \times 10^{1} + 7 \times 10^{0} + 5 \times 10^{-1}$$
<mark style='background:#eb3b5a'>Be careful in C</mark> to always specify the base used ($(100)_{2}$ for base 2). `int x = 0b32` uses <span style='color:#f7b731'>base 10</span> while `int x = 032` <span style='color:#f7b731'>uses octal base 8</span> and `int x = 0x32` <span style='color:#f7b731'>uses hexadecimal</span>!
## Other Number Systems

<mark style='background:#0fb9b1'>Binary</mark> which is <span style='color:#f7b731'>weights in powers of 2</span> with a prefix of 0b
>Digits : 0, 1

<mark style='background:#0fb9b1'>Octal</mark> which is <span style='color:#f7b731'>weights in powers of 8</span>
>Digits : 0, 1, 2, 3, 4, 5, 6, 7

<mark style='background:#0fb9b1'>Hexadecimal</mark> which is <span style='color:#f7b731'>weights with powers of 16</span> with a prefix of 0x
Digits : 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F

In general a <span style='color:#f7b731'>base/radix R</span> will have <mark style='background:#f7b731'>weights in powers or R</mark> and have <mark style='background:#f7b731'>digits from 0 to R minus 1</mark>.
# Base Conversion
---
## Converting to Decimal

First, <span style='color:#f7b731'>take note of the base value</span> denoted by R $100_{x}$. Afterwards each position will have a <span style='color:#f7b731'>weight</span> which can be calculated as such $base^{position - 1}$.

Thus to convert will follow the example below : $$(571.3)_{8} = 5 \times 8^{2} + 7 \times 8^{1} + 1 \times 8^{0} + 3 \times 8^{-1} = 337.375$$
<mark style='background:#0fb9b1'>Most significant bit</mark> - Or MSB is the bit with the highest power or the left most bit

<mark style='background:#0fb9b1'>Least significant bit</mark> - Or LSB is the bit with the lowest power or the right most bit
## Decimal to Binary

### For Whole Numbers

To convert a <span style='color:#f7b731'>whole number</span> to binary, just <mark style='background:#f7b731'>divide it repletely by 2 until the quotient is 0</mark>. The <mark style='background:#f7b731'>remainders are the bits</mark>.

Here is an **example** using the value 43 which will give us a **binary of** $(101011)_{2}$ : ![[Whole Number Binary Conversion.png|center]]
### For Decimals
To convert a <span style='color:#f7b731'>decimal number</span> to binary, just <mark style='background:#f7b731'>multiply it repletely by 2 until the fractional product is 0</mark>. The <mark style='background:#f7b731'>carry are the bits</mark>.

If its infinite decimal, then multiply until the desired number of decimal places (**Closest possible number**).

Here is an **example** using the value 0.3125 which will give us a **binary of** $(.0101)_{2}$ : 
## General Rule for Conversion

![[Decimal Number to Binary.png|center]]

To <span style='color:#fa8231'>convert any decimal to any base of R</span>, the 2 methods above can be used, <mark style='background:#f7b731'>just replace 2 with R</mark>.

To <span style='color:#fa8231'>convert from base a to base b</span>, <mark style='background:#f7b731'>convert base a to decimal first</mark> then repeat using the steps above.
## Binary to bases of 2

There is a fast way to <span style='color:#fa8231'>convert from binary to any base of 2</span>, i.e. 4, 8,16 etc : ![[Binary Fast Conversion.png|center]]
# Representing Negative Numbers
---
There are 2 types of numbers : 
- **Signed** - Includes <span style='color:#f7b731'>positive and negative</span> numbers
- **Unsigned** - Includes <span style='color:#f7b731'>non-negative</span> numbers

## Sign & Magnitude

It is a simple concept where <mark style='background:#f7b731'>one of the bits will represent the sign</mark> it is usually the left most bit):
- **0 for +**
- **1 for -**

For example : $-19$ will be $(10010011)_{sm} \rightarrow -(100100)_{2}$ and to negate $-19$ just <mark style='background:#f7b731'>invert the sign bit</mark>.

**Properties**
1) Largest Value : $+127_{10}$
2) Smallest Values : $(-127)_{10}$
3) Zeros : There is <span style='color:#f7b731'>both a positive and negative 0</span> (100000000 or 00000000)
4) Range (for n bits) : $-(2^{n-1} - 1)$ to $2^{n-1} - 1$

Therefore in general a <span style='color:#fa8231'>n-bit sign and magnitude representation has a range</span> of the following : $$\pm 2^{n-1} - 1$$
**Where :**
- One bit is used for polarity there thus the $n-1$
- And reduce the value of 1 is <span style='color:#f7b731'>because of the 0</span>

<span style='color:#eb3b5a'>One problem</span> to this is that if $00100001 + 10100001 = 11000010$ which <span style='color:#eb3b5a'>is not 0</span> ($33 + - 33$), thus this is bad in arithmetic.
## 1's Compliment

To get the <span style='color:#fa8231'>negated value of x using 1's compliment </span>is through the following : $$-x = 2^{n} - x - 1$$
**Where :**
- $n$ is the number of bits used

Thus for $-12$, using the formula the value will be $243$ and this to <span style='color:#f7b731'>express 243 in binary</span> it will be $11110011_{1s}$.

To <span style='color:#fa8231'>quickly convert</span> is to just <mark style='background:#f7b731'>invert the bits from the value</mark>, for the example above 12 in binary is (00001100).

<mark style='background:#f7b731'>Do not negate the bits if its a positive number</mark>, $14_{10} \rightarrow (00001110)_{2} = (00001110)_{1s}$

**Properties**
1) Largest Value : $+127_{10}$
2) Smallest Values : $(-127)_{10}$
3) Zeros : There is <span style='color:#f7b731'>both a positive and negative 0</span> (00000000 or 11111111)
4) Range (for n bits) : $-(2^{n-1} - 1)$ to $2^{n-1} - 1$

<span style='color:#eb3b5a'>One problem</span> is that <span style='color:#f7b731'>one number is lost in the negative side</span> (-0). Similar to the [[#Sign & Magnitude]] method.

<mark style='background:#fa8231'>For 1's compliment only</mark>, the <mark style='background:#f7b731'>MSB always has a weight of </mark>$-2^{n-1} - 1$
<div style="page-break-after: always;"></div>

## 2's Compliment

To get the <span style='color:#fa8231'>negated value of x using 1's compliment </span>is through the following : $$-x = 2^{n} - x$$**Where :**
- $n$ is the number of bits used

Thus for $-12$, using the formula the value will be $244$ and this to <span style='color:#f7b731'>express 244 in binary</span> it will be $11110100_{2s}$.

Now if the binary of 244 and 12 are added together, it will become, 1 00000000. Notice that the 8 bits are all 0 which means the value is 0. While there is a <span style='color:#0fb9b1'>overflow</span> where there is an <span style='color:#f7b731'>extra bit, which is discarded</span>.

To <span style='color:#fa8231'>quickly convert</span> is to just start from the right <mark style='background:#f7b731'>then keep all bit value until a 1 is reached</mark> then from there on <mark style='background:#f7b731'>invert all the remaining bits</mark> until the <span style='color:#0fb9b1'>most significant bit </span>is reached.

The <span style='color:#fa8231'>proper way </span>of doing this is to, <mark style='background:#f7b731'>invert all the bits then add one</mark>.

**Properties**
1) Largest Value : $+127_{10}$
2) Smallest Values : $(-128)_{10}$
3) Zeros : There is only one o which is <span style='color:#f7b731'>positive 0</span> (00000000)
4) Range (for n bits) : $-2^{n-1}$ to $2^{n-1} - 1$

<mark style='background:#fa8231'>For 2's compliment only</mark>, the <mark style='background:#f7b731'>MSB always has a weight of </mark>$-2^{n-1}$.

For <span style='color:#0fb9b1'>2's compliment</span>, there is a technique called <mark style='background:#0fb9b1'>sign extension</mark>. It allows a binary representation of some <span style='color:#f7b731'>n bits to some m bits</span>;
- If the leading bit is <span style='color:#f7b731'>1</span>, extend the binary to the left by <span style='color:#f7b731'>m-n 1's</span>
- If the leading bit is <span style='color:#f7b731'>0</span>, extend the binary to the left by <span style='color:#f7b731'>m-n 0's</span>

**Example :** 0b1101 -> to 8 bit = 0b11111101 (**0b, tells the computer its in base 2**)

This extension, is <mark style='background:#f7b731'>value-preserving</mark>.

## General Compliment

In general $(r-1)'s$ or <span style='color:#0fb9b1'>radix diminished compliment</span> allows any r compliment conversion, then general formula is $$\text{r-1 Compliment of X } = r^{n} - r^{-m} - X$$
**Where :**
- $n$ is the number of integer digits
- $m$ is the number of decimal digits

**If the base is 2, then 2's compliment is a radix compliment while 1's is a radix diminished complement ($2 - 1 = 1$) by the formula**.
<div style="page-break-after: always;"></div>

# Addition and Subtraction
---
Before carrying on, a common event that can happen is <mark style='background:#0fb9b1'>overflow</mark>. It happens when the <span style='color:#f7b731'>value goes over the maximum number</span> a base can hold.

It can be easily identified in these scenarios :
1) <span style='color:#f7b731'>Adding 2 positive</span> numbers gives a <span style='color:#f7b731'>negative number</span>
2) <span style='color:#f7b731'>Adding 2 negative</span> numbers gives a <span style='color:#f7b731'>positive number</span>
3) At the MSB, the <span style='color:#f7b731'>carry in bit is different from the carry out bit</span> (Excess values)
## With 2's Compliment

For <span style='color:#fa8231'>addition</span> follow these steps :
1) <span style='color:#f7b731'>Perform binary addition </span>, just add the bits up max value is 1, else need to carry forward
2) Ignore the carry out most significant bit
3) <mark style='background:#f7b731'>Check for overflow</mark>, it happens when <span style='color:#f7b731'>'carry in' and 'carry out' of the MSB is different</span> or the <span style='color:#f7b731'>polarity is different</span>

For <span style='color:#fa8231'>subtraction</span> follow these steps :
1) <span style='color:#f7b731'>Get the negation of the number</span> using 2's compliment that is bring subtracted by
2) Follow the addition steps
## With 1's Compliment

For <span style='color:#fa8231'>addition</span> follow these steps :
1) <span style='color:#f7b731'>Perform binary addition </span>
2) If the MSB has a <span style='color:#f7b731'>carry out</span>, <span style='color:#f7b731'>add 1 to the result</span>
3) <mark style='background:#f7b731'>Check for overflow</mark>, it happens when the <span style='color:#f7b731'>polarity is different</span>

For <span style='color:#fa8231'>subtraction</span> follow these steps :
1) <span style='color:#f7b731'>Get the negation of the number</span> using 1's compliment that is bring subtracted by
2) Follow the addition steps
<div style="page-break-after: always;"></div>

## Excess Representation

An <span style='color:#0fb9b1'>excess representation</span>, enables a <span style='color:#f7b731'>evenly distributed </span>positive and negative values. It is called <span style='color:#0fb9b1'>Excess-x Representation</span>, where $x$ tells the number of negative values the representation holds.

| Excess-4 Representation | Value |
| :--: | :--: |
| 000 | -4 |
| 001 | -3 |
| 010 | -2 |
| 011 | -1 |
| 100 | 0 |
| 101 | 1 |
| 110 | 2 |
| 111 | 3 |
It's called excess is because, take -4, if 4 is added the value is 0 which is the binary representation for -4. Thus to get the binary representation, just take the $value + x$ where <span style='color:#f7b731'>x is the excess number</span>, then convert to binary.

Range = $2^{bits}$ - $x$ excess - 1
# Fixed-Point Representation
---
In it, the <span style='color:#f7b731'>number of bits </span>for whole and fractional parts <mark style='background:#f7b731'>are fixed</mark>. This however, comes with a consequence called <span style='color:#eb3b5a'>floating point error</span>.

Take for example (0.01, 0.10, 0.11), these are 0.25, 0.5 and 0.7 respectively and see that it only <span style='color:#f7b731'>increment in 0.25</span>. Thus the <span style='color:#f7b731'>number represented must be rounded up or down to the nearest 0.25</span>. Thus the <mark style='background:#f7b731'>number of bits, range and accuracy are all fixed</mark>.

# Floating-Point Representation
---
It is a alternative to <span style='color:#f7b731'>enable storage of very large or small numbers</span> as the [[#Fixed-Point Representation]] has <span style='color:#f7b731'>limited range</span>.

When <span style='color:#fa8231'>converting</span>, to binary, convert with an <span style='color:#f7b731'>extra bit and then round it</span>. 1 will round up and 0 remains the same.

Computers follow the standard called <mark style='background:#0fb9b1'>IEEE 754</mark>, which <span style='color:#fa8231'>consist of 3 parts</span> :
1) **Sign**
> Positive or Negative and it is <span style='color:#f7b731'>for the mantissa</span>
2) **Exponent**
><span style='color:#f7b731'>Has their own respective sign</span> and thus **THIS** sign is not for this
3) **Mantissa**
>The<span style='color:#f7b731'> fraction part</span> which is <mark style='background:#0fb9b1'>normalised</mark> implicit leading bit (<span style='color:#f7b731'>Left most bit</span>) 1 ($110.1_{2} \rightarrow \text{ normalised } \rightarrow 1.101_{2} \times 2^{2}$)

It is assumed to be <span style='color:#f7b731'>base 2</span> and there are <span style='color:#fa8231'>2 formats</span> :
1) <span style='color:#0fb9b1'>Single-Precision</span> (32 bits)
>**Specifications**: 1 sign bit, 8 exponent bit with bias 127 (excess-127) and 23-bit mantissa
2) <span style='color:#0fb9b1'>Double-Precision</span> (64 bits)
 >**Specifications**: 1 sign bit, 11 exponent bit with bias 1023 (excess-1023) and 52-bit mantissa
 
 **Example of converting to a floating-point representation**
![[IEEE 753 Conversion.png|center]]