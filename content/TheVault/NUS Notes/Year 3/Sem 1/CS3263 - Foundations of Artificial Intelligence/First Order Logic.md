---
title: First Order Logic
Date Created: 2025-09-01
Last Updated: 2025-09-28
tags:
  - CS3263
  - Logic
---
# Introduction to First Order Logic
---
In FOL, instead of just facts now we **include objects & relations**.

>[!question] What's new in FOL?
>We have entities or **objects** are just people / things in the real world, for instance, colors, people, houses, Ronald McDonald.
>
>**Relations** which indicate some relationship between 2 or more objects.
>
>**Functions** is a relation where there is only 1 output for a given input (*not 2 or more*).
>
>Lastly we have **quantifiers**, universal ($\forall$) & existential ($\exists$).

>[!fail] With so many new terms our world model is now more complicated

In [[Predicate Logic|FOL]] a [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Propositional Logic.md#Satisfiability|model]] will contain the following:
- A **nonempty** set of $D$ objects (*entities*) called <b><span style='color:var(--mk-color-turquoise)'>domain of discourse</span></b>
- A **set of relations**

>[!info] Relations
>
>A relation is a <b><span style='color:var(--mk-color-yellow)'>set of tuples</span></b> where a **tuple** is a set of <b><span style='color:var(--mk-color-yellow)'>objects arranges in a fixed order</span></b>.
>
>For instance, $Father(John, Mark)$ or $Rich(John)$, this is the same for all possible objects which causes the relation to be true.

In FOL there are 3 symbols:
1) **Constant** for specific objects (*Mary, 3, Red*)
2) **Predicate** for relations (*taller-than(John, Peter)*)
3) **Function** for functions (*sum(2,3) will return 5 or father-of(Mary) can return John*)

>[!info] A predicate is a symbol that represents some property or a relationship between objects
>
>It also comes with a <b><span style='color:var(--mk-color-yellow)'>fixed arity</span></b> (*number of arguments*).
>
>For example $Alive(John)$, meaning John is alive or $Loves(Alice, Bob)$ meaning Alice loves Bob.

>[!summary] Interpretation of a Model
>
>**Every model includes an interpretation** ($I$) which consist of the following:
>- Every entity in the domain will be assigned to a constant symbol
>- For each function an entity is assigned to **each possible input** of entities to function (*All permutations*)
>- Predicate `True` will always be assigned value `True`, same for `False`
>- For every other predicate or relation, `True` or `False` is assigned to **each possible input** of entities to the predicate (*A predicate will output true or false*)
<div style="page-break-after: always;"></div>

## Syntactic Rules

1) **Term**
It can be a:
- **Constant** symbol (*King John*)
- **Variable** symbol (*x, y, z*)
- **Predicate** symbol for relations ($King$, $Mortal$)
- **Function** with 1 or more terms ($Loves(Alice, Bob)$).

2) **Sentence**
It can be a:
- **Atomic sentence**
- **Operator followed by a sentence**
- 2 sentences separated by operations or a quantifier with a variable followed by a sentence ($\forall$, $\exists$)

>[!info] Atomic sentence
>
>It can be just a predicate symbol (*Day, Night*) or a predicate symbol with one or more terms in a relation.
>
>Or it can be 2 terms separated by the = symbol (*Father(John) = Henry*)

>[!important] De Morgan's law on $\forall$ will become $\exists$ & vice versa
## Summary of FOL Terms

![[FOL Summary of Terms.png|center|450]]
## Database Semantics

In **relational databases** it can be seen as a <b><span style='color:var(--mk-color-yellow)'>special case of an FOL</span></b> model.

The semantics used in databases makes the following **assumptions**, when treating them like a FOL:
1) **Unique-name assumption** (*UNA*)
In FOL, **2 symbols** might refer to the same object, but in databases they <b><span style='color:var(--mk-color-yellow)'>treat them as different objects</span></b>.

2) **Closed-world assumption** (*CWA*)
Anything that is <b><span style='color:var(--mk-color-yellow)'>not in the database is assumed to be false</span></b>.

3) **Domain closure assumption** (*DCA*)
The **domain of discourse** only <b><span style='color:var(--mk-color-yellow)'>contains symbols which appears in the database</span></b>. For instance if no table contains Dave then Dave is not in the domain (*Domain is not closed in FOL, but in a database it is closed*).
# Inference in First-Order Logic
---
## Propositionalisation

>[!note] The goal of propositionalisation is to convert our FOL into a propositional logic.

**Universal Instantiation** (*UI*) states that we can infer any sentence obtained by <b><span style='color:var(--mk-color-yellow)'>substituting a ground term for a universally quantified variable</span></b> ($\forall x$).

>[!info] Ground term
>
>It is a term <b><span style='color:var(--mk-color-yellow)'>without any variables</span></b>.
>
>For example variables can be $x$, $y$, etc. Non variables are $John$, $Alive(John)$.

We can write this rule as, if we let $SUBST(\theta, \alpha)$ be the result of applying substitution $\theta$ to sentence $\alpha$.
$$
\frac{\forall \text{v } \alpha}{SUBST(\{v/g\}, \alpha)}
$$
Essentially we are just substituting a variable ($v$) with all possible ground terms ($g$) <b><span style='color:var(--mk-color-yellow)'>through brute forcing</span></b>.

>[!example] Example of UI
>
>Lets say we have this statement, $\forall x King(x) \land Greedy(x) \implies Evil(x)$
>
>Here $x$ is our variable and we can replace it with a ground truth (*some object*)  like John so we will get:
>
>$$King(John) \land Greedy(John) \implies Evil(John)$$
>
>We do this for all other ground terms.

**Existential Instantiation**, states that we can replace replace <b><span style='color:var(--mk-color-yellow)'>existentially quantified variable with a new constant symbol</span></b>.

This is because we know some object satisfy this statement in the domain but we are not sure which one thus we can just assign some variable to represent that object.

>[!abstract] Skolem constants & functions
>
>It is a constant that is **substituted** for a variable when <b><span style='color:var(--mk-color-yellow)'>eliminating an existential quantifier</span></b>.
>
>However when we **encounter a universal & a existential quantifier** a <b><span style='color:var(--mk-color-yellow)'>Skolem function is used</span></b>, as it will preserve the meaning.
>
>For example if we have $\forall x \forall y \exists z P(x, z) \land Q(y)$, if we replace z with a constant then we are essentially <b><span style='color:var(--mk-color-red)'>fixing z to be 1 value, thus not preserving the meaning</span> </b>.
>
>Use a **function** instead, $\forall x \forall y P(x, f(x, y)) \land Q(y)$, this function will <b><span style='color:var(--mk-color-yellow)'>map x and y to a particular value</span></b> where z holds (*the existential quantifier holds*).

We can also write it as:
$$
\frac{\exists \text{v } \alpha}{SUBST(\{v/k\}, \alpha)}
$$
>[!important] The new variable introduced must not appear in the knowledge base
>
>Assuming we have $Dog(Fido)$ in our knowledge base, then if we set our Skolem constant as Fido for $\exists Cat(x)$, then it contradicts. Thus we should set a variable that is not within the KB.
## Reduction to Propositional Inference

Then we can use any propositional algorithms to solve our query.

>[!example] Example of a reduction
>
>Our KB has $Human(John)$, $\forall \text{x } (Human(x) \implies Mortal(x))$
>
>Our query **is John mortal**.
>
>1) First apply UI so we will get $Human(John) \implies Mortal(John)$
>2) Substitute all ground terms to be a symbol so, $Human(John) = A$, $Mortal(John) = B$ and from UI we have $A \implies B$
>3) Lastly we can run any propositional algorithm to prove our query is true.

>[!failure] With function symbols, the number of ground truth substitutions is infinite
>
>Is like our nested function we can do $fn(fn(fn(fn(x))))$ which can continue forever.

This is where <b><span style='color:var(--mk-color-turquoise)'>Herband's theorem</span></b> comes in which limits this infinite possibility.

>[!info] Herband's theorem
>If a sentence is **entailed** then there is a <b><span style='color:var(--mk-color-yellow)'>proof involving a finite subset</span></b> of propositionalised knowledge base.

It essentially <b><span style='color:var(--mk-color-yellow)'>builds the proof from a depth of 1 term to a depth of k terms</span></b> where $k$ is the number you need to construct the proof.

For instance it can start from:
- $f(x)$
- $f(f(x))$
- $f(f(f(x)))$
- and so on until the proof is constructed

>[!success] The inference is complete

>[!Failure] Entailment of FOL is semi-decidable for Herband's theorem
>
>There are algorithms that says yes to every entailed sentence, but <b><span style='color:var(--mk-color-red)'>no algorithm exist to say no to every non-entailed sentence</span></b>.
## First-Order Inference

>[!note] Generalised Modus Ponens
>It raises modus ponens from a propositional logic to first-order logic.
>
>Useful for <b><span style='color:var(--mk-color-green)'>inference with first order definite clauses</span></b> (*definite clauses with only universal quantifiers*).

An important thing to note is that $SUBST(\theta, p_{i}') = SUBST(\theta, p_{i})$ for all $i$.

For instance if we have $\forall x (King(x) \land Greedy(x) \implies Evil (x))$, in normal modus ponens, it will be similar to $A \land B \implies C$.

If we let $p_{1} = King(x)$ and $p_{2}= Greedy(y)$, then by doing substitution of $\theta = \{x \backslash John, y \backslash John \}$ we will get $Evil(John)$.

We are essentially <b><span style='color:var(--mk-color-yellow)'>substituting variables with ground terms</span></b> and if we find a matching substitution for the body then the <b><span style='color:var(--mk-color-green)'>conclusion will hold</span></b>.
### Unification

It is essentially a <b><span style='color:var(--mk-color-yellow)'>combiner of 2 sentences</span></b> and returning a <b><span style='color:var(--mk-color-turquoise)'>unifier</span></b> (*a substitution*) **if it exist**, which makes the sentences identical.

>[!note] The goal of unification is to find a substitution such that it satisfies 2 or more sentences

>[!example] Examples of Unification
>
>Assume we have 2 sentences, $Loves(Dave, y)$ and $Loves(x, Gloria)$
>
>Then by unification we can get a substitution of $\theta \{x \backslash Dave, y \backslash Gloria\}$
>
>If we have $Friends(Dave, x, Gloria)$ and $Friends(x, Mary, Gloria)$ or $Friends(Dave, Mary, x)$ and $Friends(y, Gloria, Sam)$, it will <b><span style='color:var(--mk-color-red)'>both fail</span></b>:
>1) $x$ cannot be both Mary and Dave at the same time (*You can solve this by just renaming the variables*)
>2) Gloria and Mary are 2 different constants and this cannot be substituted

We can also do <b><span style='color:var(--mk-color-turquoise)'>compositions</span></b> of substitutions, it is similar to math where we do $\theta \space \circ \space \lambda$. First we apply the substitution for $\theta$ first follow by $\lambda$.
#### Most General Unifier

A unifier is considered the **most general**, if <b><span style='color:var(--mk-color-yellow)'>every other unifier is an instance of it</span></b>.

>[!info] If you can derive $\theta'$ by making substitutions from $\theta$ then $\theta$ is more general.

>[!important] A variable cannot be replaced by a term containing the variable being unified
>
>For instance you <b><span style='color:var(--mk-color-red)'>cannot</span></b> substitute $x \backslash f(x)$. This is because we can then infinitely self-substitute itself.
>
>This is handled by something called an <b><span style='color: var(--mk-color-turquoise)'>occurs check</span></b>.

>[!example] Example of a more general unifier
>
>Our statement is $Father(x, Sam)$ & $Father(y, z)$
>
>- $\theta_{1} = \{x \backslash Dave, y \backslash Dave, z \backslash Sam\}$, which unification will give $Father(Dave, Sam)$
>- $\theta_{2} = \{x \backslash y,  z \backslash Sam\}$, which unification will give $Father(y, Sam)$
>  
>$\theta_{1}$ can be obtained from $\theta_{2}$ by substituting $Dave$ as $y$, thus it is an instance of $\theta_{2}$ thus $\theta_{2}$ is **more general**.

**Algorithm to find the most general unifier**:
```cpp
// A and B are sentences and theta is a substitution
function Unify(A, B, theta) {
	for (symbol in A and B) { // Loop through every symbol P(a, b, c, ....)
	stop when you find a symbol in A disagrees with B
	}
	
	if (not exhausted) { // We found a conflicting symbol and we did not run out of symbols for either A or B
		// Let x & y be the symbols of A and B that disagree
		if (x is a variable && does not occur in y) { // occure here is the occurs checks
			theta = theta + {x/y}; // Then we sub x with y
			return Unifty(SUBST(theta, A), SUBST(theta, B), theta) ;
		} else if (y is a variable && does not occur in x) {
			theta = theta + {y/x}; // Then we sub x with y
			return Unifty(SUBST(theta, A), SUBST(theta, B), theta) ;
		} else {
			return failure; // Here netheir is a variable and they disagree with one another
		}
	}
	
	return theta;
}
```
## First Order Definite Clauses

Similar to [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Propositional Logic.md#Horn Clauses & Definite Clauses|definite clauses]] in propositional logic. It is just a <b><span style='color:var(--mk-color-yellow)'>disjunction of literals and exactly 1 is positive</span></b>.

It can be either:
- **Atomic** ($Greedy(x)$)
- **Implication**, where the antecedent is a conjunction of positive literal and consequent is single positive literal ($King(x) \land Greedy(x) \implies Evil(x)$).

>[!note] Existential quantifiers are not allowed & universal quantifiers are implicit
>
>Thus we do not write it and just leave it out.
### Forward Chaining for FOL

**Algorithm for forward chaining for FOL**
```cpp
vector<string> FOL-FC(KB, query) {
	// We will conitnue infer new facts until we cannot infer anymore or a match is found
	while True {
		newFacts = {};
		for (each rule in KB) {
			rule = standardoseVariables(rule); // Replaces all variables with ones that are not used
			// Here we are doing generalised modus ponens (Can we substitute known facts to get new ones)
			for (each substution which makes SUBST(theta, rule) = SUBST(theta, Comfbination of other facts)) {
				q = consequent of rule; // We found a substitution that proves p is true this p -> q, q is true
				if (q does not unify with a sentence in KB or newFacts) { // Prevent duplicated facts
					newFacts.push_back(q);
					// See if q answers our query since if the 2 unifies that means they are the same
					set = Unify(q, query);
					if (set != failure) {
						return set;
					}
				}
			}
		}
		// Nothing else to infer
		if (newFacts.isEmpty()) {
			return false;
		}
		KB.push_back(newFacts) // Add the new facts and iterate again
	}
}
```

>[!info] Standardised variables
> If we have a sentence like $(\forall x P(x) )\land (\exists x Q(x))$ we need to <b><span style='color: var(--mk-color-yellow)'>change one of the variables to avoid confusion</span></b>.
> 
> Example: $\forall x [\exists y Animal(y) \land \lnot Loves(x, y)] \land [\exists y Loves(y, x)]$, will need to be renamed to $\forall x [\exists y Animal(y) \land \lnot Loves(x, y)] \land [\exists z Loves(z, x)]$

**Summary** of what the algorithm does:
- For each rule in KB, find a match on the antecedent with known facts in the KB
- Once a match is found then the consequent of the rule is inferred
- If the inferred fact is our query then we can stop, else we add it into our KB
- Repeat the above & if we cannot infer any more new facts then we will stop

>[!success] It is sound as each step we are using generalised modus ponens

>[!success] It is complete
>Because FC is a breadth-first FC algorithm. 
>
>But only **for a definite clause knowledge base**

>[!fail] It is inefficient
### Backward Chaining for FOL

**Algorithm for backward chaining for FOL**
```cpp
vector<string> FOL-BC(KB, query) {
	return FOL-BC-Or(KB, query, {});
}

vector<string> FOL-BC-Or(KB, query, theta) {
	// for all p -> q, find all rules where q = our query through unification
	for (each rule in FETCH-RULES_FOR-GOAl(KB, query)) {
		lhs, rhs = STANDARDISE-VARIABLES(rule); // lhs => rhs
		for (each theta_prime in FOL-BC-And(KB, lhs, Unify(rhs, goal, theta))) {
			yield theta_prime;
		}
	}
}

vector<string> FOL-BC-And(KB, query, theta) {
	if (theta == failure) {
		return;
	} else if (query.length() == 0) {
		yield theta;
	} else {
		first, rest = first(query), rest(query) // Basically here query is a & b & c & ..., first is just a then rest is b & c &...
		for (each theta_prime in FOL-BC-Or(KB, Subst(theta, first), theta)) {
			for (each theta_prime_prime in FOL-BC-And(KB, rest, theta_prime)) {
				yield theta_prime_prime;
			}
		}
	}
}
```

Similar to [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Propositional Logic#Backward Chaining|propositional logic's backward chaining]], we are finding statements whose conclusion is our goal and we will solve the body.

This is implemented as a **generator** as it **returns multiple results**.

>[!success] It is more efficient than forward chaining

>[!fail] It is not complete
>This algorithm is from the **depth-first search** algorithm. It **does not check for loops** which might cause it to <b><span style='color:var(--mk-color-red)'>not terminate</span></b>.
<div style="page-break-after: always;"></div>

## Resolution in FOL

This is similar to [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Propositional Logic#Resolution|resolution for propositional logic]]. But instead of taking any negated clause, we also need to ensure that the <b><span style='color:var(--mk-color-yellow)'>positive clause unifies with the negation of the other clause</span></b>.

**Resolution inference rule**
$$
\frac{n_{1} \lor \dots \lor n_{j} \space , m_{1} \lor \dots \lor m_{k}}{SUBST(\theta, n_{1}\lor \dots \lor n_{a-1}  \lor n_{a+1}\lor \dots \lor n_{k} \lor m_{1} \lor \dots \lor m_{b-1} \lor m_{b+1} \lor \dots \lor m_k)}
$$
**Where**:
- $Unify(n_{a}), \lnot m_{b} = \theta$

>[!important] And similarly we need to convert from FOL to a CNF form
>We need to:
>- Eliminate implications
>- Move $\lnot$ inwards
>- Standardise variables
>- [[First Order Logic#Propositionalisation|Skolemize]]
>- Drop universal quantifiers
>- Distribute $\lor$ over $\land$

>[!example] Example of converting FOL to a CNF form
>Lets say we have $\forall x  [\forall y \space Animal(y) \implies Loves(y,x)] \implies [\exists y  \space Loves(y,x)]$
>
>- $\forall x \space \lnot  [\forall y \space \lnot Animal(y) \lor Loves(x,y)] \lor [\exists y  \space Loves(y,x)]$ (*Implication law x2*)
>- $\forall x \space [\exists y \space Animal(y) \land \lor Loves(x,y)] \lor [\exists y  \space Loves(y,z)]$ (*De Morgan's law*)
>- $\forall x \space [\exists y \space Animal(y) \land \lor Loves(x,y)] \lor [\exists z  \space Loves(z,x)]$ (*Standardise as y already is used*)
>- $\forall x \space [\space Animal(F(x)) \land \lor Loves(x,F(x))] \lor [Loves(G(x),x)]$ (*Skolemize*)
>- $[\space Animal(F(x)) \land \lor Loves(x,F(x))] \lor [Loves(G(x),x)]$ (*Drop universal quantifiers*)
>- $[Animal(F(x)) \lor Loves(G(x), x)] \land [\not Loves(x, F(x)) \lor Loves(G(x), x)]$ (*Distribution law*)

After conversion we can essentially **carry out the resolution algorithm by adding in the negation of the query** with the <b><span style='color: var(--mk-color-yellow)'>help from unification</span></b>.

>[!warning] Resolution can sometimes produce nonconstructive proofs for existential goals
>This means that when we prove that a query is true, but there is no unique binding for that variable.
### Standardising during Resolution

During our **execution** of the <b><span style='color:var(--mk-color-blue)'>resolution algorithm</span></b>, we can encounter this:
- $\lnot Loves(x, F(x)) \lor Loves(G(x), x)$
- $\lnot Animal(x) \lor Loves(Jack, x)$

We can see for the relation $Loves$ there is a similar variable $x$, we can just <b><span style='color:var(--mk-color-yellow)'>swap out one with another</span></b> by using substitution for instance $\{x \backslash y\}$ for $Loves(Jack, x)$.

Now we can unify the 2 sentences through this substitution of $\{x \backslash Jack, y \backslash F(Jack)\}$, since after substituting $x = Jack$ we will get $F(Jack)$.

