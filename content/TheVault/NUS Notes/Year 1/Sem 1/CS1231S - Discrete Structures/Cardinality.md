---
Title: Cardinality
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1231S
  - Math/Logic
---
# Cardinality
---
Let A and B be <span style='color:#f7b731'>finite sets</span> 

**Pigeonhole Principle**
If $f: A  \rightarrow B$ and it is [[Functions#Properties of Functions|Injective]], then $\vert A \vert \le \vert B \vert$

Because its a one to one relation, all X will be mapped to one Y

**Dual Pigeonhole Principle**
If $f: A  \rightarrow B$ and it is [[Functions#Properties of Functions|Surjective]], then $\vert A \vert \ge \vert B \vert$

Because all y must be mapped to some x, but multiple x can be mapped to some Y
## Finite set and Infinite Set

Let $\Bbb Z_{n} = \{1,2,3,\dots,n\}$, a set S is to be <span style='color:#0fb9b1'>finite</span> if and only if <mark class="hltr-orange">S is empty or there exists a bijection</mark> from S to $\Bbb Z_{n}$ for some $n \in \Bbb Z^{+}$

$2\Bbb Z$ is the set of all even integers

<span style='color:#eb3b5a'>Else</span> S is <span style='color:#0fb9b1'>infinite</span>

**Equality of Cardinality of Finite Sets** (Cantor's Definition of Cardinality)
> Let A and B be any infinite sets then $\vert A \vert = \vert B \vert$  if and only if there is a <mark class="hltr-orange">bijection</mark> $f: A \rightarrow B$

### Properties of Cardinality

Let A, B , C be some sets

**Reflexive**
> $\vert A \vert = \vert A \vert$

**Symmetric**
> $\vert A \vert  = \vert B \vert \rightarrow  \vert B \vert  = \vert A \vert$

**Transitive**
> $(\vert A \vert  = \vert B \vert) \land  (\vert B \vert  = \vert C \vert) \rightarrow  \vert A \vert  = \vert C \vert$

For <span style='color:#0fb9b1'>infinite</span> sets if there is a <mark class="hltr-orange">bijective function</mark> that maps the 2 sets, then $A \subsetneq B$ (Proper Subset) and also they have the <span style='color:#f7b731'>same cardinality </span>

Therefore another way to denote a infinite set is through $(B \subseteq A) \land (B \ne A) \land (\vert B \vert = \vert A \vert)$ if for set A there is another set B

# Countable Infinite
---

The set $\Bbb Z^{+}$ is the set of all positive integers which is the most basic of infinite sets 

Any set $A$ that has the same cardinality as $\Bbb Z^{+}$ is called <span style='color:#0fb9b1'>countably infinite </span>. Or <mark class="hltr-orange">if there is some bijection between</mark> any set to $\Bbb Z^{+}$ will also be <span style='color:#0fb9b1'>countably infinite</span>
	With this, $\Bbb Z$ and $\Bbb Q^{+}$ is all countable

**Cardinal Numbers**
> $\aleph_0$ = $\vert \Bbb Z^{+} \vert$ 

$\aleph_0$ is pronounced as aleph which refers to only countable infinity

A set S is said to be <span style='color:#0fb9b1'>countably infinity</span> if and only if $\vert S \vert = \aleph_0$ and it it is not countable then it will be <span style='color:#0fb9b1'>uncountable</span>

**Theorem Cartesian Product**
> If Sets A and B are countably infinite then so it $A \times B$

**Corollary (General Cartesian Product)**
> Given $n \ge 2$ countably infinite sets, the cartesian product of all n sets is also countably infinite

**Theorem (Unions)**
> The union of n countably infinite sets is also countable

$$\bigcup^{\infty}_{i = 1} A_{i} $$
# Countability on Sequences
---

**Countable**
> A set is <span style='color:#0fb9b1'>countable</span> if and only if it is <span style='color:#f7b731'>finite</span> or it is <span style='color:#f7b731'>countably infinite</span>

A set is countable if and only if there is a sequence where <mark class="hltr-orange">every element in the set appears exactly once in the sequence</mark> or if <mark class="hltr-orange">there is a sequence in which every element of B appears</mark> (There are extra numbers in the sequence)

Therefore to prove this, the 2 sets <span style='color:#f7b731'>must be injective and surjective</span>.

# Larger Infinities
---
**Theorem 7.4.2 (Cantor)**
> A set of real numbers between 0 and 1 is <span style='color:#0fb9b1'>uncountable</span>

**Theorem 7.4.3**
> Any subset of a set that is countable is also countable

**Theorem 7.4.4**
> Any subset of a set that is uncountable is also uncountable

**Proposition 9.3**
> Every infinite set has a countably infinite subset

**Lemma 9.4 Union of Countably Infinite Sets**
> Sets A and B are countable infinite sets, then $A \cup B$ is countable '

**The Continuum Hypothesis**
> $\aleph_{0}\lt \vert A \vert \lt \vert \Bbb R \vert$ is undeciable 