---
title: Static Analysis & Type Systems
Date Created: 2025-03-28
Last Updated: 2025-09-28
tags:
  - CS3213
  - Proofs
  - Math
  - SWE/Testing/StaticAnalysis
---
# Static Analysis
---
<b><span style='color:var(--mk-color-turquoise)'>Static analysis</span></b> is the <b><span style='color:var(--mk-color-yellow)'>examination of code without executing</span></b> it.

When we do static analysis our <span style='color:var(--mk-color-orange)'>goal</span> is to:
- **Identify potential errors**
- Ensure adherence to **coding standards**
- **Optimise performance**

<span style='color:var(--mk-color-orange)'>Why use static analysis</span> is because:
- **Early bug detection**
- **Improved code quality**
- **Reduced debugging time**
- **Enhanced maintainability**

There any many <span style='color:var(--mk-color-orange)'>types of static analysis</span>, some are:
- Linters & style checkers (*Check the formatting and practices in the code without a deeper analysis*)
- Data-flow analysis (*Reason about the potential set of values at different points in the execution*)
- Control-flow analysis (*Reasons about the potential orders of executions*)
- **Type checking** (*Verify that the variables are used consistently according to their types.*)
# Type Systems
---
It is a static analyzer that <b><span style='color:var(--mk-color-yellow)'>detects type errors</span></b> (*runtime failures caused by type mismatch*).

It **ensure that a program will not have any undesirable behaviour** (*type mismatch*) by <b><span style='color:var(--mk-color-yellow)'>checking the interactions with different parts before executing</span></b>.

> [!bug] Language systems are unsafe as type errors can happen during runtime

A type system is like a <b><span style='color:var(--mk-color-yellow)'>set of rules</span></b> and if a programs **follows all the rules** then <b><span style='color:var(--mk-color-green)'>it is well typed</span></b>, if not it will be <b><span style='color:var(--mk-color-red)'>ill-types or not typable</span></b>.

> [!quote] Benjamin Pierce, Types and Programming Languages
> A type system is a tractable syntactic method for proving the absence of certain program behaviors by classifying phrases according to the kinds of values they compute.
# Lambda Calculus
---
Common <b><span style='color:var(--mk-color-red)'>programing languages have complex documentation</span></b>, ideally we want a core language with:
- **Essential features to express all computation**
- **No redundance** (*any extra features are syntactic sugars*)

Lambda calculus is <b><span style='color:var(--mk-color-yellow)'>both a programming language and a model for computation</span></b>.

> [!question] Why learn lambda calculus?
> It is the <b><span style='color:var(--mk-color-yellow)'>foundation for functional programming</span></b> (*Lisp, ML, Haskell*).
> 
> It is also used as a code language to <b><span style='color:var(--mk-color-yellow)'>study language theories</span></b>:
> - Type systems
> - Scope & binding
> - Higher order functions
> - Denotational semantics
> - Program equivalence
## Lambda Calculus Syntax 

In general a **function can be expressed** as a <b><span style='color:var(--mk-color-yellow)'>mapping of 1 variable to another</span></b>.

When we denote a **function** we use the <b><span style='color:var(--mk-color-yellow)'>lambda symbol</span></b> ($\lambda$). For **variables** we can <b><span style='color:var(--mk-color-yellow)'>use any alphabet</span></b>.

Thus to **denote a function of a arbitrary input x and returns an output of y** we will write the following:
$$
\lambda x . y
$$
The above is a <b><span style='color:var(--mk-color-turquoise)'>lambda abstraction</span></b>. If we want to apply this function (<b><span style='color:var(--mk-color-turquoise)'>lambda application</span></b>), then we will write the following:
$$
(\lambda x . y) 3
$$
This just means the input is 3 or $x = 3$;

We can also **add in operations and data types as well** for instance:
$$
(\lambda x . (x \times 2)) 3
$$
This just means that $x = 3$ and our output we will take $x * 2$ or $3 * 2 = 6$.

> [!important] The body of $\lambda$ extends as far right as possible
> $\lambda x . M N$ is not $(\lambda x . M) N$ but $(\lambda x . M N)$

> [!important] Function applications are left-associative
> For instance if we have $(\lambda x . \lambda y . x - y) 5 \ 3$ then it will be $((\lambda x . \lambda y . x - y) 5) 3$.
### Higher-Order Functions

They are essentially <b><span style='color:var(--mk-color-yellow)'>functions that return or input another function</span></b>.

> [!warning] $\lambda x . \lambda y . x y$ is not $\lambda x . \lambda y . x \times y$
> The former represents $x \circ y$ while the latter represents $x \times y$.

> [!example] Example of a higher order function
> Lets look at  $(\lambda f . \lambda x . f (f x)) (\lambda y . y + 1) 5$.
> 
> 1) Substitute $f$ with $\lambda y . y + 1$, which we will get $\lambda x . (\lambda y . y + 1) ((\lambda y. y + 1) x) 5$
> 2) Simplify the expression 
> 	- First $\lambda x . (\lambda y . y + 1) ((\lambda y. y + 1) x) 5$ will become $\lambda x . (\lambda y . y + 1) (x + 1) 5$
> 	- Secondly $\lambda x . ((x + 1) + 1) 5$
> 3) Add in the last variable  $((5 + 1) + 1) = 7$

A lambda function **only accepts 1 argument** thus by **chaining functions** is the <b><span style='color:var(--mk-color-yellow)'>process of currying</span></b>.

> [!abstract] Curry & uncurry
> **Currying**, is the profess of transforming a multi input function into a <b><span style='color:var(--mk-color-yellow)'>sequence of functions taking 1 input</span></b>.
> 
> **Uncurrying** is the **opposite** of currying.
### Free & Bounded Variables

**Bounded variables** are your <b><span style='color:var(--mk-color-yellow)'>local variables</span></b>, those within the scope of the function.

**Free variables** on the other hand are like <b><span style='color:var(--mk-color-yellow)'>global variables</span></b>. For example, $\lambda x . (x + y)$, $y$ is the free variable.

When we say a variable $x$ is a free variable in M, it means $x \in fv(M)$.

> [!info] $\alpha$-equivalence
> This term denotes that for <b><span style='color:var(--mk-color-yellow)'>bounded variables the name is interchangeable</span></b> (*placeholder*). ($\lambda x . (x + y)$ *is the same as* $\lambda z . (z + y)$).
> 
> However for <b><span style='color:var(--mk-color-yellow)'>free variables it does matter</span></b>. As global variable x and global variable y can have 2 different values.

We denote a **set of free variables** in $M$ as $fv(M)$. And we have <span style='color:var(--mk-color-orange)'>3 formal definitions</span>:
1) For **variables** (*var*), $fv(x)$ the set of free variables is just $\{x\}$
2) For **lambda abstractions** (*abs*), $fv(\lambda x . M)$ the set of free variables will be $fv(M) \backslash \{x\}$
3) For **lambda applications** (*app*), $fv(M N)$ the set of free variables will be $fv(M) \cup fv(N)$

> [!example] Finding the set of free variables
> Lets say we have $fv((\lambda x . x + y) x)$.
> 
> Firstly it is a lambda expression so we will get $fv(\lambda x . x + y) \cup fv(x)$.
> 
> Now the left term is a abstraction so we will get $(fv(x + y) \backslash \{x\} ) \cup fv(x)$.
> 
> Now putting it all together we will have $\{x, y\} \backslash \{x\} \cup \{x\}$ which will be $\{x, y\}$
## Semantics

### Substitution

> [!info] $\beta$ reduction.
> As previously mentioned, if $(\lambda x . x + 1 ) 4$ we replace $x$ with 4, this is known as a $\beta$ reduction.
> 
> It is to <b><span style='color:var(--mk-color-yellow)'>apply a reduction rule to any sub-term</span></b>.

We can <span style='color:var(--mk-color-orange)'>rewrite this substitution</span> as $(\lambda x . M ) N \rightarrow M[N/x]$. It can be read as replace all $x$ with $N$.

**Rule of thumb** if we are doing $(\lambda x . y)[x/y]$ <b><span style='color:var(--mk-color-yellow)'>rename the bounded variables</span></b> as if we do not we will have an <b><span style='color:var(--mk-color-red)'>unintended name capture</span></b>.

Some of the <span style='color:var(--mk-color-orange)'>rules of substitutions</span> are:
1) $x[N/x]$ is just $N$ because $x$ is a variable and we just let $x = N$
2) $y[N/x]$ is just $y$ because we have no variable named $x$
3) $(M \ P)[N/x]$ is a lambda application it will be $(M[N/x]) (P[N/x])$ 
4) $(\lambda x . M)[N/x]$ will be $\lambda x . M$. Here we only replace free variables since bound variables does not matter
5) $(\lambda y . M)[N/x]$ will be $(\lambda y . (M[N/x])$ if $y \notin fv(N)$
6) $(\lambda y . M)[N/x]$ will be $(\lambda z . (M[z/y][N/x]))$ if $y \in fv(N)$ and $z$ is unused. Here we are just renaming the bound variable
### Reduction Rules

There are a additional <span style='color:var(--mk-color-orange)'>4 rules</span> for reduction, the **first** is our $\beta$ reduction as mentioned previously.

The **second rule** is:
$$
\frac{M \rightarrow M'}{M \ N \rightarrow M' \ N}
$$
The **third rule** is:
$$
\frac{N \rightarrow N'}{M \ N \rightarrow M \ N'}
$$
The **forth rule** is:
$$
\frac{M \rightarrow M'}{\lambda x . M \rightarrow \lambda x . M'}
$$
> We can read the rules as follows, If it is true (*numerator*) then the following will hold (*denominator*).
#### Reduction Strategies

We have <span style='color:var(--mk-color-orange)'>2 strategies</span>:
1) **Normal-order**, where we do the <b><span style='color:var(--mk-color-yellow)'>left most outer-most reduction first</span></b>
2) **Applicative-order**, where we do the <b><span style='color:var(--mk-color-yellow)'>left most innter-most reduction first</span></b>

![[Reduction Strategies Example.png|center]]

For **applicative-order** it <b><span style='color:var(--mk-color-red)'>might not be as efficient</span></b> as normal-order **when the argument is not used**.

They are very similar to **evaluation strategies**
- **Call-by-name** (*similar to normal order*)
- **Call-by-need** (*memorized version of call-by-name*)
- **Call-by-value** (*like applicative-order*)
##### Normal Form

If we can <b><span style='color:var(--mk-color-yellow)'>still reduce</span></b> a lambda expression then it is known as $\beta$-redex (*reducible expression*).

If we <b><span style='color:var(--mk-color-yellow)'>cannot reduce any further</span></b> then it is known as $\beta$-normal form.

> [!abstract] Confluence Theorem
> It is known as the Church-Rosser property, which states that the <b><span style='color:var(--mk-color-yellow)'>terms can be reduced in any order</span></b> **as long as we reach a** $\beta$-**normal form**.

There are some **reductions which does not end** these are known as <b><span style='color:var(--mk-color-turquoise)'>non-terminating reductions</span></b>. Thus this means it will <b><span style='color:var(--mk-color-red)'>not have any normal form</span></b>.


> [!warning] Depending on how you reduce it can be terminating or non-terminating
> ![[Example of Different Reductions Leads to Different Results.png|center]]
# Programming In Lambda Calculus
---
## Boolean Values & Operations

**Boolean values and operations**, we can encode it as such:
1) `True` =  $\lambda x . \lambda y . x$
2) `False`=  $\lambda x . \lambda y . y$

We can interpret $x$ and $y$ as the <b><span style='color:var(--mk-color-yellow)'>return value for the true and false branches</span></b>. So if true return $x$, else return $y$

3) `NOT` = $\lambda b . b \text{ False} \text{ True}$ or it can be $\lambda b . \lambda x . \lambda y . b \ y \ x$ (*accepts 1 input b it will simplify to True or false*)
   
For `Not` lets say $(\lambda b . b \text{ False} \text{ True}) \text{ True}$ if we **do beta reduction** we will get:
1) $(\lambda x . \lambda y . x) \text{ False} \text{ True}$
2) $(\lambda y . \text{ False}) \text{ True}$
3) $\text{False}$ (*Same goes if we did true*)

4) `AND` = $\lambda x . \lambda y . x \ y \ x$
5) `OR` = $\lambda x . \lambda y . x \ x \ y$

Similar to `True` and `False`, here it <b><span style='color:var(--mk-color-yellow)'>takes in 2 Boolean expressions</span></b>.

Now we can combine everything together to make a `if else` statement, we will do $b M N$ where $b$ will be our condition.
## Church Numerals

They are <b><span style='color:var(--mk-color-yellow)'>not really numbers but to apply a function some number of times</span></b>. Its like if we apply function $f$ 2 times we will get $f(f(x))$.

**Examples of church numerals**
- For 0, $\lambda f . \lambda x . x$
- For 1, $\lambda f . \lambda x . f \ x$
- For $n$, $\lambda f . \lambda x . f^{n} \ x$
- For successor (*n + 1*), $\lambda n . \lambda f . \lambda x . f(n \ f \ x)$ or $\lambda n . \lambda f . \lambda x . n \ f( f \ x)$ where $n$ is a church numeral

**Some functions which can be encoded**
- `isZero`, is $\lambda n . \lambda x . \lambda y . n (\lambda z . y) x$. If we let $n$ to be **any of the church numerals** if its 0 it will simplify to true
- Addition is $\lambda n . \lambda m . \lambda f . \lambda x . n f (m \ f \ x)$
- Multiplication is $\lambda n . \lambda m . \lambda f . n(m \ f)$
## Pairs & Tuples

A **pair** `<M, N>` can be denoted as $\lambda f . f \ M \ N$. We will denote the first item in the pair as $\pi_{0}$ and the second item as $\pi_{1}$.

$\pi_{0}$ will be defined as $\lambda p . p (\lambda x . \lambda y . x)$

$\pi_{1}$ will be defined as $\lambda p . p (\lambda x . \lambda y . y)$

Now for a **tuple or list** it the same as a pair just that for a list of size $n$ it will be denoted as $\lambda f . f M_{1} \dots M_{n}$.

To access a element at index $i$ ($\pi_{i}$) it will be $\lambda p . p (\lambda x_{1} \dots . \lambda x_{n} . x_{i})$.
# Simply Typed Lambda Calculus
---
We seen a case where a lambda expression will never terminate. With a <b><span style='color:var(--mk-color-green)'>well-types terms</span></b> in <b><span style='color:var(--mk-color-turquoise)'>STLC</span></b>, it will <b><span style='color:var(--mk-color-yellow)'>always terminate</span></b>.

> [!question] Why types?
> - **Catch simple mistakes early** (`2 + True + "a"` makes no sense)
> - Ensures **type safety** as well type programs will not go wrong (*never enters a meaningless state be it type errors or run-time errors*)
> - **Easer to analyze and optimise** (*compilers can generate better code and access components with a known offset*)

However types <b><span style='color:var(--mk-color-red)'>impose constraints</span></b> on the programmer causing some valid programs to be invalid in a typed language.

Many typed languages have **informal descriptions** of the type systems (*example, in language reference manuals*). A <b><span style='color:var(--mk-color-red)'>fair amount of careful analysis</span></b> is required to **avoid false claims** of type safety (*documentation might not be rigorous*).

A formal presentation of a type system is a <b><span style='color:var(--mk-color-yellow)'>precise specification of the type checker</span></b>. And <b><span style='color:var(--mk-color-green)'>allows formal proofs of type safety</span></b>.

STLC is a <b><span style='color:var(--mk-color-yellow)'>foundation for understanding other common language constructs</span></b>:
- Extend the syntax (types & terms)
- Extend the operational semantics (reduction rules)
- Extend the type system (typing rules)
- Extend the soundness proof (new proof cases)
## Type Systems

Here we can have **typing rules** by <b><span style='color:var(--mk-color-yellow)'>assigning types to terms</span></b>. And **type safety** (*soundness of typing rules*) to <b><span style='color:var(--mk-color-yellow)'>ensure that the program will not go wrong</span></b>.

First we need to **classify functions** using different argument and return types (*explicitly state*).

We also need to **check the types of free variables**. The <b><span style='color:var(--mk-color-yellow)'>types of free variables are the context</span></b>.

Some of these <span style='color:var(--mk-color-orange)'>types are denoted</span> as:
- $\uptau$ (*pronounced as tau*) usually for **Boolean** types
- $\sigma$ usually for **integer** types
- $\sigma \times \uptau$ this is a **product type** this just **represents a pair of values with the corresponding type**
- $\sigma + \uptau$ this is a **sum type** this just **represents a value of either of the 2 types**
- $::=$ is known as definition or "is defined as" (*is like saying let this be this*)
- $\top$ is a **base type** like Boolean or Integers
- $\sigma \rightarrow \uptau$ is a **function type** where the input is a integer and outputs a Boolean (*we can nest this*). Also this is <b><span style='color:var(--mk-color-yellow)'>right associative</span></b>

> [!important] The symbols $\sigma$ and $\uptau$ are not fixed they can be of any type specified

> [!example] Some examples of using types
> - $\lambda x : \uptau . M$ means that the variable x is of type Boolean
> 
> - $M, N ::= x$ means that let $M, N$ be $x$. So now future usage of $x$  will mean $M, N$
## Typing Judgement

A <b><span style='color:var(--mk-color-turquoise)'>typing context</span></b> is a <b><span style='color:var(--mk-color-yellow)'>set of typing assumptions</span></b> we can denote this as $\Gamma$. And if we want to **denote variable M is of type Boolean** we can write it as such $\Gamma \vdash M : \uptau$ (*translate to M is of type $\uptau$ in context $\Gamma$*).

> [!info] If the variable is in the context, it is a well-typed term

We can denote a set of typing assumptions as $\Gamma ::= \ . | \ \Gamma, x : \uptau$  . The **dot** just means an <b><span style='color:var(--mk-color-yellow)'>empty context and is used for closed terms</span></b>. The | is to denote or.
### Typing Rules

1) **Variable rule** (*var*)
$$
\frac{}{\Gamma, x : \uptau \vdash x : t}
$$

It just states that if a type context has $x : \uptau$ for example then $x : \uptau$. 

2) **Application rule** (*app*)
$$
\frac{\Gamma \vdash M : \sigma \rightarrow \uptau \ \land \ \Gamma \vdash N : \sigma}{\Gamma \vdash M N : \uptau}
$$
Essentially it says if we have a function input and variable of the same type we can use it to get an output of some other type.

3) **Abstraction rule** (*abs*)
$$
\frac{\Gamma, x : \sigma \vdash M : \uptau}{\Gamma \vdash (\lambda x : \sigma. M) : \sigma \rightarrow \uptau}
$$
It states that if $M$ is of type $\uptau$ under the context where $x$ is of type $\sigma$. Then $\lambda x : \sigma . M$ implies that the type is $\sigma \rightarrow \uptau$.

**Derivation tree example**

![[Derivation Tree Example.png|center]]

> The **goal** is to make the LHS of $\vdash$ to be empty or to prove that you can derive one expression from another.
## Type System Properties

When designing a type system we want to strike a <b><span style='color:var(--mk-color-yellow)'>balance between soundness and completeness</span></b>.

A type system can <b><span style='color:var(--mk-color-red)'>never by sound and complete</span></b>, if so <b><span style='color:var(--mk-color-yellow)'>choose soundness</span></b> to reduce false positives.
### Soundness

A **sound** type system <b><span style='color:var(--mk-color-yellow)'>never accepts a program that can go wrong</span></b>, <b><span style='color:var(--mk-color-green)'>no false negatives and the language is type safe</span></b>.

> [!tldr] Type safety theorem
>  The reduction of a well typed term either diverges, or terminates in a value of the expected type.

The **formal definition** is that, for any $M, M'$ and $\uptau$, if $. \vdash M : \uptau$ and $M \rightarrow M'$ then $. \vdash M' : \uptau$ and either $M' \in \text{values}$ or $\exists M'' . M' \rightarrow M''$.

We can **prove** this by using <span style='color:var(--mk-color-orange)'>2 key lemmas</span>:
1) **Preservation** (*subject reduction*)

For any $M, M'$ and $\uptau$ if $. \vdash M : \uptau$ and $M \rightarrow M'$ then $. \vdash M' : \uptau$.

> [!info] It means a well tyed terms reduce only to well typed terms of the same type

2) **Progress**

For any $M$ and $\uptau$, if $. \vdash M : \uptau$ then either $M \in \text{Values}$ or $\exists M' . M \rightarrow M'$.

> [!info] It means a well typed term is either a value or can be reduced
### Completeness

A **complete** type system <b><span style='color:var(--mk-color-yellow)'>never rejects a program that can’t go wrong</span></b>, <b><span style='color:var(--mk-color-green)'>no false positives</span></b>.

**Example of our type system is not complete because it is too sound**:
![[Not Complete Type System Example.png|center]]
### Termination

For <b><span style='color:var(--mk-color-yellow)'>every well-typed term in STLC it will always terminate</span></b>.

Thus something like $(\lambda x . x \ x)(\lambda x . x \ x)$ <b><span style='color:var(--mk-color-red)'>cannot be assigned to a type</span></b>.

> [!question] Why can we not assign a type?
> Lets look at the right hand side term lets say it accepts an input if $x \sigma \vdash x : \sigma$. 
> 
> Then we also need a type for $x$ where $x : \sigma \vdash x : \sigma \rightarrow \uptau$, causing $x$ to have 2 types.
