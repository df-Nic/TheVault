---
title: Propositional Logic
Date Created: 2025-08-20
Last Updated: 2025-09-28
tags:
  - CS3263
  - Logic
---
# Fundamentals of Logic
---
A **knowledge-based agent** uses something called a <b><span style='color:var(--mk-color-turquoise)'>knowledge base</span></b> to define the environment it is in.

>[!summary] Knowledge base
>
>It can be seen as a <b><span style='color:var(--mk-color-yellow)'>set of rules</span></b> (*sentences*) which are seen as <b><span style='color:var(--mk-color-yellow)'>axioms</span></b> (*facts which are deemed true*) about the world.
>
>When new <b><span style='color:var(--mk-color-yellow)'>sentences are derived</span></b> it is known as **inference**.
>
>And we can add new sentences using the `TELL` operation and query using the `ASK` operation.

In standard logics, every sentence **must be either** <b><span style='color:var(--mk-color-green)'>true</span></b> or <b><span style='color:var(--mk-color-red)'>false</span></b> or <b><span style='color:var(--mk-color-gray)'>unknown</span></b>.

Logic provides us with a **formal language**, which is a set of expressions (*sentences*) using an alphabet (*symbols*) & rules.

>[!note] Syntax
>
> It determine which sentences are <b><span style='color:var(--mk-color-yellow)'>valid</span></b> (*well-formed*) and which are not.
> 
> Example: $x + y = 4$ is well formed but $x4+y$ is not.
## Satisfiability

Given a sentence (*or a set of constraints*) $\alpha$ is true for a model $m$, we can say the following:
- $m$ <b><span style='color:var(--mk-color-turquoise)'>satisfies</span></b> $\alpha$
- $m$ is a <b><span style='color:var(--mk-color-yellow)'>model</span></b> for $\alpha$

>[!info] Models & Worlds
>
>A <b><span style='color:var(--mk-color-turquoise)'>world</span></b>, can be thought of an <b><span style='color:var(--mk-color-yellow)'>assignment to variables</span></b> (*James is a guy, Marry is a girl, etc*).
>
>A <b><span style='color:var(--mk-color-turquoise)'>model</span></b> is also **a world**, but with the added characteristic that its assignment <b><span style='color:var(--mk-color-yellow)'>makes a statement true</span></b>.

Then we can let $M(\alpha)$ be the <b><span style='color:var(--mk-color-yellow)'>set of all models</span></b> that satisfies $\alpha$.

>[!important] A sentence is satisfiable if there is at least 1 world which makes the sentence evaluate to true
>
>For example, $A \land \lnot A$ is not satisfiable since there is no assignment of A which makes the statement true.

The $M(True)$ is the **universal set**, while the $M(False)$ is just an **empty set** ($\emptyset$).

## Entailment

When we say $\alpha$ entails (*$\models$*) $\beta$, it means that every model in which $\color{orange}{\alpha}$ <b><span style='color:var(--mk-color-yellow)'>is true</span></b>, $\color{orange}{\beta}$ <b><span style='color:var(--mk-color-yellow)'>is also true</span></b>.

We can also infer that,  **$\alpha \models \beta$** $M(\alpha) \subseteq M(\beta)$. 

![[Entailment Definition.png|center|100]]

>[!important] Entailment is important because given some facts we know is true we want to find other facts which are true

>[!failure] If one model is true for $\alpha$ but is false for $\beta$ then it is not entailed
>

If $\alpha$ entails $\beta$, then $\alpha$ is a **stronger assertion** than . This is because <b><span style='color:var(--mk-color-yellow)'>it rules out more possible worlds</span></b> since, if $\alpha$ is true then the world for $\beta$ is true (*but not the other way round*).

>[!example] Example of entailment
>
>If we have $P \land Q \models P$, then we know that $M(P \land Q) \subseteq M(P)$.
>
>Essentially the model in which makes P and Q true, makes P true as well.

When proving entailment, use either resolution or use the definition of entailment.

>[!important] $false \models \alpha$ is always true. Since it is a empty set it entails every sentence
### Monotonicity

If **more information is added** into the knowledge base the set of entailed sentences can <b><span style='color:var(--mk-color-yellow)'>only increase</span></b>.

Thus if $KB \models \alpha$, then given another sentence $\beta$, $KB \land \beta \models \alpha$. Meaning that $M(KB \land \beta) \subseteq M(KB) \subseteq M(\alpha)$.

>[!question] Why is this so?
>
> Since if $KB$ is true then $\alpha$ is also true, this means that if we were to add 1 more sentence ($\beta$) <b><span style='color:var(--mk-color-yellow)'>will not cause the previous inferences to be invalid</span></b>.
> 
> What if the **add a new statement contradicts**, this means that your world is explosive, which we should <b><span style='color:var(--mk-color-red)'>avoid</span></b>.
#### Implications

It is to use a **sound inference** procedure on $KB$ to <b><span style='color:var(--mk-color-yellow)'>derive another statement</span></b> $\alpha$.

This also means that $KB$ is a subset of true sentences about the real world.

>[!info] Inference rule
>
>Some set of rules which forms suitable premises using a subset of sentences.

>[!info] Sound inference
>
> An inference allows you to move from a premise to a conclusion. A **sound inference** means that the <b><span style='color:var(--mk-color-yellow)'>inference rule you are using is valid</span></b> thus leading to a <b><span style='color:var(--mk-color-green)'>valid conclusion</span></b>.
> 
> An example of a not-sound inference:
> - If $A \implies B$
> - $B$
> - Then $A$ (*which is not true*)

When a sentence is **derived** from the knowledge base by a sound inference procedure ($i$), we can **denote** this using $KB \vdash_{i} \alpha$ (*can be read as $\alpha$ is derived from KB or $i$ derives $\alpha$ from KB*).
<div style="page-break-after: always;"></div>

>[!info] Complete inference
>
>In a inference system (*a set of inference rules*), it is complete if it can <b><span style='color:var(--mk-color-yellow)'>derive any conclusion that is true</span></b>.
>
>What is means is that given a $KB$ if $A$ when derived is true then our <b><span style='color:var(--mk-color-yellow)'>inference system must be able to derive</span></b> $\color{orange}{A}$, if not it is not complete.

![[Logical Representation & Reasoning.png|center|500]]

Essentially we are representing aspects of the world through sentences and we can use entailment to find new rules of the world which was not included previously.

# Propositional Logic
---
In propositional logic, what we use to write well-formed sentences is called <b><span style='color:var(--mk-color-turquoise)'>propositions</span></b>.

>[!abstract] Propositions
>
>Also known as <b><span style='color:var(--mk-color-turquoise)'>atomic sentences</span></b>, & in propositional logic, their syntax contains the following:
>- English alphabets with or without an index (*literal*)
>- Logical values `true` or `false`

If 2 or more propositions are used with symbols, ($\land$ (*conjunction*), $\lor$ (*disjunction*), $\lnot$ (*negation*), $\iff$) then it is called a <b><span style='color:var(--mk-color-turquoise)'>compound proposition</span></b> (*or complex sentences*).

>[!example] Examples of complex sentences
>
>- $A \land B$
>- $(A)$
>- $A \implies B$
>- $\lnot A$

Propositional logic is both:
- **Declarative** - The knowledge base is declared & inference depends on the domain
- **Compositional** - The meaning of a sentence is a function of the meaning of the parts

>[!important] Operator precedence
>1) Parentheses (*brackets*)
>2) $\lnot$ (*Not or negation*)
>3) $\land$ (*and*)
>4) $\lor$ (*or*)
>5) $\implies$ (*implies or implication or if-then statements*)
>6) $\iff$ (*if and only if*)
<div style="page-break-after: always;"></div>

## Semantics

Semantics is a set of rules **tells** you, given a sentence and a assignment of variables (*model*), **weather the sentence is true or false**.

>[!example] Simple example of semantics
>
>So given $A \land B$, semantics will tell us that for this statement to be true, A and B must be true.

The result of this assignment is called the <b><span style='color:var(--mk-color-turquoise)'>truth value</span></b> of the proposition.

>[!summary] Basically if the truth value is true then the proposition is true and vice versa

**Truth Table**
![[Truth Table.png|center]]
### Validity

Given a sentence $\alpha$:
- It is **valid** if it is <b><span style='color:var(--mk-color-green)'>true for all models</span></b>
- It is a **tautology**, meaning it is necessarily true. Which means it will be <b><span style='color:var(--mk-color-yellow)'>true regardless of the truth value</span></b>.
- It is a **contradiction** if it is <b><span style='color:var(--mk-color-red)'>false for all models</span></b>

>[!note] Deduction Theorem
>
>For any sentence, if $\alpha \models \beta \iff \alpha \implies \beta$
>
>The intuition behind this is that given a $KB$ and we derive $\alpha$ which leads us to derive $\beta$. Then essentially $\beta$ is true when $\alpha$ is true.
>
>To prove that this is correct we can also prove that $\alpha \land \lnot \beta$ (*implication & de morgans*) <b><span style='color:var(--mk-color-red)'>cannot be satisfied</span></b>.

# Model Checking
---
Model checking is the process of <b><span style='color:var(--mk-color-yellow)'>enumerating all possible worlds and finding models in which is true</span></b> for $\alpha$ and $KB$, thus proving entailment.

We can solve weather a particular set of sentences is satisfiable or not through using a <b><span style='color:var(--mk-color-turquoise)'>Boolean satisfiability problem</span></b> (*SAT*) solver. It is **similar to CSP thus the techniques can be used here**.

>[!example] Popular SAT Algorithms
>
>- Davis-Putnam algorithm (*Intelligent backtracking + random restarts*)
>- WalkSat (*Randomised local search, cannot detect unsatisfiability*)
<div style="page-break-after: always;"></div>

# Theorem Proving
---
To prove entailment, in theorem proving our goal is to <b><span style='color:var(--mk-color-yellow)'>derive</span></b> $\alpha$ from $KB$ <b><span style='color:var(--mk-color-yellow)'>using a inference algorithm</span></b> ($i$).

We need to apply **inference rules** to construct a **proof**:
- Valid inference rules in derivation system
- Forward chaining rules
- Backward chaining rules
- Resolution rules

>[!success] Theorem proving is more efficient if the size of the model is large since we do not need to construct all models
## Basic Inference Rules

>[!info] Modus Ponens
>
>One of the best known rules it just states that given $\alpha \implies \beta$ and $\alpha$ is given then we can always infer $\beta$.

We can use a list of logical equivalences as inference rules as well:
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
	
13) **Bidirectional Law**
	$p \iff q \equiv ((p \implies q) \land (q \implies p))$
## Deduction System

A <b><span style='color:var(--mk-color-yellow)'>set of inference rules</span></b> is known as a **deduction system**.

**A complete and sound deduction system**
![[Complete Deduction System.png|center|450]]
## Resolution

It is a powerful rule which <b><span style='color:var(--mk-color-yellow)'>by itself is sound & complete</span></b>.

A **resolution based theorem prover** can for any 2 sentences it can decide if they are <b><span style='color:var(--mk-color-yellow)'>entailed or not</span></b>.

It uses proof by contradiction on the statement $\alpha \land \lnot \beta$ (*unsatisfiable*).

>[!important] Resolution rule only applies to clauses, thus we need to convert to a conjunctive normal form (CNF)
>
>Essentially in a CNF, it contains:
>1) **Conjunctive of clauses** ($\text{clause}_{1} \land \text{clause}_{2} \land \text{clause}_{3}$)
>2) A clause is a **disjunction of literals** ($A \lor B \lor \lnot C$ or $A$)

**Resolution rule**:
$$
(A \lor P), (B \lor \lnot P) \models A \lor B
$$
Where:
- $A$ and $B$ are (disjunctive) clauses
- $P$ is a literal

If $A \lor B$ has copies of the same literal then we will remove all but one of them, this is known as **factoring**.

What this rule means is that no matter what value of $P$ is the statement $A \lor B$ will <b><span style='color:var(--mk-color-green)'>always be true</span></b>.

If we have $P$ and $\lnot P$, then we will get an <b><span style='color:var(--mk-color-yellow)'>empty clause</span></b>, thus a <b><span style='color:var(--mk-color-red)'>contradiction</span></b>.

>[!question] Why does it use proof by contradiction?
>
>We know that $KB \models \alpha$ means that $KB \implies \alpha$ is <b><span style='color:var(--mk-color-green)'>valid</span></b>.
>
>The counter to this is if we can show that $KB \land \lnot \alpha$ is <b><span style='color:var(--mk-color-red)'>unsatisfiable</span></b>. So what resolution does is that it adds $\lnot \alpha$ into $KB$ and checks if it causes $KB$ to have 2 <b><span style='color:var(--mk-color-yellow)'>statements contradict one another</span></b>.
>
>If it happens than $KB \land \lnot \alpha$ can never exist.

**Resolution algorithm**:
```cpp
bool PL_RESOLUTION (KB, A) {
	clauses = set of clauses in CNF representation of KB and not A;
	new = [];
	while true {
		for each pair of clauses Ci and Cj in clauses {
			resolvents = PL_RESOLVE(Ci, Cj); // Use the resolution rule to find all possible new clauses
			if (resolvents.isEmpty()) { // Constrdiction
				return true;
			}
			new = new union resolvents;
			if (new subset clauses) { // Means we did not reach a contradiction thus KB does not entail A
				return false;
			}
			clauses = clauses union new;
		}
	}
}
```

>[!tip] For resolvents which resolves to true does not need to be added into the set of clauses
>
>For instance $A \lor \lnot A$ will always be true thus we do not need to put inside our KB.

# Horn Clauses & Definite Clauses
---
>[!info] A definite clause is a disjunction of literals where exactly one is positive
>
>For example $\lnot A \lor \lnot B \lor C$
>
>Here only C is positive.

>[!info] A horn clause is a disjunction of literals where at most one is positive
>
>For example $\lnot A \lor \lnot B \lor C$ or $\lnot A \lor \lnot B$

A definitive clause can be written as an implication with a **body** (*premise*) and a **head** (*conclusion*), $\lnot A \lor \lnot B \lor C  \equiv A \land B \implies C$:
- $A \land B$ is the body
- $C$ is the head

>[!question] Why does this implication work?
>
>For the implication to fail we need A and B to be true and C to be false, but by doing so the clause is false thus the implication is correct.
>
>This will be **used in forward and backward chaining**.

Deciding on **entailment** with horn clauses can be <b><span style='color:var(--mk-color-green)'>done in linear time</span></b> (`O(KB)`):
- Only modus ponens is used
- Uses forward chaining & backwards chaining
- Basis for logic programming
## Forward Chaining

**Forward chaining** is using the knowledge base of definitive clauses <b><span style='color:var(--mk-color-yellow)'>can it entail the query</span></b> ($\alpha$).

**Forward chaining algorithm**:
```cpp
bool forwardChaining(KB, query) {
	// KB is a set of definite clauses
	count; // A variable to store the number of symbols for each clause in the KB
	inferred; // A hasmap to keep track of all seen symbols
	queue; // A queue which will hold symbols which are true
		
	// First: Add all symbols which are true to the queue
	for (clause : KB) {
		if (clause == symbol) {
			q.push(clause);
		}
	}
	
	while (!queue.isEmpty()) {
		symbol = queue.pop();
		if (symbol == query) {
			return true; // KB entails our query then just stop and return true
		}
		if (infered[symbol] == false) { // Is like a visited but for the symbols
			infered[symbol] = true;
			for (clause : KB) {
				if  (symbol in clause.premise) {
					count[clause]--; // We have satisfy one of the symbols
				}
				if (count[clause] == 0) { // Means that our implication is true
					queue.push(clause.conclusion);
				}
			}
		}
	}
	return false;
}
```
## Backward Chaining

**Backward chaining** is using the query ($\alpha$) and trying to <b><span style='color:var(--mk-color-yellow)'>work back from the goal</span></b>.

>[!info] This is also known as a and-or graph search
>OR branches asks which rule can I use to prove the goal
>
>AND branches asks which premises do I need to prove the rule

**Backward chaining algorithm**:
```cpp
vector<string> andOrSearch (problem) {
	// Here problem is our knwledge base
	// Initial will be the query
	return orSearch(problem, problem.Initial, vector<string> path);
}

// state will be the propositional we want to solve
// The path is used to detect cycles
vector<string> orSearch(problem, state, path) {
	if (problem.isGoal(state)) { // Goals are symbols in the knowledge base that are true (Literals)
		return path;
	}
	if (isCycle(path)) { // If the state is in the path means we will eventually loop back
		return failure; // There is a cycle and we cannot continue
	}
	for (rule :  problem.actions(state)) { // For each rule whoes conclusion is the same as our state
		// Do an AND search on the symbols in the premis
		plan = andSearch(problem,  result(state, action), path.push_back(state)) ;
		if (plan != failure) {
			return action + plan; 
		}
	}
	return failure;
}

vector<string> andSearch(problem, states, path) {
	vector<string> plans;
	for (state : states) {
		plan = orSearch(problem, state, path);
		if (plan == failure) {
			return failure;
		}
	}
	return firstPlan // Return the first non failure plan in the plans
}
```