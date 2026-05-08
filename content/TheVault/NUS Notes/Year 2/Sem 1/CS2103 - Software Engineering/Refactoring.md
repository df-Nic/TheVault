---
title: Refactoring
Date Created: 2024-09-08
Last Updated: 2025-09-28
tags:
  - CS2103
  - SWE
  - CodeQuality
---

# What is Refactoring
---
As you code we try and <span style='color:var(--mk-color-orange)'>follow these steps</span>:
1) **Make it work**
2) **Make it right**
3) **Make it fast**

But this results in <span style='color:var(--mk-color-red)'>messy code</span> if we **do not clean it frequently** and this is where <span style='color:var(--mk-color-turquoise)'>refactoring</span> comes in.
><span style='color:var(--mk-color-turquoise)'>Refactoring</span> is a the process of <span style='color:var(--mk-color-yellow)'>improving</span> the **programs** internal structure in <span style='color:var(--mk-color-yellow)'>small steps without modifying</span> its external behaviour.

Refactoring is <b><span style='color:var(--mk-color-red)'>not rewriting</span></b> nor is it <b><span style='color:var(--mk-color-red)'>bug fixing</span></b>. Also refactoring can <span style='color:var(--mk-color-red)'>cause regressions</span> (*Code that works no long works after refactoring*). Thus <span style='color:var(--mk-color-yellow)'>regression testing should be carried out</span>. 

So <span style='color:var(--mk-color-orange)'>why</span> do we **refactor**?
1) <span style='color:var(--mk-color-green)'>Spot</span> hidden bugs which can be hard to find
2) <span style='color:var(--mk-color-green)'>Improve performance</span> (*Refactoring simplifies code which can be easier to compile and optimise*)

**Example:**
```Java
void printOwing() {
    printBanner();
    printDetails(getOutstanding());
}
void printDetails(double outstanding) {
	// This 2 lines were originally in the function above
    System.out.println("name:	" + name);
    System.out.println("amount	" + outstanding);
}
```
# How to Refactor
---
Here are some **commonly used** <span style='color:var(--mk-color-turquoise)'>refactoring catalogs</span> (*Techniques*):

**Consolidate Conditional Expression**
>If there are **multiple** `if` statements to check for a condition, try and <span style='color:var(--mk-color-yellow)'>consolidate them into 1 function</span>

**Consolidate conditional**
>For `if-else` statements try and <span style='color:var(--mk-color-yellow)'>compact logic into smaller functions</span>, even the conditional checks.

**Inline functions**
>For **simple logic**, instead of separating into different functions <span style='color:var(--mk-color-yellow)'>put it in 1 function</span>.

**Remove double negative**
>Any double negative should be remove since the <span style='color:var(--mk-color-yellow)'>positive can be used</span>

**Remove magic literals**
>Any **constants** should be <span style='color:var(--mk-color-yellow)'>stored in a variable</span> (`static` or `non-static)

**Nested conditionals with Guard Clauses**
>This is the same concept as the [[Code Quality#Make the Happy Path Prominent|"making the happy path prominent"]]

**Remove flag argument**
>If the **code does 2 things depending on certain command**, then just <span style='color:var(--mk-color-yellow)'>spilt them into 2 functions</span>.

**Reverse Conditional**
>Try and ensure that the **body** inside the `if-else` statement is <span style='color:var(--mk-color-yellow)'>inline with the check condition</span>

**Spilt loop**
>If possible **segregate the logic** of <span style='color:var(--mk-color-teal)'>iterative loops</span> into <span style='color:var(--mk-color-yellow)'>multiple loops</span>:

**Spilt Temporary Variable**
>It is the same concept as [[Code Quality#Do not Recycle Variable Names|"do no recycle variable names"]]

# When to Refactor
---
Certain **code smells** are indications that code might be <span style='color:var(--mk-color-yellow)'>poorly structured or designed</span>.

Here are some <span style='color:var(--mk-color-orange)'>indications on when to refactor</span>:
- **Long method** - Do not exceed **20 lines**
- **Large class** - If possible break large classes into <span style='color:var(--mk-color-purple)'>subclasses</span> or <span style='color:var(--mk-color-purple)'>interfaces</span> 
- **Primitive Obsession** - Try and <span style='color:var(--mk-color-yellow)'>create classes to denote functionality</span> instead of using primitive types (Don't use `int`, `stirng`, etc.)
- **Temporary field** -  For variables that will be used for awhile try and not set them as variables
- **Shotgun surgery** - When altering a class, other classes needs to be recoded.

Therefore try and **periodically refactor** code to <span style='color:var(--mk-color-green)'>prevent pilling up</span>. Also keep in mind **to not over refactor** when the cost cannot be justified.

