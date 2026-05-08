---
Title: Methods Of Proof
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1231S
  - Math/Logic
  - Math/Proofs
---
# Direct Proof and Counter Example
---
## Proof By Construction

Given a <span style='color:#0fb9b1'>existential statement</span>, $\exists x \in D, Q(x)$, is true if and only if $Q(x)$ is <span style='color:#f7b731'>true for at least one x in the set D</span>.

To prove this statement, <span style='color:#f7b731'>find a value for x in the set D</span> which makes $Q(x)$ true, this is called a <span style='color:#f7b731'>constructive proof of existence</span>.
## Proof By Counterexample

Given a <span style='color:#0fb9b1'>universal</span> (conditional) <span style='color:#0fb9b1'>statement</span>, $\forall x \in D (P(x) \rightarrow Q(x))$ is <span style='color:#f7b731'>false if the negation of this statement is true</span>, $\exists x \in D (P(x) \land \lnot Q(x))$.

<span style='color:#f7b731'>Find a value x in the set D</span> for which the <span style='color:#0fb9b1'>hypothesis</span> ($P(x)$) is <span style='color:#f7b731'>true</span> but the <span style='color:#0fb9b1'>conclusion</span> ($Q(x$) is <span style='color:#f7b731'>false</span>.
## Proof By Exhaustion

Given a <span style='color:#0fb9b1'>universal</span> (conditional) <span style='color:#0fb9b1'>statement</span>, $\forall x \in D (P(x) \rightarrow Q(x))$ is <span style='color:#f7b731'>true if all values of x is true</span>.

If <span style='color:#f7b731'>D is finite</span>, then the statement can be proven true through <span style='color:#0fb9b1'>exhaustion</span> where every value will be checked to see if the statement is true.
## Proof By Generalizing from the Generic Particular

This will be used for a <span style='color:#f7b731'>domain with a infinite size</span>. If it can be proven that every element of a set satisfies a certain property and supposed x is a <span style='color:#f7b731'>particular but arbitrarily chosen element</span> results in the statement being true.

# Indirect Proof
---
Sometimes a <span style='color:#0fb9b1'>direct proof</span> is <span style='color:#f7b731'>difficult to derive</span>, thus an <span style='color:#0fb9b1'>indirect proof </span>can be used.

## Proof By Contradiction

Given a statement (S) to be proved true. Therefore the <span style='color:#0fb9b1'>negation</span> of the statement ($\lnot S$) is false. Show that the <span style='color:#f7b731'>supposition</span> (negation) <span style='color:#f7b731'>leads to a contradiction</span> and thus the statement is true.

## Proof By Contraposition

Contrapositive : $P \rightarrow Q$ is $'\lnot Q \rightarrow \lnot P'$

The contrapositive can be used to prove the statement is true since they are equivalent. Thus if the <span style='color:#f7b731'>contraposition can be proven true then the statement is also true</span>. 