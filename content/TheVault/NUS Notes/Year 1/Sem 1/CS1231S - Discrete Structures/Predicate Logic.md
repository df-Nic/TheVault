---
Title: Predicate Logic
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1231S
  - Math/Logic
---
# Predicates and Quantified Statements
---
## Terminology

**Predicate**
> A sentence that contains a <span style='color:#f7b731'>finite number of variables</span> and becomes a <span style='color:#0fb9b1'>statement</span> when <span style='color:#f7b731'>values are being substituted</span>. Its truth value depends on the values being substituted.

**Domain / Universe Set**
> A <span style='color:#0fb9b1'>predicate variable</span> is the set of <span style='color:#f7b731'>all values that can be substituted</span>.

**Example:** Let P(X, Y) be -> "X is a student at NUS and studies at Y"
- X and Y are <span style='color:#0fb9b1'>predicate variables</span>
- P is a <span style='color:#0fb9b1'>predicate symbol</span>
- P(X, Y) is a <span style='color:#0fb9b1'>predicate</span>
-  The <span style='color:#0fb9b1'>domain</span> is all possible inputs of X and Y

**Truth set**
> For <span style='color:#f7b731'>all variables</span> in the <span style='color:#0fb9b1'>domain</span> that makes the <span style='color:#f7b731'>predicate true</span> is called a truth set.

It is denoted as, $\{ x \in D \ | \ P(x) \}$.
	The symbol $|$ means "such that"

**Universal Quantifier** $\forall$
> It denotes "<span style='color:#f7b731'>for all</span>".

It is denoted as $\forall x \in D \ | \ P(x)$
	This is called a <span style='color:#f7b731'>universal statement</span>

The statement is true iff it is <span style='color:#f7b731'>true for every x in the domain</span>.
The statement is false iff it is <span style='color:#f7b731'>false for at least one value in the domain</span>. (**Counterexample**)

**Existential Quantifier** $\exists$ or $\exists!$
> It denotes "<span style='color:#f7b731'>there exists</span>" or in other terms "there is at least one". As for the latter it denotes, "<span style='color:#f7b731'>there is one and only one</span>"

It is denoted as $\exists x \in D \ | \ P(x)$
	This is called a <span style='color:#f7b731'>existential statement</span>.

The statement is true iff it is <span style='color:#f7b731'>true for at least one value in the domain</span>.
The statement is false iff it is <span style='color:#f7b731'>false for all values in the domain</span>.

By adding <span style='color:#0fb9b1'>quantifiers</span>, a <mark class="hltr-orange">statement can be made from predicates</mark>.

**Universal / Existential Conditional Statement**
> Is a combination of a <span style='color:#0fb9b1'>quantifier</span> and a <span style='color:#0fb9b1'>conditional statement</span>.

**An example**: $\forall x \ P(x) \rightarrow Q(x)$

A universal/existential conditional statement is <span style='color:#f7b731'>equivalent its universal statement</span> variant.
	$\forall x \in U \ P(x) \rightarrow Q(x) \equiv \forall x \in D \ | \ Q(x)$ or $\exists x \in U \ P(x) \rightarrow Q(x) \equiv  \exists x \in D \ | \ Q(x)$

This is true because <span style='color:#f7b731'>U is a bigger set than D</span>. Thus, all of U is true, then the subset which is D has to be true as well. 

**Abduction**
> Not guarantee but a strong possibility, therefore do not discount logically invalid arguments as it depends on application. 
## Negation of Quantified Statements

To <span style='color:#f7b731'>negate</span> any quantified statement;

1) $\lnot(\forall x \in D \ | \ P(x)) \equiv \exists x \in D, \lnot P(x)$

2) $\lnot(\exists x \in D \ | \ P(x)) \equiv \forall x \in D, \lnot P(x)$

In theory, to negate a <span style='color:#0fb9b1'>quantified statement</span>, <mark class="hltr-orange">reverse</mark> its <span style='color:#0fb9b1'>quantifier</span> and <mark class="hltr-orange">negate</mark> the <span style='color:#0fb9b1'>predicate statement</span>.

## Negation of Quantified Conditional Statement

To <span style='color:#f7b731'>negate</span> any quantified statement;

1) $\lnot(\forall x (P(x) \rightarrow Q(x)))$
	1.1) $\lnot(\forall x (P(x) \rightarrow Q(x))) \equiv \exists x \ | \ \lnot(P(x) \rightarrow P(x))$
	1.2) $\lnot (P(x) \rightarrow Q(x)) \equiv P(x) \land \lnot Q(x)$

Thus the <span style='color:#f7b731'>negation</span> of the statement above is, $\exists x \ | \ (P(x) \land \lnot Q(x))$

## Vacuous Truth of Universal Conditional Statements

**Vacuous Truth**
> A <span style='color:#f7b731'>conditional or universal statement</span> that is <span style='color:#f7b731'>true</span> because the <span style='color:#f7b731'>hypothesis</span> (Antecedent) <span style='color:#f7b731'>cannot be satisfied</span>.

Given a empty bowl and a statement, "All the balls in the bowl are blue", is this true?

It is <span style='color:#f7b731'>true</span> (Vacuously True / True By Default) as if the statement in <span style='color:#f7b731'>negated</span>, <span style='color:#f7b731'>it will be false</span> ("There exist a ball in the bowl that is not blue").

Therefore a universal conditional statement is *<span style='color:#0fb9b1'>vacuously true</span>* if and only if P(x) is false for $\forall x \in D$.

## Variants of Universal Conditional Statements

Consider the following : $\forall x \in D \ (P(x) \rightarrow Q(x))$

**Contrapositive :** $\forall x \in D \ (\lnot Q(x) \rightarrow \lnot P(x))$

**Converse :** $\forall x \in D \ (Q(x) \rightarrow P(x))$

**Inverse :** $\forall x \in D \ (\lnot P(x) \rightarrow \lnot Q(x))$

**Sufficient Condition :** $\forall x (P(x) \rightarrow Q(x))$, P(x) is a sufficient condition for Q(x).

**Necessary Condition :** $\forall x (Q(x) \rightarrow P(x))$, P(x) is a necessary condition for Q(x).

**Only if :** $\forall x (P(x) \rightarrow Q(x))$, P(x) only if Q(x).

## Common Mistakes of Writing Quantified Statements

Let 
-  Bird(x) : x is a bird
-  Fly(x) : x can fly

Given this **statement** : All birds can fly

Answer 1 : $\forall x \ Fly(Bird(x))$
	This is <span style='color:#eb3b5a'>incorrect</span> as Bird(x) is a <span style='color:#0fb9b1'>predicate</span>, which <span style='color:#f7b731'>evaluates to true or false</span>. It is like writing Fly(True) or Fly(False) which is saying can True / False fly, it makes no sense.

Answer 2 : $\forall x \ (Bird(x) \land Fly(x))$
	This in <span style='color:#eb3b5a'>incorrect</span> as this statement is implying that for all x, it must be a bird and it flies.

Answer 3: $\forall x \ (Bird(x) \rightarrow Fly(x))$
	This is the <span style='color:#20bf6b'>correct</span> way of writing the quantified statement.

Given this **statement** : There is a bird that can fly

Answer 1 : $\exists x \ | \ Bird(x) \rightarrow Fly(x)$
	This is <span style='color:#eb3b5a'>incorrect</span>, as by <span style='color:#0fb9b1'>vacuously true</span> <span style='color:#f7b731'>if there are no birds at all</span>, the quantified conditional statement is <span style='color:#f7b731'>true</span>. However the original statement will be <span style='color:#f7b731'>false</span> as there is no bird at all.

Answer 2 : $\exists x \ | \ (Bird(x) \land Fly(x))$
	This is the <span style='color:#20bf6b'>correct</span> way of writing the quantified statement.

Given this **statement** : Not all birds can fly

Answer 1: $\forall x \ (Bird(x) \rightarrow \lnot Fly(x))$
	This in <span style='color:#eb3b5a'>incorrect</span> as this statement is implying that all bird cannot fly.

Answer 2 : $\exists x \ | \ Bird(x) \rightarrow \lnot Fly(x)$
	This in <span style='color:#eb3b5a'>incorrect</span>. What if there is no birds, then it is <span style='color:#0fb9b1'>vacuously true</span>. However the original statement will be false as there are no birds.

Answer 2 : $\exists x \ | \ (Bird(x) \land \lnot Fly(x))$
	This is the <span style='color:#20bf6b'>correct</span> way of writing the quantified statement.

# Multiple Quantifier Statements
---

It a quantified statement which uses <span style='color:#f7b731'>multiple quantifiers</span>, be it universal or existential quantifiers or both.

Given these 2 statements:
1) $\forall x \in D, \exists y \in E \ | \ P(x, y)$
	This means for <span style='color:#f7b731'>all values of x in set D</span>, there is at <span style='color:#f7b731'>least 1 value of y in set E</span> that will make the statement P(x, y) <span style='color:#f7b731'>true</span>.

2) $\exists x \in D \ | \ \forall y \in E, P(x, y)$
	This means for <span style='color:#f7b731'>at least one value x in set D</span>, that will make the statement P(x, y) <span style='color:#f7b731'>true</span> <span style='color:#f7b731'>for all values of y in set E</span>.

## Order of Quantifiers

<span style='color:#f7b731'>Changing the order</span> of the quantifiers does <span style='color:#f7b731'>change the meaning</span> of the statement. Unless it <span style='color:#f7b731'>all uses the same quantifier</span>.

$\forall x, \exists y | P(x, y) \neq \exists y | \forall x, P(x, y)$. These are <span style='color:#f7b731'>2 different statements</span>

$\forall x, \forall y \equiv \forall y, \forall x \equiv \forall x,y$. These are all convey the same meaning.

## Formal Logic Notation

Certain statements can be <span style='color:#f7b731'>written in many different ways</span> but it all c<span style='color:#f7b731'>onveys the same meaning</span>.

"$\forall x \in D, P(x)$" can be written as $\forall x (x\in D \rightarrow P(x))$

"$\exists x \in D | P(x)$" can be written as $\exists x(x \in D \land P(x))$

<span style='color:#eb3b5a'>However for this course it will follow the former way of writing.</span>

# Arguments with Quantified Statements
---

**Universal Instantiation**
> If some <span style='color:#f7b731'>property is true for everything in a set</span>, then it is <span style='color:#f7b731'>true for any particular thing in the set</span>.

For this type of argument to be <span style='color:#f7b731'>valid</span>. <span style='color:#f7b731'>No matter what particular value is substituted</span> for the predicate symbols for any predicate, <span style='color:#f7b731'>if the result is true for all premises</span> then the <span style='color:#f7b731'>conclusion has to be true</span>. If not it is not valid.
### Universal Modus Ponens

1) $\forall x, (P(x) \rightarrow Q(x)$ (This first premise is also called a <span style='color:#0fb9b1'>major premise</span>)
2) P(a) for a particular a (<span style='color:#0fb9b1'>Premise</span>)
3) $\bullet$ Q(a) (<span style='color:#0fb9b1'>Conclusion</span>)

It is just a variant of the original <span style='color:#0fb9b1'>Modus Ponens</span>. Where given a hypothesis where P implies Q, and P is true therefore Q has to be true.

It is universal as it includes the <span style='color:#0fb9b1'>universal quantifier</span>.

### Universal Modus Tollens

1) $\forall x, (P(x) \rightarrow Q(x)$
2) ~Q(a) for a particular a
3) $\bullet$ ~P(a)

It is just a variant of the original <span style='color:#0fb9b1'>Modus Tollens</span>. Where given a hypothesis where P implies Q, and ~Q therefore ~P has to be true. (Contrapositive)

It is universal as it includes the <span style='color:#0fb9b1'>universal quantifier</span>. And it is the bases of <span style='color:#0fb9b1'>proof by contradiction</span>.

## Universal Transitivity

1) $\forall x, (P(x) \rightarrow Q(x)$
2) $\forall x, (Q(x) \rightarrow R(x)$
3) $\bullet$ $\forall x, (P(x) \rightarrow R(x)$

It is just a variant of the original <span style='color:#0fb9b1'>Transitivty</span>. Where given a hypothesis where P implies Q, and Q implies R therefore P implies R.

# Rules of Inheritance for Quantified Statements
---

**Universal Instantiation**
1) $\forall x \in D, P(x)$
2) $\bullet P(a)$$ if $a \in D$

**Universal Generalization**
1) $P(a)$ for every $a \in D$
2) $\bullet \forall x \in D, P(x)$

**Existential Instantiation**
1) $\exists x \in D, P(x)$
2) $\bullet P(a)$ for some $a \in D$

**Existential Generalization**
1) $P(a)$ for some $a \in D$
2) $\bullet \exists x \in D, P(x)$

