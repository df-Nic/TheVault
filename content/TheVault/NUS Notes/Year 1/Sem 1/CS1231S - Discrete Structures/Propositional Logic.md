---
Title: Propositional Logic
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1231S
  - Math/Logic/PropositionalLogic
---
# Compound Statements
---
## Terminology

**Statement / Proposition**
> A sentence that is <span style='color:#f7b731'>either true or false but not both</span>.

**Conjunction**
> It is the keyword for <span style='color:#f7b731'>"and"</span> or $\land$

**Disjunction**
> It is the keyword for <span style='color:#f7b731'>"or"</span> or $\lor$

**Negation**
> It is the keyword for <span style='color:#f7b731'>"not"</span> or $\lnot$ or ~. Double negation, will result in the same value

**Order of Operations**
1) Parentheses first, as they override or disambiguate order of operations. 
2) Negation
3) Followed by Conjunction or Disjunction, <span style='color:#f7b731'>both are coequal</span>.
4) If-then / implies or if and only if.

Try and <mark style='background:var(--mk-color-yellow)'>not write statements that are ambiguous</mark>.

**Statement Form / Propositional Form**
> An expression made up of <span style='color:#f7b731'>statement variables</span> and <span style='color:#f7b731'>logical connectiveness</span> that becomes a statement. If there is variables, then it is not a statement

**Logical Equivalence**
> Two statements are logically equivalent if they have <span style='color:#f7b731'>identical truth values</span> for each possible substitution of statements.

**Tautology**
> A statement form that is <span style='color:#f7b731'>always true regardless of the truth values</span> of the individual statements substituted.

**Contradiction**
> A statement form that is <span style='color:#f7b731'>always false regardless of the truth values</span> of the individual statements substituted.
### Truth Table

|  P  |  Q  | ~P  | ~Q  | P $\land$ Q | P $\lor$ Q |
| :-: | :-: | :-: | :-: | :---------: | :--------: |
|  T  |  T  |  F  |  F  |      T      |     T      |
|  F  |  T  |  T  |  F  |      F      |     T      |
|  T  |  F  |  F  |  T  |      F      |     T      |
|  F  |  F  |  T  |  T  |      F      |     F      |

**Exclusive-or** ($(p \lor q) \land \lnot(p \land q$)
> Either one of p or q has to be true while the other has to be false for the statement to be true.
## Logical Equivalences

1)  **Commutative Law**
	$p \land q \equiv q \land p$ **OR**  $p \lor q \equiv q \lor p$

2)  **Associative Law**
	$p \land q \land r \equiv (p \land q) \land r \equiv p \land(q \land r)$ **OR** $p \lor q \lor r \equiv (q \lor p) \lor r \equiv p \lor(q \lor r)$

3)  **Distribution Law**
	$p \land (q \lor r) \equiv (p \land q) \lor (p \land r)$ **OR** $p \lor (q \land r) \equiv (p \lor q) \land (p \lor r)$

4)  **Identity Law**
	$p \land true \equiv p$ **OR** $p \lor false \equiv p$

5)  **Negation Law**
	$p \lor \lnot p \equiv true$ **OR** $p \land \lnot p \equiv false$

6)  **Double Negative Law**
	$\lnot(\lnot p) \equiv p$

7)  **Idempotent Law**
	$p \land p \equiv q$ **OR** $q \lor q \equiv q$

8)  **Universal Bound Law**
	$p \lor true \equiv true$ **OR** $p \land false \equiv false$

9)  **De Morgan's Law**
	$\lnot(p \land q) \equiv \lnot p \lor \lnot q$ **OR** $\lnot(p \lor q) \equiv \lnot p \land \lnot q$

10)  **Absorption Law**
	$p \lor (p \land q) \equiv p$ **OR** $p \land (p \lor q) \equiv p$

11)  **Negation of True and False**
	~true = false **OR** ~false = true

12) **Implication Law**
	$p \rightarrow q \equiv \lnot p \lor q$ **OR**  $\lnot(p \rightarrow q) \equiv  p \land \lnot q$

# Conditional Statements
---

Statement: If you are are computer science major then you will take CS1231S.

Let p be : If you are a computer science major
Let q be : You will take CS1231S
$\rightarrow$ : If-then / Implies

A <span style='color:#0fb9b1'>conditional statement</span> for the given example will be: $p \rightarrow q$

**Vacuously True / True by Default**
> A conditional statement is <span style='color:#f7b731'>true by virtue of fact that its hypothesis is false</span>.
## Terminology

**Conditional**
> If p and q are statement variables, the conditional of q by p is denoted as $p \rightarrow q$. <mark class="hltr-orange">It is only false when p is true and q us false</mark>. Do take note that $p \rightarrow q \ne q \rightarrow p$.

**Hypothesis / Antecedent**
> It is the first assumption in the statement (p).

**Conclusion / Consequent**
> It is the second part of the assumption in the statement (q).

**Contrapositive**
> A contrapositive of a statement $p \rightarrow q \equiv \lnot q \rightarrow \lnot p$.

**Converse**
> The converse of the statement $p \rightarrow q$ is $q \rightarrow p$.

**Inverse**
> The inverse of the statement $p \rightarrow q$ is $\lnot p \rightarrow \lnot q$. The inverse is equivalent to $q \rightarrow p$ a converse.

**Only if**
> Saying "p only if q" means $p \rightarrow q$. This is because <span style='color:#f7b731'>it also means if not q then not p</span>.

**If**
> Saying "p if q" means $q \rightarrow p$.

**If And Only If**
> It means $p \iff q$. Both p and q must have the <span style='color:#f7b731'>same truth values</span> for the statement to be true.

**Biconditional**
> A statement is biconditional of p and q uses the words <span style='color:#f7b731'>if and only if</span>, which is denoted $p \iff q$. The <span style='color:#f7b731'>statement is true if both p and q have the same truth values</span>.

**Necessary and Sufficient**
> p is a sufficient condition for q means $p \rightarrow q$, whereas for necessary it will be $q \rightarrow p$. If p is <span style='color:#f7b731'>both necessary and sufficient</span> then it will be $p \iff q$.

# Arguments
---

An <span style='color:#0fb9b1'>argument</span> is a <span style='color:#f7b731'>sequence of statements ending in a conclusion</span>. It is only true if all its statements (premises) is true.

A <span style='color:#0fb9b1'>premise</span> (Assumptions or Hypothesis), <span style='color:#f7b731'>are all the statements</span> in the argument <span style='color:#f7b731'>except the final one</span>.

A <span style='color:#0fb9b1'>conclusion</span>, which uses the $\bullet$ symbol read as therefore, is <span style='color:#f7b731'>the final statement</span>.

## Determining the Validity or Invalidity

1) Identify all the <span style='color:#0fb9b1'>premises</span> and <span style='color:#0fb9b1'>conclusion</span> in argument form.
2)  Construct truth tables <span style='color:#f7b731'>showing the truth values</span> for all premises and conclusion.
3) The rows in the truth table where <span style='color:#f7b731'>all premises are true</span> is called the <span style='color:#0fb9b1'>critical row</span>.
	- If he conclusion is false then the argument is invalid
	- If the conclusion if true then the argument is valid.

### Critical Row

Looking at the critical row is sufficient, this is because, looking at the <span style='color:#0fb9b1'>tautology</span> definition, if $(p1 \land p2 \land p3 \land \dots pn) \rightarrow K$, where K is the <span style='color:#0fb9b1'>conclusion</span> and p is the <span style='color:#0fb9b1'>premises</span>.

If <span style='color:#f7b731'>all the premises are true that means that the conclusion must be true</span> ($true \land true \land \dots$). However if there is a situation where the <span style='color:#f7b731'>conclusion is false, then the argument is invalid</span>.

## Syllogism

It is an <span style='color:#f7b731'>argument consisting of two premises and a conclusion</span>.

**Modus Ponens**
1) If $p \rightarrow q$
2) p
3) $\bullet$ q

**Modus Tollens**
1) If $p \rightarrow q$
2) $\lnot q$
3) $\bullet \lnot p$ 

Modus Tollens, uses the idea of contrapositive. $p \rightarrow q \equiv \lnot q \rightarrow \lnot p$.

# Rules of Inference
---

It is just <span style='color:#f7b731'>another form of argument that is valid</span>.

1) Generalization
	1) $p$ or $q$
	2) $\bullet p \lor q$  or  $\bullet p \lor q$, respectively

Example: Let p be, I like dogs. then the conclusion is I like dogs or I like cats, which is always true given p.

2) Specialization
	1) $p \land q$ or $p \land q$
	2) $\bullet p$ or $\bullet q$, respectively

Allows the discarding of extraneous information to concentrate on a particular property of interest.

Example: Let the premise be, I know how to speak English and Chinese. Conclusion, I know how to speak Chinese.

3) Elimination
	1) $p \lor q$ 
	2) $\lnot q$ or $\lnot p$ 
	3) $\bullet p$ or $\bullet q$ respectively based on point 2 

If there are <span style='color:#f7b731'>two possibilities</span> and <span style='color:#f7b731'>one can be ruled out</span>, then the <span style='color:#f7b731'>other must be true</span>.

Example: I like apples or oranges, you also know that I don't like oranges, therefore I like applies.

4) Transitivity
	1) $p \rightarrow q$
	2) $q \rightarrow r$
	3) $\bullet p \rightarrow r$

If one statement implies a second and the second implies the third then in conclusion the first implies the third.

Example: A square is a rectangle ($p \rightarrow q$). A rectangle is a quadrilateral ($q \rightarrow r$). Therefore a square is a quadrilateral ($\bullet p \rightarrow r$). 

5) Proof by Division into Cases
	1) $p \lor q$
	2) $p \rightarrow r$
	3) $q \rightarrow r$
	4) $\bullet r$

If one of the <span style='color:#f7b731'>two possibilities are true</span>. If in <span style='color:#f7b731'>either case a certain conclusion follows</span> then that <span style='color:#f7b731'>conclusion must be true</span>.

Example: x is either positive or negative. If x is positive x<sup>2</sup> > 0. If x is negative x<sup>2</sup> > 0. Therefore, x<sup>2</sup> > 0.

# Fallacies
---

An <span style='color:#f7b731'>error</span> in reasoning that results in an invalid argument

**Common fallacies:**
1) Ambiguous Premises, treating as if they were unambiguous (<span style='color:#0fb9b1'>Converse Error</span>)

![[Converse Error Example.png|center]]

2) Circular Reasoning, assumed to be proved without having derived it from the premises (<span style='color:#0fb9b1'>Inverse Error</span>)

![[Inverse Error Example.png|center]]

3) Jumping to a Conclusion, without adequate reasoning


**Valid Argument with A False Premise**
> Argument is <span style='color:#f7b731'>valid</span> by modus ponens. But its <span style='color:#f7b731'>major premise is false</span> thus so its conclusion.

Example: If I am a Singaporean then I am 2 meters tall. Since I am a Singaporean then I am 2 meters tall. 
> Well though is true in terms of modes ponens but I am not 2 meters tall.

**Sound and Unsound**
> An argument is <span style='color:#0fb9b1'>sound</span> if and only if it is <span style='color:#f7b731'>valid and all its premises are true</span>, else it is <span style='color:#0fb9b1'>unsound</span>.

## Contradiction Rule

If you can show that the supposition that the statement <span style='color:#f7b731'>p is false leads logically to a contradiction</span> then the <span style='color:#f7b731'>conclusion is that p is true</span>.

1) $\lnot p \rightarrow false$
2) $\bullet p$

If an <span style='color:#f7b731'>assumption leads to a contradiction</span>, then that <span style='color:#f7b731'>assumption must be false</span>. This is the heart of the methods of proof by contradiction.