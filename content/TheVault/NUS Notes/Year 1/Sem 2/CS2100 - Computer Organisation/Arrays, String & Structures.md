---
title: Arrays, String & Structures
Date Created: 2024-01-24
tags:
  - CS2100
  - C
  - DataStructures
---
# Arrays
---
There are various data types which allows the <span style='color:#f7b731'>storage of</span> a <mark style='background:#f7b731'>collection of data</mark> of a specific type.

<span style='color:#0fb9b1'>Arrays</span> in <span style='color:#8854d0'>C</span> are <mark style='background:#f7b731'>homogeneous</mark>, meaning it <span style='color:#f7b731'>stores data of the same type</span>. When declaring, the element type, name and size must be specified, `int intArr[30];`. 

<span style='color:#0fb9b1'>Arrays</span>, take up <mark style='background:#f7b731'>continuous memory locations</mark>, this means that, index 0 to index $n$ of the array, its memory location is side by side, which takes up a [[MIPS#Memory Instructions|word]], but the address will <span style='color:#f7b731'>just point to the 1st byte in the word</span>.

```C
#include <stdio.h>
#define MAX 5

int main(void) {
	int numbers[MAX] = {4,12,-3,7}; /* The last index will be 0*/
	int funny[MAX] = {0}; /* The array will be all 0*/
	int i, sum = 0;
	for (i=0; i<MAX; i++) {
	sum += numbers[i]; /* &numbers[i] also works as it will do dereferencing*/
	}
	
	printf("Sum = %d\n", sum);
	funny = numbers /* Invalid cannot reassign*/
	return 0;
}
```

For <span style='color:#0fb9b1'>arrays</span>, the address of the <span style='color:#fa8231'>variable and the address at index 0</span> will <mark style='background:#f7b731'>always be the same</mark>.

An <mark style='background:#f7b731'>array name is a fixed</mark> (constant) pointer; it points to the first element of the array, and this <mark style='background:#eb3b5a'>cannot be altered.</mark>

```C
int a[3]; /* This is just an example */
printf("%p\n", a); /* ffbff724 */
printf("%p\n", &a[0]); /* ffbff724 */
printf("%p\n", &a[1]); /* ffbff728 */

/* Both of these works to make a function accept an array syntext suggar*/
int function (int *, int){}
int function2 (int [], int){}
```

Note that the <mark style='background:#f7b731'>variables stores the address of the array</mark> not some value. Therefore, when passing into a function, there is <span style='color:#f7b731'>no need to put</span> the `*` keyword and it will pass in the memory address.

Note that, if the <span style='color:#fa8231'>array size is specified as a parameter</span> of a function, <span style='color:#8854d0'>C</span> <mark style='background:#f7b731'>will still compile but it will ignore it</mark>.
<div style="page-break-after: always;"></div>

# String
---
Unlike in other languages, a <span style='color:#0fb9b1'>string</span> in <span style='color:#8854d0'>C</span> is just an <mark style='background:#f7b731'>array of characters</mark>. Where the <mark style='background:#f7b731'>last element of the array must contain the null character</mark>, `'\0'`, which <span style='color:#f7b731'>takes up a space in the array</span> and acts as a <span style='color:#f7b731'>terminator</span> for functions.

This <span style='color:#0fb9b1'>null character</span>, `'\0'` has a <span style='color:#f7b731'>ASCII value of 0</span>, and with this character at the end of the array, it now <span style='color:#f7b731'>can use string functions</span>, and this is called <mark style='background:#0fb9b1'>true strings</mark>.

If there are still extra spaces after the <span style='color:#0fb9b1'>null character</span>, it will be random gibberish.

```C
char fruit [] = "apple"; /* The null terminator is automatically added*/
char fruit [] = {'a', 'p', 'p', 'l', 'e', '\0'};
char fruit [6] = {'a', 'p', 'p', 'l', 'e', '\0'}; /* 6  cause of the null terminator */
```
## Functions for String

### Reading Strings

In <span style='color:#8854d0'>C</span>, there are 2 functions to read string inputs, one is called `fgets()` and the other is `scanf()`.

**How to use :**
```C
fgets(str, size, stdin); /* This reads until size - 1 characters or until a new line */
scanf("%s", str); /* This reads until a white space (' ') is encountered */
```

For the `fgets()` function the <span style='color:#f7b731'>third parameter is the file pointer</span>, thus to <mark style='background:#f7b731'>read from the keyboard</mark> `stdin` is used which means <span style='color:#0fb9b1'>standard in</span>. It also <span style='color:#f7b731'>reads the newline character</span>.

There is however another function called `gets()`, which <span style='color:#f7b731'>reads as much as possible until the user presses 'enter'</span>. This is bad as it is <span style='color:#eb3b5a'>prone to malware injections</span> (Stack overflow exploit) as hackers can write long code as an input to functions.
### Printing Strings

In <span style='color:#8854d0'>C</span>, there are 2 functions to print string inputs, one is called `puts()` and the other is `printf()`.

**How to use :**
```C
puts(str); /* Terminates with a newline (It automatically adds the new line)*/
scanf("%s\n", str);
```
### Length of Strings

The <span style='color:#fa8231'>function to get the length of a string</span> is called `lenstr()`, which get the length of the string, <span style='color:#f7b731'>not including the null character</span>.

To <span style='color:#fa8231'>compare 2 strings</span>, the `strcmp(s1, s2)` can be used. It compares based on the ASCII value (<span style='color:#0fb9b1'>lexicographically</span>). How it works is that it will loop through and minus their ASCII values to see which one is bigger ;
- If its negative if string 1 is smaller than string 2
- If its positive if string 1 is bigger than string 2
- It is 0 if string 1 and 2 are equal

However `strcmp(s1, s2)` might <span style='color:#eb3b5a'>not be safe </span>as if there is <span style='color:#eb3b5a'>no null character, it will continue running</span>. Thus `strncmp(s1, s2, n)` is safer as it <span style='color:#f7b731'>compares up till n characters</span>.

**How to use :**
```C
char fruit [] = {'a', 'p', 'p', 'l', 'e', '\n', '\0'};
int length = lenstr(fruit) /* This will be 6 as it also countes the new line */

char string1[] = "abc";
char String2[] = "abd";
strncmp(string1, string2, 3) /* Returns -1*/
```
### Copy Strings

To <span style='color:#fa8231'>copy a string</span>, the function `strcpy(s1, s2)` can be used. It <span style='color:#f7b731'>copies string 2 into string 1</span>, it is also used to<span style='color:#f7b731'> assign a string to a variable</span>.

If the <span style='color:#fa8231'>array is too small</span>, it will <span style='color:#f7b731'>copy until it is full</span> or until it <span style='color:#f7b731'>reaches a null character</span>.

Similarly it is not safe for the same reasons and `strncpy(s1, s2, n)`, is preferred and $n$ must be <span style='color:#f7b731'>1 less than the array size</span>.

**How to use :**
```C
char fruit [] = {'a', 'p', 'p', 'l', 'e', '\0'};
char fruit_name[];

strncpy(fruit_name, fruit, 5);
```

# Structures
---
Unlike arrays where it only stores homogeneous data, <span style='color:#0fb9b1'>structures</span> allows a collection of <span style='color:#f7b731'>homogeneous data of different types</span>. <span style='color:#fa8231'>To declare one</span>, it will be <span style='color:#f7b731'>above the function prototype</span>.

Think of <span style='color:#f7b731'>structures as classes</span> and since its just a type, <span style='color:#f7b731'>no memory is allocated</span>. How to <span style='color:#fa8231'>create</span> one is as follows :
```C
typedef struct {
int length, width, height;
float amount;
} box_t;

box_t box_one = {1, 1, 1, 2.0}; // To initilize the struct variable

box_one.length = 10; // Similar to classes, use the . to access a member
```
<div style="page-break-after: always;"></div>

To <span style='color:#fa8231'>create an object</span> using user input, <span style='color:#f7b731'>the address must be used</span>;
```C
result_t result1;
printf("Enter student number, score and grade: ");
scanf("%d %f %c", &result1.stuNum, &result1.score,
&result1.grade);
```

Unlike arrays, <span style='color:#f7b731'>structures can be assigned</span>, `struct_1 = struct_2`. It copies over the values from one object to another. In addition, when it is <span style='color:#fa8231'>passed into a function</span>, the <mark style='background:#f7b731'>structure is copied over</mark> as the parameter.

Thus for a <span style='color:#fa8231'>function to modify the structure</span> values, then similar to a variable, just <span style='color:#f7b731'>pass in the pointer</span>, `*object.var = value`. Another way to write that is using `->` for example, `object -> var = value;`, which does not need the `*` keyword.