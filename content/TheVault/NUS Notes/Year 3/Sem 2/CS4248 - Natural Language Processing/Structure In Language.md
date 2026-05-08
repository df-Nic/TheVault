---
Title: Structure In Language
Date Created: 03-February-2026
Last Updated: 27-April-2026
Tags:
  - DSA3362
  - AI/NLP/TextProcessing
---
# Sequences
---
So far we have looked at strings as a sequence of words. However <b><span style='color: #FFD700'>languages have their own grammatical rules</span></b>.

In **classic NLP models**, a document is just a <b><span style='color: #87CEEB'>bag of words</span></b> (*BoW*).

>[!info] Bag of words
>A bag can be a whole document or the context of a word. But essentially it <b><span style='color: #FFD700'>represents text by just counting the frequencies</span></b> & ignoring language structure.

>[!important] In natural language the order of the word matters
>We can get very different meanings with the same set of words.

There are some **fundamental rules** to word order (*for English*):
- Subject verb object (*SVO*)
- Adjectives only before nouns
- and many more ..

There are also **informal rules** which we <b><span style='color: #FFD700'>do not need to follow, but they make sentences more coherent</span></b>.

>[!example] An example of a informal rule is the order of adjectives

There are different **types of sequence tasks**:
1) **Sequence classification** (*many to 1*)
	- Sentiment analysis
	- Document categorisation
2) **Sequence labeling / tagging** (*many to many*)
	- Part of speech tagging
	- Named entity recognition (*Tagging abbreviations like US to United States*)
3) **Sequence translation** (*many to many*)
	- Machine translation
	- Sentence simplification
	- Text summarisation
4) **Sequence generation** (*one to many*)
	- Image captioning
## Part Of Speech (POS) Tagging

>[!abstract] Part of speech (POS)
>They are also known as <b><span style='color: #87CEEB'>word classes</span></b> or <b><span style='color: #87CEEB'>syntactic category</span></b>.
>
>Essentially they are your nouns, verbs, adjectives, proposition, conjunction, and many more.
>
>In English there are 8 main POS but there are also many classes & subclasses.

In POS tagging our goal is simply to <b><span style='color: #FFD700'>assign each word to a part of speech</span></b>.

>[!example] Example of POS tagging
>Given a text "Bob walked slowly":
>- Bob is a proper noun singular
>- walked is a verb past tense
>- slowly is a adverb

>[!abstract] Penn Treebank Tag-Set
> In the English language the, it is a <b><span style='color: #FFD700'>widely used standardised set of 36 POS tags & 12 punctuation / symbols tags</span></b>.

These different tags can fall under **2 categories**:
- **Closed** class words, which means a <b><span style='color: #FFD700'>fixed set</span></b> of words (*like your pronouns, conjunctions, prepositions, etc*) typically they <b><span style='color: #FFD700'>structure sentences</span></b> (*the, an, a, them, etc*)
- **Open** class words, which means there is <b><span style='color: #FFD700'>no fixed set</span></b> & new words can be invented, borrowed etc (*like your nouns, verbs, adjectives, adverbs*)

**POS tagging is regarded** as a <b><span style='color: #FFD700'>important low-level NLP task</span></b>. It is used to build applications as well. For instance knowing the **POS can actually be used as additional features** which can be used to train our model.

Some useful downstream tasks which requires POS:
- Named entity recognition
- Information extraction
- Parsing
- Speech synthesis / recognitions
- Authorship attribution
- Machine translation
### Ambiguity Challenges

The task of <b><span style='color: var(--mk-color-red)'>POS tagging is actually a difficult task</span></b> to do. And the main issue is <b><span style='color: var(--mk-color-red)'>ambiguity</span></b>, even with additional context provided.

>[!info] Ambiguous words
>In POS it means that a <b><span style='color: #FFD700'>word as 2 or more possible POS tags</span></b> & it depends on the text corpus.

>[!example] Example of how ambiguity can affect the tagged POS
>Given a sentence "Flying planes can be dangerous". The **word flying is it a verb or a adjective?**
>
>This sentence can mean that flying a plane is dangerous or that a flying plane is dangerous.

If we look at the English language:
- 85% of the word types are unambiguous
- 15% of the word types are ambiguous

>[!warning] So what is the problem now?
>Take **any word corpus**, we can expect around <span style='color: var(--mk-color-red)'>55-65% of word tokens are ambiguous</span>.
>
>This means that **ambiguous words** though accounts for 15% of the word types are <b><span style='color: var(--mk-color-red)'>very commonly used</span></b>.
### Algorithms For POS Tagging

Lets start with the most **straight forward approach**:
1) <b><span style='color: #FFD700'>Label each word with its most frequent POS tag</span></b> within the corpus
2) For **unknown words** (*OOV*) <b><span style='color: #FFD700'>label them as nouns</span></b> (*most common open word class*)

This results in about **92% accuracy** as compared to state of the art methods (*97-98% accuracy*). However there are **2 main problems** to this approach.

>[!fail] Imbalanced errors
>This is mainly due to Zipf's Law where words like 'the', 'a' are <b><span style='color: var(--mk-color-red)'>unambiguous words but occur very often</span></b>.
>
>These <b><span style='color: var(--mk-color-red)'>words also does not carry information</span></b> as compared to verbs, nouns which are ambiguous.

>[!fail] Downstream error propagation
>Due to bad POS tagging, it will affect other tasks which requires these POS tags.
#### Unsupervised Algorithms

The idea is to utilised the POS tags from unambiguous words, these are also known as <b><span style='color: #87CEEB'>anchor words</span></b> (*only 1 POS tag*).

We <b><span style='color: #FFD700'>observed patterns to group words into clusters of the same word class</span></b>. Then we use the anchor word to <b><span style='color: #FFD700'>assign this group to its POS tag</span></b>.

>[!example] An example of this unsupervised algorithm
>Assuming our anchor word happiness is a noun. Then we observed the following:
>- "I want happiness"
>- "I want pizza"
>- "I want freedom"
>
>We notice that I want comes before "happiness" & same goes for "pizza" & "freedom". So they will all be group into 1 cluster & be tagged with noun. 

>[!success] No need for hand-labeled text corpora
>We only need the lexicon of the anchor words (*starting anchor words with their POS tags*). The rest will be handled by the algorithm.

>[!fail] Poorer performance as compared to supervised methods
#### Supervised Methods

Here these are your typical models such as:
- Hidden Markov Models (*HMM*)
- Conditional Random Fields (*CRF*)
- Neural sequence models (*RNNs, Transformers*)
- Large language models (*BERT*)

All these <b><span style='color: #FFD700'>requires hand-labeled text corpus</span></b> for training of the supervised models.

However **POS tagging** is considered a <b><span style='color: #FFD700'>solved tasks for high-resource languages</span></b> (*English*) & models have reached <b><span style='color: #98FB98'>accuracies that are "human ceiling"</span></b>.

>[!fail] The only challenge comes for low-resource languages
>These are the languages which are <b><span style='color: var(--mk-color-red)'>lacking in large annotated datasets</span></b>.
#####  Hidden Markov Models

![[Hidden Markov Models Example.png|center|300]]

Essentially it is our [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Introduction to Neural Networks.md|neural network]] where it is training hidden states to <b><span style='color: #FFD700'>predict the POS tags based on what was seen before</span></b>.

There are **2 important values** to take note of:
- **Transition** value (*Probability of going from 1 POS tag to another*)
- **Emission** value (*Probability of the word appearing given this POS tag*)

Then for each layer we combine the values to find the <b><span style='color: #FFD700'>largest probability path</span></b> & the sequence of POS tags will be what our sentence will be tagged with.
##### Recurrent Neural Networks

One example will be to use BI-LSTM or [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Neural Network on Sequential Data.md#Long Short-Term Memory|LSTM]].

![[LSTM POS Tagging Example.png|center|500]]

>[!fail] Using LSTM we do not consider past POS only past words
>So take the 4th probability, we only take into account the past 4 words but not taking into account we saw a noun, verb & another verb. 
# Syntactic Parsing
---
Unlike POS tagging where we assign each word in a sentence a part of speech tag, for **syntactic parsing** we are interested in <b><span style='color: #FFD700'>how multiple words are formed to give some meaning</span></b>, which are then combined to form sentences.

So we are <b><span style='color: #FFD700'>extracting all possible parses</span></b> (*meaning*) for a particular sentences. Afterwards we need to **do** <b><span style='color: #87CEEB'>syntactic disambiguation</span></b>, where we <b><span style='color: #FFD700'>score the all parses</span></b> (*probability*) and return the best one.

>[!note] To do syntactic disambiguation we require some dataset
## Constituency Parsing

>[!abstract] Constituent
>It is also known as a <b><span style='color: #87CEEB'>phrase structure</span></b>. It is a <b><span style='color: #FFD700'>group of words that behaves as a single unit or phrase</span></b>.

**Sentences** can be described as a <b><span style='color: #FFD700'>hierarchical structure of constituents</span></b> (*parse trees*).

So to form constituents, the **simple answer** is just to <b><span style='color: #FFD700'>group words that make sense on its own</span></b>. A more **formal answer** is <b><span style='color: #FFD700'>constituency tests</span></b>.

Here are some examples of constituency tests:
- **Tropicalization**, where a constituent can be <b><span style='color: #FFD700'>moved to different locations of the sentence</span></b> & still keeps the sentence correct
- **Proform substitution**, where a constituent can be <b><span style='color: #FFD700'>substituted with a proform</span></b> (*it, that, them, they, there*)
- **Fragment answers**, where a <b><span style='color: #FFD700'>constituent can answer a question</span></b> regarding the original sentence

>[!example] An example of fragment answer
>Given the sentence "Alice was hit by the green car". The question can be "Who hit Alice?"
>
>The answer is the green car and thus "the green car" is the constituent.

Some **popular algorithms** for constituency parsing:
- Cocke-Youngler-Kasami (*CYK*) algorithm, a bottom up approach to find which non-terminals can generate this substring 
- Earley parser, a top down algorithm so given what was seen what grammar rules might still be in progress (*determines other parses*)
### Context Free Grammars

The most common way to <b><span style='color: #FFD700'>capture constituency & ordering is by nesting words together</span></b>.

The idea is that we define meaningful constituents & <b><span style='color: #FFD700'>how more constituents is formed out of other constituents</span></b>.

>[!success] More powerful than RegExs as they can express recursive structure

There are **2 types of symbols** used in rules:
1) **Non-terminal** symbols, can be <b><span style='color: #FFD700'>replaced with other symbols</span></b> according to the rules (*phrase names, POS*)
2) **Terminal** symbols, is an <b><span style='color: #FFD700'>output of a rule</span></b> that cannot be changed or replaced further (*words / tokens*)

>[!abstract] Rules or Productions
> It can be in the form of $S \rightarrow \text{NP VP}$ or $\text{Det} \rightarrow \text{a | the}$ (*for this choose either one not all*).
> 
> Formally:
> - $N$ is the set of all non-terminal symbols
> - $\sum$ is the set of all terminal symbols
> - $R$ is the set of rules where $A \rightarrow \alpha$ means that $A \in N, \alpha \in (N \cup \sum)$
> - $S$ is a special start symbol
> 
> In general a rule states that when <b><span style='color: #FFD700'>encountering the symbol on the left we can replace it with the symbols on the right</span></b>.
> 
> The only constraint is that the <b><span style='color: #FFD700'>left hand side must be a single non-terminal</span></b> symbol.

>[!question] Why is this called context free?
>This is because for all rules the left hand side can only be 1 symbol and no more. This means it <b><span style='color: #FFD700'>does not care what comes before or after</span></b>.

**Applying these rules in any order** will <b><span style='color: #98FB98'>always result in a grammatically correct sentence</span></b> (*but whether it makes sense that is another story*).

We can **visualise the application** of these rules through a <b><span style='color: #87CEEB'>parse tree</span></b>:
![[Parse Tree Example.png|center|450]]

These trees can be used for:
- Grammar checking
- Keyphrase extraction
- Semantic analysis
- Question answering
- And more...
#### Structural Ambiguity Challenges

For structural ambiguity it means that for a given phrase there can be many ways to interpret it. So the problem is that <b><span style='color: var(--mk-color-red)'>grammar can assign more than one parse to a sentence</span></b>.

There are **2 common types** of structural ambiguity:
1) **Attachment** ambiguity, which is when a particular <b><span style='color: #FFD700'>constituent can be attached to the parse tree at more than 1 place</span></b>

>[!example] Example of an attachment ambiguity
>Given the sentence "I book the flight through Singapore".
>"through Singapore" can be attached to noun phrase related to "flight" meaning you will fly past Singapore.
>
>Or it can be attached to verb phrase related to "book", meaning you book through Singapore (*yes it means that Singapore is a person / agency*).

2) **Coordination** ambiguity, which is when <b><span style='color: #FFD700'>phrases can be conjoined by conjunctions</span></b> (*and, or but, if, because, etc*) or the different types of conjunctions (*coordinating, correlative*)

>[!example] Example of an coordination ambiguity
>Given the sentence "SIA has the best meals and entertainment".
>Does "best" refer to both meals & entertainment or just meals only but not entertainment?
#### Probability of a Parse Tree

We can handle ambiguity by <b><span style='color: #FFD700'>assigning probabilities to rules</span></b>. So given a dataset we want to know:
$$
P(A \rightarrow \alpha) = P(\alpha \vert A) = \frac{\text{Count}(A \rightarrow \alpha)}{\text{Count}(A)}
$$


>[!important] For rules that transforms to non-terminal symbols, the probabilities will sum to 1 for rules which LHS are the same symbol

>[!important] For rules that transforms to terminal symbols, the probabilities to transform to any of the terminal symbol will sum to 1 
>Basically RHS probabilities all sum to 1.

So the **probability of a parse tree** is just the product of the <b><span style='color: #FFD700'>probabilities of all rules</span></b>:
$$
P(T, S) = \prod^{n}_{i} P(A \rightarrow \alpha) = \sum^{n}_{i} \ln P(A \rightarrow \alpha)
$$
>[!note] We sum the log probabilities to avoid arithmetic underflow
## Dependency Parsing

Here we <b><span style='color: #FFD700'>express sentences in terms of dependencies between the tokens</span></b>, this grammar type is known as <b><span style='color: #87CEEB'>dependency grammar</span></b>.

There are **2 parts** to this:
1) <b><span style='color: #FFD700'>Identify pairs</span></b> of related words
2) <b><span style='color: #FFD700'>Identify type/label</span></b> of the relationship between words

![[Dependency Parsing Example.png|center|200]]

In a **dependency relationship**:
- It is a <b><span style='color: #FFD700'>directed</span></b> relationship
- There is <b><span style='color: #FFD700'>1 head & 1 dependent</span></b> (*the dependent modifies the head*)
- The labels are taken from a [predefined set](https://universaldependencies.org)

To identify the head ($H$), dependent ($D$) in a construction ($C$):
- H determines the syntactic category of C
- H can often replace C
- H determines the semantic category of C
- D gives semantic specification
- H is obligatory; D may be optional
- H selects D and determines whether D is obligatory or optional
- The form of D depends on H (agreement or government)
- The linear position of D is specified with reference to H

There are a some **dependency types**:
- **Head-complement** (*dobj, iobj, nsubj*), it means that the <b><span style='color: #FFD700'>dependent is required</span></b> to complete the meaning of the head
- **Head-modifier** (*amod, advmod*), the <b><span style='color: #FFD700'>dependent is optional</span></b>, it adds extra information but not necessary for grammar
- **Head-specifier** (*det*), it <b><span style='color: #FFD700'>specifies the head</span></b>, typically it is a determiner-noun relation
- **Coordination** (*conj, cc*), <b><span style='color: #FFD700'>unsure of of where the head is</span></b> so the word can be linked to 2 heads, but is usually resolved by parser

There are many algorithms that does dependency parsing, though each have different implementations but **typically 2 main components/steps**:
1) Fixed parsing algorithm (*symbolic, not learned*)
2) Learned scoring model (*trained on annotated data*)

Main difference between various algorithms: scoring model
- "Classic" models (e.g., Logistic Regression, SVM)
- Neural models (e.g., FFNN, RNN/LSTM/GRU, CNN, Transformer)

>[!example] spaCy open-source NLP library
>It has different algorithms available depending on "language model". Typical choices are, FFN, CNN, or Transformer for scoring model
### Applications For Dependency Parsing

1) **Rule based text simplification**

An example will be <b><span style='color: #87CEEB'>appositions</span></b>, they are basically <b><span style='color: #FFD700'>2 noun phrases next to each other referring to the same entity</span></b>.

So when **spotting this dependency** we can:
- <b><span style='color: #FFD700'>Remove</span></b> apposition
- <b><span style='color: #FFD700'>Split</span></b> the sentence

>[!example] Example of text implication through identifying appositions
>Assume we have a sentence "Musk the CEO of Tesla bought Twitter".
>
>If we were to **remove appositions**: "Must bought Twitter".
>
>If we were to **split appositions**: "Musk bought Twitter. Musk is the CEO of Twitter".

There is also <b><span style='color: #87CEEB'>relative clauses</span></b> (*relcl*) which we can also use to do text simplification.

2) **Information extraction**

Essentially we want to <b><span style='color: #FFD700'>build a knowledge graph</span></b> based on the given text. And this can be used to detect contradicting statements.

>[!info] Knowledge graphs
>They are essentially a larger <b><span style='color: #FFD700'>set of subject, predicate, object triples</span></b>.
>
>Essentially 2 objects (*subject, object*) and the relationship between them (*predicate*).

We can <b><span style='color: #FFD700'>use dependencies to generate our triplets</span></b>. The most basic example is using a subject of sentence (*nsubj*), a verb (*active form*) & a direct object (*dobj*).

>[!example] Example of information extraction
>Assume we have a sentence "Yesterday, Alice ate the tasty cake"
>
>So "ate" is a verb, then it has a relationship to "Alice" which is a subject of the sentence & "cake" which is the direct object.
>
>So we can have these potential triplets:
>- (Alice, ate, cake)
>- (Alice, ate, tasty cake)
>- (Alice, eat, cake)
>
>So you can tell from this example it is <b><span style='color: var(--mk-color-red)'>not obvious which is the correct triple</span></b> which makes it hard to form it through plain text.

>[!fail] It can be hard to extract triplets
>Lets say we have a <b><span style='color: var(--mk-color-red)'>negation</span></b> (*not*) so do we extract the triplet and make it (Alice, not eat, cake) or do not extract it?
>
>What about <b><span style='color: var(--mk-color-red)'>"uncertainty"</span></b>, do we not extract or extract multiple triplets capturing the relationship between statements?



