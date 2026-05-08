---
Title: Functions
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1231S
  - Math/Logic
---
# Functions
---
**Functions**
> It is an <span style='color:#f7b731'>assignment of each element in the set of X</span> to <span style='color:#f7b731'>exactly one element of Y</span>. It is denoted as $f : X \rightarrow Y$

Symbolically: 

F1 : $\forall x \in X \ \exists y \in Y, (x,y) \in f$
F2 : $\forall x \in X \ \forall y_{1}, y_{2} \in Y (((x,y_{1}) \in f \land (x,y_{2}) \in f) \rightarrow y_{1} = y_{2})$
	This means that the y values in F1 are <span style='color:#f7b731'>unique</span>.
F3 : $\forall x_{1}, x_{2} \in X (x_{1} = x_{2} \rightarrow f(x_{1}) = f(x_{2}))$

From the above:
F1 $\land$ F2 $\iff$ F3

Alternatively: 
1) $\forall x \in X \ \exists ! \ y\in Y, (x,y) \in f$  
2) $\forall x \in X \ \exists y \in Y, \{y\} = \{b | (x,b) \in f\}$
	{y} will be a <span style='color:#0fb9b1'>singleton set</span>.
3) $\{ (a,b) : (a,b) \in (A \times B) \land b = f(a) \}$

A <mark class="hltr-orange">function is a relation but not all relations is a function</mark>

Properties of a function:
1)  Every element in the <span style='color:#0fb9b1'>domain</span> X <span style='color:#f7b731'>must</span> be mapped to <span style='color:#f7b731'>at least one value</span> in the co-domain Y
2)  <span style='color:#f7b731'>No single element</span> in the <span style='color:#0fb9b1'>domain</span> X can <span style='color:#f7b731'>map to 2 or more elements</span> in the <span style='color:#0fb9b1'>co-domain</span> Y. 

**Argument**
> Is the x value, it is also called the input or <span style='color:#0fb9b1'>preimage</span>

The <span style='color:#0fb9b1'>domain</span> will be $Domain = A$

**Output**
> It is the y value, it is also called the <span style='color:#0fb9b1'>image</span>

The <span style='color:#0fb9b1'>co-domain</span> will be $\text{Co-Domain} = B$
The <span style='color:#0fb9b1'>range</span> will be $Range \subseteq \text{Co-domain}$ which is the setwise image of X under f
	$\{y \in B : y = f(x) \text{for some} x \in A\}$

**Setwise Function**
> It is the same as a function but it works for a set of values instead of one value only it is denoted as $f^{-1}(a)$

Symbolically: 
- If A $\subseteq$ X then $f(A) = \{f(x) : x \in A\}$ 
	This is called a <span style='color:#f7b731'>setwise image function</span>, which produces a set of <span style='color:#0fb9b1'>images</span>
- If B $\subseteq$ Y then $f^{-1}(B) = \{x \in X : f(x) \in B\}$ 
	This is not a inverse function it is called a <span style='color:#f7b731'>setwise preimage function</span>, which produces a set of <span style='color:#0fb9b1'>preimages</span>

**Congruence Modulo n**
> This relation can be defined as a function $\Bbb Z_{n}$ where n is some value 

Then the addition and multiplication on this function is as follows:

If $[x], [y] \in \Bbb Z_{n}$
1)  $[x] + [y] = [x + y]$
2)  $[x] \times [y] = [x \times y]$
# Sequences
---

**Sequences (Infinite length)**
> A sequence $a_0,a_1,a_{2,}\dots$ can be represented by a function a whose domain is $Z_{\ge 0}$ that satisfies $a(n)=a_n$ for every $n \in Z_{\le 0}$

**Fibonacci Sequence**
> The Fibonacci sequence $F_0,F_1,F_{2}, \dots$ is defined by setting, for each $n \in Z_{\ge 0}$, $F_0=0$ and $F_1=1$ and $F_(n+2) = F_(n+1)+F_n$.

**String**
> Let A be a set. A string or a word over A is an expression of the form $a_0 a_1 a_{2}, \dots a_{l-1}$ where $l \in Z_{\ge 0}$ and $a_0,a_1,a_2,\dots,a_{l-1} \in A$

Here $l$ denotes the <span style='color:#f7b731'>length of the string</span>. The <span style='color:#0fb9b1'>empty string</span> is a string of length 0 denoted by $\varepsilon$

## Equality of Sequences

Given any two sequences $a_0,a_1,a_2,\dots$ and $b_0,b_1,b_2,\dots$ defined by the functions $a(n)=a_n$ and $b(n)=b_n$ respectively for every $n \in Z_{\ge 0}$, we say that the two sequences are equal if and only if $a(n)= b(n)$ <mark class="hltr-orange">for every</mark> $n \in Z_{\ge 0}$

$A^\infty$ or $Seq(A)$ denote the set of all (infinite) sequences over A = is a relation with type $A^\infty \times A^\infty$

Symbolically: $\exists n \in Z . Z_{\ge n} \rightarrow A$ where n is a <span style='color:#f7b731'>unbounded domain</span> but the range will be some value in the set $A$
## Equality of Strings

Given any two strings $s_1= a_0 a_1 a_2 \dots a_{l-1}$ and $s_2=b_0 b_1 b_2 \dots b_{l-1}$  where $l \in Z_{\ge 0}$, we say that $s_1=s_2$ if and only if $a_i=b_i$ for all $i \in \{0,1,2,…,l-1\}$.

$A^*$ or $Str(A)$ denote the set of all (finite) strings over A = is a relation with type $A^* \times A^*$

Symbolically: $\exists m \in Z, l \in Z_{\ge 0} . [m,m+l) \rightarrow A$ where m is a <span style='color:#f7b731'>unbounded domain</span> but the range will be some string in the set $A$

## Equality of Functions

Two functions $f:A \rightarrow B$ and $g:C \rightarrow D$ are equal, i.e. $f=g, \iff A=C \text{ and } B=D$, and $f(x)=g(x)$  $\forall x \in A$.

1)  Ensure that the <span style='color:#f7b731'>domain for both the functions are equal</span>
2)  Ensure that the <span style='color:#f7b731'>range for both the functions are equal</span>
3)  Check if <mark class="hltr-orange">every input for each domain will compute the same value</mark> for both functions

# Properties of Functions

**Injection**
> It means that the function has a <span style='color:#f7b731'>one to one correspondent</span> between input and output

Symbolically: $\forall x_{1}, \forall x_{2} \in X (f(x_{1}) = f(x_{2}) \rightarrow x_{1} = x_{2}$ 

The difference between <span style='color:#0fb9b1'>injection</span> and the property of a function is that, injection means that for all of x, only <span style='color:#f7b731'>one unique x can be mapped to one unique y</span>.

It is <mark class="hltr-red">not injective</mark> if $\exists x_{1},x_{2} \in X (f(x_{1)} = f(x_{2}) \land x_{1} \neq x_{2})$ 

**Surjection**
> Every element in the <span style='color:#0fb9b1'>co-domain</span> is at least mapped to one <span style='color:#0fb9b1'>preimage</span>, thus <mark class="hltr-orange">range = co-domain</mark>

Symbolically: $\exists y \in Y, \exists x \in X (y = f(x))$ 

It is <mark class="hltr-red">not surjective</mark> if $\exists y \in Y, \forall x \in X (y \neq f(x))$

**Bijection**
> A function is a bijective if and only if it is <mark class="hltr-orange">both a injection and surjection</mark>

Symbolically: $\forall y \in Y, \exists !x \in X (y = f(x))$

All functions which are <span style='color:#0fb9b1'>bijective</span> there will <mark class="hltr-orange">always be a inverse function</mark>
## Inverse Functions

For a inverse function to exist the function <mark class="hltr-orange">must be a bijective function</mark>. This inverse function is denoted as $f^{-1}$ and it <span style='color:#f7b731'>reverts each element in the co-domain back to the domain it came from</span>.

Symbolically: $\forall x \in X, \forall y \in Y (y = f(x) \iff x = g(y))$ 

**Uniqueness of Inverses**
> If there are 2 functions which are an inverse of a function f, then <span style='color:#f7b731'>both the functions are the same</span>

And this inverse function is also <span style='color:#0fb9b1'>bijective</span>

## Composition of Functions

Let $f : X \rightarrow Y$ and $g : Y \rightarrow Z$

Then the composition of the functions $g \circ f : X \rightarrow Z$ is as follows $(g \circ f)(x) = g(f(x)) \forall x \in X$ 

If 2 functions f and g are:
1)  <span style='color:#0fb9b1'>Injective</span> then the composition $g \circ f$ will also be Injective (Theorem 7.3.3)
2)  <span style='color:#0fb9b1'>Surjective</span> then the composition $g \circ f$ will also be Surjective (Theorem 7.3.4)
3)  <span style='color:#0fb9b1'>Bijective</span> then the composition $g \circ f$ will also be Bijective (Not Confirmed XD)
### Identity Functions

The <span style='color:#0fb9b1'>identity function</span> is denoted as $id_{x}$ which is a function from X to X, $id_{x}(x) = x \ \forall x \in X$

Let $f: X \rightarrow Y$

1)  $f \circ id_X=f$ because
	- Domains of $f \circ id_X$ and $f$ are both $X$;
	- Co-domains of $f \circ id_X$ and $f$ are both Y;
	- $(f \circ id_X)(x)= f(id_X (x))=f(x)$ for all $x \in X$.

2)  $id_{Y} \circ f = f$ because
	- Domains of $id_{Y} \circ f$and $f$ are both X;
	- Co-domains of $id_{Y} \circ f$ and $f$ are both $Y$;
	- $(id_{Y} \circ f)(x)= id_Y (f(x))=f(x)$ for all $x \in X$.

**Monoids**
> They have the <span style='color:#0fb9b1'>identity value</span> and the <span style='color:#0fb9b1'>associative</span> property. (Addition, multiplication and composition of functions are monoids)

Example of compositions that are monoids:
1) $f \circ f^{-1}$ which is just the $id^{y \rightarrow y}$
2) $f^{-1} \circ f$ which is just the $id^{x \rightarrow x}$

## Associativity of a Function

Let $f: A \rightarrow B$, $g: B \rightarrow C$, Let $h: C \rightarrow D$

Then $(h \circ g) \circ f = h \circ (g \circ f)$

This is useful for optimization in computation 

## Well Defined Functions

A <span style='color:#0fb9b1'>well defined function</span> means that <span style='color:#f7b731'>for any input</span>, it will always <mark class="hltr-orange">give the same output</mark>

### Addition on $\Bbb Z_n$ is well defined
 
 $\forall n \in \Bbb Z^{+}$ and $\forall [x_{1}],[y_{1}],[x_{2}],[y_{2}] \in \Bbb Z_{n}$, $([x_{1}],[y_{1}]) = ([x_{2}],[y_{2}]) \rightarrow [x_{1}] + [y_{1}] = [x_{2}] + [y_{2}]$
### Multiplication on $\Bbb Z_n$ is well defined
 
 $\forall n \in \Bbb Z^{+}$ and $\forall [x_{1}],[y_{1}],[x_{2}],[y_{2}] \in \Bbb Z_{n}$, $([x_{1}],[y_{1}]) = ([x_{2}],[y_{2}]) \rightarrow [x_{1}] \times [y_{1}] = [x_{2}] \times [y_{2}]$
### Well-Defined Property on a Function

$\forall x_{1}, x_{2} \in X, \forall f : X \rightarrow Y, x_{1} = x_{2} \rightarrow f(x_{1}) = f(x_{2})$

### Well-Defined Property on a Equivalent Relation ~

$\forall x_{1}, x_{2} \in X, \forall f : X \rightarrow Y, x_{1} \sim x_{2} \rightarrow f(x_{1}) \sim f(x_{2})$

### Well-Defined Property on a Equivalent Class $[x]$

$\forall x_{1}, x_{2} \in X, \forall f : X \rightarrow Y, [x_{1}] = [x_{2}] \rightarrow [f(x_{1})] = [f(x_{2})]$
